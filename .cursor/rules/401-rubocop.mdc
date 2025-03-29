---
description: Standards for RuboCop configuration and usage
globs: .rubocop.yml
alwaysApply: false
---
# RuboCop Configuration Standards

## Context
- Applied when configuring or modifying RuboCop settings
- Used for maintaining consistent code style across the project
- Referenced when adding new Ruby files or features

## Requirements
- Keep the `.rubocop.yml` file organized by cop categories
- Document non-obvious cop configurations with comments
- Maintain consistency with the Ruby community style guide
- Use inheritance for environment-specific configurations
- Run RuboCop before committing code

## Configuration Guidelines

### Core Structure
- Use plugins section for extensions (rubocop-rails, rubocop-rspec, etc.)
- Group related cops together
- Maintain alphabetical order within groups
- Document custom configurations

### Disabling Cops
- Prefer inline disables for specific instances rather than global disables
- Document why a cop is disabled with a comment
- Regularly review disabled cops for potential re-enabling

### Auto-correction
- Use `--auto-correct-all` for safe corrections
- Review changes after auto-correction
- Run tests after auto-correction

## Examples

<example>
# Good: Well-organized RuboCop configuration
AllCops:
  DisplayCopNames: true
  DisplayStyleGuide: true
  NewCops: enable
  
# Style Cops
Style/Documentation:
  Enabled: false  # We use YARD for documentation

# Metrics Cops
Metrics/MethodLength:
  Max: 15  # Increased from default 10 for complex business logic
</example>

<example type="invalid">
# Bad: Poorly organized RuboCop configuration
Style/Documentation:
  Enabled: false
AllCops:
  DisplayCopNames: true
Metrics/MethodLength:
  Max: 15
</example>

## Integration Guidelines
- Run RuboCop in CI/CD pipeline
- Use RuboCop's caching for faster runs
- Consider using pre-commit hooks for automatic checks
- Integrate with editor/IDE for real-time feedback

metadata:
  priority: high
  version: 1.0
