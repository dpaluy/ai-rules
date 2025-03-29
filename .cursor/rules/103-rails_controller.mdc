---
description: Rules for Rails Controllers and Objects
globs: app/controllers/**/*.rb
---
rules:
  - name: Value Object Rule
    condition: |
      Model attributes have associated business logic beyond simple getters/setters
    action: |
      - Extract domain-specific value objects (e.g. PhoneNumber, Money)
      - Implement #hash and #eql? for hash key usage
      - Add comparison methods (#better_than?) instead of relying on operators

  - name: Service Object Rule
    condition: |
      Performing actions that:
      - Involve multiple models
      - Interact with external services
      - Represent alternative strategies
    action: |
      - Create single-purpose Action/Service classes
      - Keep controllers thin by moving business logic here
      - Use dependency injection for variations

  - name: Form Object Rule
    condition: |
      Handling multi-model form submissions
    action: |
      - Replace accepts_nested_attributes_for with Form Object
      - Use Virtus for ActiveRecord-like attributes
      - Consolidate validation context

  - name: Query Object Rule
    condition: |
      Complex SQL in scopes/class methods
    action: |
      - Extract to *Query classes accepting Relation
      - Chain queries via composition
      - Test with real DB records

  - name: View Object Rule
    condition: |
      Logic exists solely for presentation
    action: |
      - Extract to *View classes with template-specific formatting
      - Maintain 1:1 relationship with templates
      - Avoid "Presenter" terminology conflicts

  - name: Policy Object Rule
    condition: |
      Complex read operations/business rules
    action: |
      - Extract to *Policy classes for authorization/eligibility
      - Separate from Query Objects (memory vs DB operations)
      - Return boolean decisions

  - name: Decorator Rule
    condition: |
      Adding conditional callback responsibilities
    action: |
      - Wrap core objects with Decorator pattern
      - Maintain original interface
      - Use Ruby's SimpleDelegator

  - Implementing params `expect` in Rails 8 Controllers
    [controllers.md](mdc:docs/patterns/rails/controllers.md)


anti_patterns:
  - Never extract model mixins to concerns/
  - Prefer composition over inheritance
  - Keep AR models focused on persistence

testing_guidelines:
  - Test Query Objects with real DB records
  - Verify View Objects through template rendering
  - Validate Form Objects through controller specs
  - Keep model specs focused on persistence layer

general_principles:
  - Emphasize Single Responsibility Principle through Plain Old Ruby Objects
  - Maintain Rails conventions
  - Prevent callback hell
  - Keep models under 100 lines of code
  - Implement patterns based on specific domain pain points



metadata:
  priority: high
  version: 1.0  
    