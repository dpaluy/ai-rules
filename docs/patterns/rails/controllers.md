# Rails Controllers Examples

## Implementing params `expect` in Rails 8 Controllers

This approach ensures safer, more explicit parameter validation in your Rails application.
This method enforces the expected structure of request parameters, raising an ActionController::ParameterMissing error with a 400 Bad Request if the input is malformed or missing, improving robustness over 500 errors from older methods.

### Steps to Implement:
Example:

```ruby
class PeopleController < ApplicationController
  def create
    person = create(person_params)
  end

  private

  def person_params
    params.expect(person: [:name, :age, pets: [[:name]]]).with_defaults(organization_id: current_organization.id)
  end
end
```

### Best Practices:

- Use params#expect for all non-optional parameters to enforce structure.
- Update tests to handle ActionController::ParameterMissing exceptions.
