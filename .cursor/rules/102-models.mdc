---
description: ActiveRecord Model Standards
globs: app/models/**/*.rb
alwaysApply: false
---
- One model = one responsibility
- Use scopes for common queries
- Validate at model level
- Add indexes for frequently queried fields
- Use enum for state machines
- Extract POROs for complex calculations

Example:
```ruby
class Order < ApplicationRecord
  include Trackable
  
  enum status: { pending: 0, processing: 1, completed: 2 }
  
  belongs_to :user
  has_many :line_items
  
  scope :recent, -> { where(created_at: 1.week.ago..) }
  
  validates :total, numericality: { greater_than: 0 }
  
  def calculate_tax
    TaxCalculator.new(self).compute
  end
end
```

metadata:
  priority: high
  version: 1.0
