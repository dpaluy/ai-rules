# Authorization Specification

## Roles
1. owner
   - Full system access
   - Billing management
   - User management

2. admin
   - Report management
   - User invitation
   - Connection management

3. analyst
   - Report creation/execution
   - View connections

4. viewer
   - View reports
   - Execute existing reports

## Policies
```ruby
# Base policy with tenant isolation
class ApplicationPolicy < ActionPolicy::Base
  authorize :user
  authorize :organization, optional: true

  def owner?
    user.role == "owner"
  end

  private

  def same_organization?
    record.organization_id == user.organization_id
  end
end

# Example policies
class ReportPolicy < ApplicationPolicy
  def manage?
    same_organization? && (owner? || admin?)
  end

  def execute?
    same_organization?
  end
end
```

## Scopes

```ruby
# Active Record scope
module OrganizationScope
  extend ActiveSupport::Concern

  included do
    belongs_to :organization
    default_scope { where(organization: Current.organization) }
  end
end
```

## Tests

1. Role-based access
2. Resource isolation
3. Policy inheritance
4. Scope effectiveness
