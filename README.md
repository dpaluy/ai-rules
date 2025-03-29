# Rails AI Rules

A comprehensive collection of rules, patterns, and standards for developing Ruby on Rails applications using AI assistance effectively.

## Overview

This project provides a structured set of rules and guidelines for AI-assisted Rails development, ensuring consistent, high-quality code production across projects.

## Project Structure

## Core Components

### Rule Categories

- **000-099**: Core standards and formats
- **100-199**: Language and framework rules
- **200-299**: Frontend and design rules
- **300-399**: Testing standards
- **400-499**: Tool configurations
- **800-899**: Workflows
- **900-999**: Templates

### Documentation

- **Architecture**: System design and principles in `docs/architecture.md`
- **Patterns**: Implementation patterns in `docs/patterns/`
- **Specifications**: Component specs in `docs/specs/`

## Key Features

- Test-Driven Development (TDD) workflow
- Rails 8+ best practices
- ViewComponent patterns
- Hotwire (Turbo + Stimulus) implementation
- Modern frontend architecture
- Comprehensive testing strategy
- Security-first approach

## Implementation Patterns

### Ruby/Rails Patterns
- Service Objects
- Form Objects
- Query Objects
- View Objects
- Policy Objects
- Plain Old Ruby Objects (POROs)

### Frontend Patterns
- ViewComponents
- Stimulus Controllers
- Turbo Frames
- TailwindCSS Architecture

## Getting Started

1. Clone this repository
2. Review the architecture documentation
3. Follow TDD workflow in `docs/tdd.md`
4. Use patterns from `docs/patterns/`
5. Implement specs from `docs/specs/`

## Best Practices

### Code Organization
- Follow Ruby community style guide
- Use service objects for business logic
- Keep controllers skinny
- Implement ViewComponents for UI

### Testing
- Write tests first (TDD)
- Use RSpec fixtures
- Mock external services
- Test both happy and sad paths

### Documentation
- Add YARD documentation
- Include JSDoc for Stimulus
- Keep docs up-to-date
- Document API endpoints

## Contributing

1. Fork the repository
2. Create a feature branch
3. Follow TDD workflow
4. Submit a pull request

## License

This project is available as open source under the terms of the [MIT License](LICENSE).
