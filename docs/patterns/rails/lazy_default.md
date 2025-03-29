# Lazy Default Initialization Pattern in ActiveRecord

## Overview
The **Lazy Default Initialization** pattern ensures that associated records are initialized with default values **only when accessed**. This prevents unnecessary database writes while maintaining data integrity.

## Implementation

### **Step 1: Define the Association**
```ruby
class Invoice < ApplicationRecord
  has_many :payment_reminders, -> { order_by_id },
           class_name: "Invoice::PaymentReminder",
           inverse_of: :invoice,
           dependent: :destroy do
    def with_defaults_if_none
      load_target

      if target.empty?
        Invoice::PaymentReminder::DEFAULTS.each do |attributes|
          build(attributes)
        end
      end

      target
    end
  end
end
```

### **Step 2: Define Default Values**
```ruby
class Invoice::PaymentReminder < ApplicationRecord
  belongs_to :invoice

  DEFAULTS = [
    { reminder_type: "email", days_before_due: 7 },
    { reminder_type: "sms", days_before_due: 3 }
  ].freeze
end
```

### **Step 3: Use the Pattern**
```ruby
invoice = Invoice.find(1)

# Returns existing payment reminders or an empty array
invoice.payment_reminders

# Ensures reminders exist, initializing defaults if none are present
invoice.payment_reminders.with_defaults_if_none
```

## Key Benefits
- **Lazy Initialization**: Defaults are only created when accessed, reducing unnecessary DB writes.
- **Prevents Orphaned Data**: Associated records are destroyed when the parent is deleted.
- **Uses `build` Instead of `create`**: Ensures objects exist in memory but are not persisted until needed.
- **Efficient Association Loading**: `load_target` ensures association is loaded only once per call.

## Considerations
- If default values should **always** be present, consider using a `before_save` callback instead.
- If defaults should be **persisted immediately**, replace `build` with `create!`.
- Be mindful of **concurrent access** scenarios where multiple threads may attempt to initialize defaults simultaneously.

## Alternative Approaches
- **Memoization (`@reminders ||= …`)** for caching results in memory.
- **`before_create` Callbacks** if default records should always be persisted upfront.

## Example: Extending for Multi-Tenant Systems
For multi-tenant systems, ensure that default records include the correct tenant ID:
```ruby
def with_defaults_if_none
  load_target

  if target.empty?
    Invoice::PaymentReminder::DEFAULTS.each do |attributes|
      build(attributes.merge(tenant_id: invoice.tenant_id))
    end
  end

  target
end
```
