---
description: Rails specific rules
globs: app/**/*.rb
alwaysApply: false
---
# Rails-Specific Conventions
RAILS_CONVENTIONS: >
  - Follow REST conventions for controllers
  - Use strong parameters in controllers
  - Place business logic in models or service objects
  - Use concerns for shared functionality
  - Follow Rails directory structure
  - Use partials for reusable view components

# Database Conventions
DATABASE_RULES: >
  - Use plural table names
  - Use timestamps in migrations
  - Include foreign key constraints
  - Add appropriate indexes
  - Use references for associations

# Example Model Structure
MODEL_PATTERN: >
  class User < ApplicationRecord
    # Constants first
    ROLES = %w[admin moderator user].freeze

    # Associations
    belongs_to :organization
    has_many :posts, dependent: :destroy

    # Validations
    validates :name, presence: true
    validates :email, uniqueness: true

    # Scopes
    scope :active, -> { where(status: 'active') }

    # Class methods
    def self.find_by_credentials(credentials)
      find_by(email: credentials[:email])
    end

    # Instance methods
    def full_name
      "#{first_name} #{last_name}"
    end
  end

# API Response Format
API_RESPONSE_FORMAT: >
  {
    status: "success",
    data: {
      id: 1,
      attributes: {
        name: "David",
        email: "david@example.com"
      }
    },
    meta: {
      timestamp: "2024-11-02T12:00:00Z"
    }
  }

# Performance Guidelines
- Use query optimization
- Implement caching where appropriate
- Use background jobs for heavy tasks
- Add database indexes
- Monitor N+1 queries
- Use bulk operations when possible

# Security Guidelines
- Use strong parameters
- Add authorization checks
- Sanitize user inputs
- Protect from mass assignment
- Follow OWASP guidelines

# Code Organization
- Follow Ruby community style guide @.rubocop.yml
- Use service objects for business logic
- Keep controllers skinny, models focused

metadata:
  priority: high
  version: 1.0
