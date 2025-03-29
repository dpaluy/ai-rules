# Service Objects Patterns

Service objects in Ruby on Rails encapsulate business logic while keeping controllers and models focused on their primary responsibilities. Here's a structured implementation guide:

---

## Implementation Steps
1. **Create `app/services` directory**
   `mkdir app/services`

2. **Define base service (optional but recommended)**
   ```ruby
   # app/services/application_service.rb
   class ApplicationService
     def self.call(*args, &block)
       new(*args, &block).call
     end
   end
   ```

3. **Create service class**
   ```ruby
   # app/services/payment_processor.rb
   class PaymentProcessor < ApplicationService
     def initialize(order, user)
       @order = order
       @user = user
     end

     def call
       validate_balance
       charge_card
       send_receipt
     end

     private

     def validate_balance
       # Business logic
     end
   end
   ```

4. **Invoke from controller**
   ```ruby
   # app/controllers/orders_controller.rb
   def create
     @order = Order.new(order_params)
     result = PaymentProcessor.call(@order, current_user)
     # Handle result
   end
   ```

## Best Practices
**Naming & Structure**
- Use verb-noun naming (`PaymentProcessor` vs `ProcessPayment`)[1][21]
- Maintain single responsibility per service[5][7]
- Group related services in namespaces:
  ```
  app/services/
    ├── billing/
    │   ├── invoice_generator.rb
    │   └── payment_processor.rb
    └── social/
        └── tweet_poster.rb
  ```

**Method Design**
- Expose only one public method (`call` by convention)[7][15]
- Return consistent result objects:
  ```ruby
  { success: true, data: result } || { success: false, error: message }
  ```

**Error Handling**
- Use transactions for database operations[6]:
  ```ruby
  def call
    ActiveRecord::Base.transaction do
      # Multiple DB operations
    end
  end
  ```
- Raise custom exceptions for domain errors

## Example: Email Notification Service
```ruby
# app/services/notifications/email_sender.rb
module Notifications
  class EmailSender < ApplicationService
    def initialize(user, template)
      @user = user
      @template = template
    end

    def call
      validate_recipient
      compose_email
      deliver
      log_activity
    end

    private

    def validate_recipient
      raise InvalidRecipientError unless @user.email.present?
    end

    def compose_email
      # Template rendering logic
    end
  end
end
```
Invoke with: `Notifications::EmailSender.call(user, :welcome_email)`

## Advanced Patterns

1. **Form Objects**
   Pair with services for input validation[18]:
   ```ruby
   class RegistrationService < ApplicationService
     def initialize(form)
       @form = form
     end

     def call
       return unless @form.valid?
       # Continue processing
     end
   end
   ```

2. **Dependency Injection**
   Make services testable through DI:
   ```ruby
   class PdfGenerator < ApplicationService
     def initialize(document, renderer: PdfRenderer)
       @document = document
       @renderer = renderer
     end
   end
   ```

3. **Result Objects**
   Standardize service responses:
   ```ruby
   class ServiceResult
     attr_reader :data, :error

     def initialize(success:, data: nil, error: nil)
       @success = success
       @data = data
       @error = error
     end

     def success? = @success
   end
   ```

## **Use Service Object When:**
A **Service Object** is a single-use class that executes **one specific operation** in a procedural manner. Use a Service Object if:

1. **Performing a Single Business Action** – When logic represents a single-use case (e.g., processing a payment, sending an email, generating a report).
2. **No Need for State** – If the logic does not require instance variables beyond initialization.
3. **Interacting with External APIs or Services** – When dealing with third-party integrations or background jobs.
4. **Encapsulating Database Transactions** – If the logic involves multiple database writes that should be executed in a single operation.
5. **Reducing Controller Fat** – Moving complex logic from controllers to service objects for better readability and reusability.
6. **Best For:** Single-use actions, stateless procedures, database transactions, API interactions.

## Common Anti-Patterns to Avoid
- Creating "god" services that handle multiple unrelated tasks
- Putting view logic in services
- Directly accessing `params` hash in services
- Ignoring transaction boundaries for DB operations
- Never Combine PORO and Service Objects
