# Delivery System Specification

## Domain Models

```ruby
create_table :delivery_targets do |t|
 t.references :report, null: false, foreign_key: true
 t.references :service_connection, foreign_key: true
 t.string :target_type # email, slack, webhook
 t.jsonb :config, null: false, default: {}
 t.boolean :active, null: false, default: true
 t.timestamps

 t.index [:report_id, :target_type]
 t.index [:active]
end

create_table :delivery_attempts do |t|
 t.references :delivery_target, null: false
 t.references :report_execution, null: false
 t.string :status # queued, processing, delivered, failed
 t.jsonb :metadata, null: false, default: {}
 t.integer :retry_count, default: 0
 t.datetime :delivered_at
 t.timestamps

 t.index [:status, :created_at]
 t.index [:delivery_target_id, :status]
end
```

## Delivery Services

```ruby
module Deliveries
 class BaseDeliveryService
   def deliver(execution_id, target_id)
     raise NotImplementedError
   end

   private

   def record_attempt(status:, metadata: {})
     DeliveryAttempt.create!(
       status: status,
       metadata: metadata
     )
   end
 end

 class EmailDeliveryService < BaseDeliveryService
   def deliver(execution_id, target_id)
     result = Mailpace::Client.deliver(
       build_payload(execution_id, target_id)
     )
     record_attempt(status: :delivered, metadata: result)
   end
 end

 class SlackDeliveryService < BaseDeliveryService
   def deliver(execution_id, target_id)
     attachment = build_attachment(execution_id)
     post_to_slack(target_id, attachment)
   end
 end
end
```

## Background Processing

```ruby
class Deliveries::ProcessJob < ApplicationJob
  queue_as :deliveries
  retry_on StandardError, attempts: 3

  def perform(execution_id, target_id)
    target = DeliveryTarget.find(target_id)
    execution = ReportExecution.find(execution_id)

    # Generate and attach report file
    report_data = execution.generate_report
    execution.report_file.attach(
      io: StringIO.new(report_data),
      filename: "report_#{execution_id}.pdf",
      content_type: 'application/pdf'
    )

    service = target.delivery_service.new
    service.deliver(execution_id, target_id)
  end
end

class Deliveries::RetryJob < ApplicationJob
  queue_as :delivery_retries

  def perform(attempt_id)
    attempt = DeliveryAttempt.find(attempt_id)
    return if attempt.retry_count >= 3

    attempt.with_lock do
      attempt.increment!(:retry_count)
      execution = attempt.report_execution

      # Re-attach report if needed
      unless execution.report_file.attached?
        report_data = execution.generate_report
        execution.report_file.attach(
          io: StringIO.new(report_data),
          filename: "report_#{execution.id}.pdf",
          content_type: 'application/pdf'
        )
      end

      Deliveries::ProcessJob.perform_later(
        execution.id,
        attempt.delivery_target_id
      )
    end
  end
end
```

## Failure Handling

### Retry Strategy

- Immediate retry on temporary failures
- Exponential backoff: 5m, 15m, 1h
- Max 3 retries per target
- Dead letter queue after max retries

### Error Categories

#### Temporary (retry)

- Rate limits
- Network timeouts
- Service unavailable

#### Permanent (fail)

- Invalid credentials
- Missing permissions
- Invalid payload

## Monitoring

### Key Metrics

- Delivery success rate
- Average delivery time
- Retry frequency
- Error distribution

### Health Checks

- Service availability
- Queue depth
- Processing latency
- Error rates

## Testing

```ruby
RSpec.describe Deliveries::EmailDeliveryService do
 let(:execution) { create(:report_execution) }
 let(:target) { create(:delivery_target, :email) }

 context 'with valid payload' do
   it 'delivers successfully'
   it 'records attempt'
   it 'updates statistics'
 end

 context 'with service failure' do
   it 'handles retries'
   it 'logs errors'
   it 'maintains consistency'
 end
end
```
