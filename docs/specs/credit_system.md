# Credit System Specification

## Domain Models

```ruby
create_table :credit_ledgers do |t|
  t.references :organization, null: false, foreign_key: true
  t.integer :balance, null: false, default: 0
  t.integer :monthly_allowance, null: false
  t.date :reset_date, null: false
  t.datetime :last_warning_at
  t.timestamps

  t.index [:organization_id, :reset_date]
end

create_table :credit_transactions do |t|
  t.references :organization, null: false, foreign_key: true
  t.references :user, null: false, foreign_key: true
  t.references :report_execution, foreign_key: true
  t.integer :amount, null: false
  t.string :transaction_type, null: false # debit, credit, refund
  t.jsonb :metadata, null: false, default: {}
  t.timestamps

  t.index [:organization_id, :created_at]
  t.index [:transaction_type, :created_at]
end
```

## Cost Rules

### Base Costs

- Standard query: 1 credit
- Parameterized query: 1 credit
- Scheduled execution: 1 credit

### Multipliers

- Results > 1000 rows: 2x
- Runtime > 30s: 3x
- Export formats: CSV 1x, Excel 2x

## Core Services

```ruby
module Credits
  class ConsumptionService
    def initialize(organization, report_execution)
      @organization = organization
      @execution = report_execution
    end

    def call
      transaction do
        verify_balance!
        calculate_cost
        record_transaction
        update_ledger
      end
    end
  end

  class ResetService
    def call
      Organization.find_each do |org|
        reset_credits(org)
      end
    end
  end

  class RefundService
    def call(transaction_id)
      transaction do
        revert_transaction
        credit_ledger
        log_refund
      end
    end
  end
end
```

### Background Processing

```ruby
class Credits::ResetJob < ApplicationJob
  queue_as :billing
  retry_on StandardError, attempts: 3

  def perform
    Credits::ResetService.new.call
  end
end

class Credits::WarningJob < ApplicationJob
  queue_as :notifications

  def perform(organization_id)
    notify_threshold_reached
  end
end
```

## Testing Strategy

## Unit Tests

```ruby
RSpec.describe Credits::ConsumptionService do
  context 'with sufficient balance' do
    it 'deducts correct credits'
    it 'creates transaction record'
    it 'applies multipliers'
  end

  context 'with insufficient balance' do
    it 'raises InsufficientCredits'
    it 'maintains consistent state'
  end
end
```

## Failure Modes

### Critical

#### Insufficient balance

- Block query execution
- Notify admins/users
- Log attempt

#### Double-spending

- Use transaction isolation
- Lock balances during spend
- Validate after transaction

#### Failed resets

- Retry with backoff
- Alert on consecutive failures
- Manual reset trigger

#### Incorrect multipliers

- Validate before application
- Log all multiplier calculations
- Enable emergency override

### Non-Critical

#### Delayed notifications

- Queue for retry
- Drop after 24h

#### Stale metrics

- Rebuild on detection
- Schedule regular refresh

#### Warning thresholds

- Default to conservative values
- Allow per-org configuration

## Monitoring

### Metrics

#### Credit consumption rate

- Per org/user
- Time-based trends
- Usage patterns

#### Reset success rate

- Failed vs successful
- Reset timing
- Error distribution

#### Refund frequency

- By cause
- By org size
- Patterns

#### Balance distribution

- Per plan tier
- Usage quartiles
- Seasonal patterns

### Alerts

#### Critical: Balance < 10%

- Immediate notification
- Auto-suspension warning
- Admin escalation

#### Warning: Balance < 25%

- User notification
- Usage recommendations

#### Info: High consumption rate

- Pattern detection
- Forecasting alert
- Optimization suggestions

### Integration Tests

- Credit lifecycle
- Reset procedures
- Refund flows
- Race conditions
