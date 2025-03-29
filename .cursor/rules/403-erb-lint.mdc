---
description: Standards for ERB Lint configuration and usage
globs: .erb_lint.yml
alwaysApply: false
---
# ERB Lint Configuration Standards

## Context
- Applied when configuring or modifying ERB Lint settings
- Used for maintaining consistent ERB template style
- Referenced when adding new templates or view components

## Requirements
- Maintain a well-organized `.erb_lint.yml` file
- Enable appropriate linters for the project
- Configure RuboCop integration properly
- Document custom configurations
- Run ERB Lint before committing code

## Configuration Guidelines

### Core Structure
- Enable default linters unless explicitly disabled
- Configure RuboCop integration with appropriate cop exclusions
- Exclude vendor and node_modules directories
- Document reasons for disabling specific linters

### Custom Linters
- Place custom linters in `lib/erb_lint/linters/`
- Document custom linter behavior
- Write tests for custom linters
- Register custom linters in the configuration

### Integration with ViewComponents
- Apply consistent linting rules to ViewComponent templates
- Configure appropriate exclusions for ViewComponent-specific patterns
- Ensure compatibility with ViewComponent rendering

## Examples

<example>
# Good: Well-organized ERB Lint configuration
---
EnableDefaultLinters: true
exclude:
  - "node_modules/**/*"
  - "vendor/**/*"
linters:
  ErbSafety:
    enabled: true
  FinalNewline:
    enabled: true
  Rubocop:
    enabled: true
    rubocop_config:
      inherit_from:
        - .rubocop.yml
      Layout/LineLength:
        Enabled: false
      Rails/OutputSafety:
        Enabled: false
</example>

<example type="invalid">
# Bad: Poorly organized ERB Lint configuration
---
EnableDefaultLinters: false # Disables all default linters
linters:
  Rubocop:
    enabled: true
    # Missing rubocop_config section
</example>

## Integration Guidelines
- Run ERB Lint in CI/CD pipeline
- Integrate with editor/IDE for real-time feedback
- Use with pre-commit hooks for automatic checks
- Run alongside RuboCop for comprehensive linting

metadata:
  priority: high
  version: 1.0
