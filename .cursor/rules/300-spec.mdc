---
description: Standards for RSpec configuration and testing practices
globs: spec/**/*.rb
alwaysApply: false
---
# RSpec Testing Standards

## Context
- Applied when writing or modifying tests
- Used for maintaining consistent testing practices
- Referenced when implementing new features
- [spec_helper.rb](mdc:spec/spec_helper.rb) and [rails_helper.rb](mdc:spec/rails_helper.rb) are defined correctly

## Core Conventions
- Use RSpec for testing
- Follow arrange-act-assert pattern
- Use fixtures instead of factories
- Write descriptive test cases
- Test both happy and sad paths
- Ignore spec type while describing RSpec
- NEVER add "require 'rails_helper'" to spec files. We already import it via @.rspec
- NEVER add redundant spec type. RSpecRails/InferredSpecType rule!
- Use the fully qualified namespace path with double colons (::) instead of nesting modules to improve code readability and reduce indentation levels
- Mock external services appropriately

## Testing Guidelines

### Test Organization
- Group related tests with `describe` and `context`
- Use descriptive block names that explain the behavior
- Follow the fully qualified namespace path with double colons (::)
- Keep test files organized to mirror the application structure

### Fixtures
- Use fixtures for test data instead of factories
- Name fixtures descriptively
- Keep fixtures minimal and focused
- Use ERB in fixtures for dynamic data when necessary

### Mocking and Stubbing
- Mock external services to avoid network calls
- Use `allow` for stubbing return values
- Use `expect` for verifying method calls
- Reset mocks after tests with `after` blocks

### Test Performance
- Keep tests fast by minimizing database operations
- Use `before(:all)` for expensive setup operations
- Use `let` for lazy-loaded test data
- Avoid unnecessary database queries

## Examples

<example>
# Good: Well-organized RSpec test
RSpec.describe User do
  # Load specific fixtures
  fixtures :users

  describe "validations" do
    subject(:user) { users(:valid_user) }

    it { should validate_presence_of(:name) }
    it { should validate_uniqueness_of(:email) }
  end

  describe "invalid email" do 
    subject(:invalid_user) { User.new(name: "John Doe", email: "invalid@email") }

    it { is_expected.to_not be_valid }
  end
end

RSpec.describe OrderProcessor do
  fixtures :orders

  let(:order) { orders(:paid_order) }
  
  describe "#process" do
    context "with valid payment" do
      before do
        allow(PaymentGateway).to receive(:charge).and_return(true)
      end
      
      it "updates order status" do
        expect { 
          described_class.new(order).process 
        }.to change(order, :status).to("completed")
      end
    end
  end
end
</example>

<example type="invalid">
# Bad: Poorly organized RSpec test
describe "User" do
  it "validates presence of name" do
    user = User.new
    user.valid?
    expect(user.errors[:name]).to include("can't be blank")
  end
  
  it "validates uniqueness of email" do
    # Missing test implementation
  end
  
  # Missing context blocks
  # No use of fixtures
  # Unclear test organization
end
</example>

## Configuration Guidelines
- Configure RSpec to use fixtures by default
- Set up appropriate formatters for CI/CD
- Configure random test ordering
- Set up appropriate test coverage tools

metadata:
  priority: high
  version: 1.1
