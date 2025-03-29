# Project Rules

Use file specific rules as defined in @.cursor/rules/*.mdc

## Code Style
- Ruby: Follow Rails style guide
- JavaScript: Use ES6+ features
- CSS: Use TailwindCSS utility classes
- Documentation: Follow standardized formats

## Testing Standards (RSpec)
- **Framework**: Use RSpec for all tests (unit, integration, system).
- **Test Data**: Use Rails fixtures (located in `spec/fixtures/`) for test data setup, not FactoryBot. Keep fixtures minimal and focused. **Important:** Reuse existing fixture records whenever possible. Only add new, uniquely named entries to fixture files if specific data variations are required for a test; do not overwrite existing fixture files.
- **Structure**:
    - Use descriptive `describe` and `context` blocks.
    - Follow the arrange-act-assert pattern.
    - Use fully qualified namespace paths (`::`) instead of nesting modules.
- **Assertions**: Test both happy and sad paths.
- **Setup**:
    - Do not explicitly `require "rails_helper"` in spec files (it's handled by `.rspec`).
    - Do not use redundant spec type inference (handled by RSpecRails/InferredSpecType).
- **Mocking**: Mock external services appropriately using `allow` and `expect`.
- **Performance**: Minimize database operations; use `let` for lazy loading.

## Project Patterns
- Database adapters use adapter pattern
- Reports use factory pattern
- Notifications use observer pattern
- Delivery mechanisms use strategy pattern
- Security follows Zero Trust model
- Error handling uses categorized approach

## Implementation Paths
- Database connections: app/adapters/
- Report management: app/models/report.rb
- Delivery mechanisms: app/models/report_destination.rb
- Security: app/policies/
- Background jobs: app/jobs/
- Services: app/services/

## User Preferences
- Prioritize security and reliability
- Focus on intuitive UX for non-technical users
- Maintain clear documentation
- Ensure comprehensive test coverage
- Provide detailed error messages
- Support team collaboration

## Known Challenges
- Database connection reliability
- Query performance at scale
- Security implementation
- Multi-tenant data isolation
- Resource controls (memory, CPU, storage)
- Data consistency requirements

## Workflow Rules
- Following standardized documentation formats
- Implementing user story standards
- Following architecture documentation standards
- Using PRD template for product requirements
- Using story template for user stories

## Documentation Standards
- PRD: Product Requirements Document standards
- Architecture: Architecture documentation standards
- User Stories: User story standards
- Agile Workflow: TDD workflow

## Story Format
```
**As a** [role]
**I want** [capability]
**So that** [benefit]

**Status:** [Complete/In Progress/Not Started]

**Context:**
- [Background information]
- [Business value]
- [Technical considerations]

**Tasks:**
1. - [ ] [Task 1]
   1. - [ ] [Subtask 1.1]
   2. - [ ] [Subtask 1.2]
2. - [ ] [Task 2]
3. - [ ] [Task 3]
```
