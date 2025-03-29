---
description: Standards for Prettier configuration and usage
globs: .prettierrc.cjs
alwaysApply: false
---
# Prettier Configuration Standards

## Context
- Applied when configuring or modifying Prettier settings
- Used for maintaining consistent JavaScript/CSS formatting
- Referenced when adding new frontend code

## Requirements
- Maintain a well-organized `.prettierrc.cjs` file
- Configure consistent formatting rules
- Ensure compatibility with other linters
- Document custom configurations
- Run Prettier before committing code

## Configuration Guidelines

### Core Structure
- Use `.prettierrc.cjs` for configuration
- Keep configuration minimal and focused
- Document non-default settings
- Ensure consistency with EditorConfig

### Key Settings
- Set `tabWidth: 2` for consistency
- Use `useTabs: false` to use spaces
- Set `printWidth` appropriately for the project
- Configure `semi`, `singleQuote`, and `trailingComma` consistently

### Integration with Other Tools
- Ensure compatibility with ESLint
- Configure to work with Tailwind CSS
- Integrate with TypeScript formatting
- Coordinate with EditorConfig settings

## Examples

<example>
// Good: Well-organized Prettier configuration
// .prettierrc.cjs
/** @type {import("prettier").Config} */

module.exports = {
  tabWidth: 2,
  useTabs: false,
  printWidth: 100,
  semi: true,
  singleQuote: true,
  trailingComma: 'es5',
  bracketSpacing: true,
  arrowParens: 'avoid',
};
</example>

<example type="invalid">
// Bad: Poorly organized Prettier configuration
// .prettierrc.cjs
module.exports = {
  tabWidth: 4, // Inconsistent with EditorConfig
  printWidth: 200, // Too wide
};
</example>

## Integration Guidelines
- Run Prettier in CI/CD pipeline
- Use with pre-commit hooks for automatic formatting
- Integrate with editor/IDE for real-time formatting
- Configure to ignore specific files or directories

metadata:
  priority: high
  version: 1.0
