---
description: Generic ruby rules
globs: *.rb
alwaysApply: false
---
## General Ruby Styling
PREFER_RUBY_SYNTAX: >
  - Use Ruby 3.x syntax
  - Use snake_case for methods and variables
  - Use CamelCase for classes and modules
  - Use SCREAMING_SNAKE_CASE for constants
  - Prefer string interpolation over concatenation
  - Use modern hash syntax: { key: value }
  - When a local variable matches the exact name of a parameter in a method call, use the shorthand syntax by providing just the parameter name with a colon instead of explicitly mapping the variable
  - Use double quotes only when interpolation is needed

## Code Examples for Syntax Reference
Use the shorthand syntax when hash keys match local variable names.
Note: It requires exact matching between symbol key and variable name

EXAMPLE_PATTERNS: >
  # Hash syntax
  age = 49
  user = { name: "David", age: }

## Rules for Developers (by Sandi Metz)

rules:
  - name: class_length
    description: Classes should not exceed 100 lines of code
    example: |
      class UserProfile
        # Keep core logic under 100 lines
        # Extract secondary concerns to new classes
      end
    check:
      - "count_lines > 100"
      - "split_file? when spec exceeds limit"
    exceptions: "Valid SRP justification required"

  - name: method_length
    description: Methods must be 5 lines or fewer
    example: |
      def validate_user
        return if anonymous?
        check_email_format
        check_age_restriction
      end
    check:
      - "count_lines > 5"
      - "if/else branches limited to 1 line each"
    exceptions: "Pair approval via Rule 0"

  - name: method_parameters
    description: Maximum 4 parameters per method
    example: |
      def create_post(user, title, content, category)
        # Hash options count as parameters
      end
    check:
      - "parameters.count > 4"
      - "view helpers exempt via Rule 0"
    exceptions: "Rails view helpers (link_to/form_for)"

  - name: controller_instantiation 
    description: Controllers may only instantiate one object
    example: |
      def show
        @dashboard = DashboardFacade.new(current_user)
      end
    check:
      - "multiple instance variables in views"
      - "direct collaborator access (@obj.collaborator.value)"
    implementation:
      - "Use facade pattern"
      - "Prefix unused vars with _ (@_calculation)"

metadata:
  priority: high
  version: 1.0
  