# Rails AI Rules

A comprehensive collection of rules, patterns, and standards for effectively developing Ruby on Rails applications with AI assistance.

## Overview

This repository provides structured guidelines to ensure consistent and high-quality code production in AI-assisted Rails development.

## Project Structure

The repository is organized into the following directories and files:

- **`docs/architecture.md`**: Details the system design and architectural principles of the project.
- **`docs/patterns/`**: Contains various implementation patterns utilized within the project.
- **`docs/specs/`**: Houses component specifications and standards.
- **`docs/tdd.md`**: Outlines the Test-Driven Development workflow adopted in the project.

## Rule Categories

Rules within this project are numerically categorized as follows:

- **000-099**: Core standards and formats.
- **100-199**: Language and framework-specific rules.
- **200-299**: Frontend and design-related rules.
- **300-399**: Testing standards and best practices.
- **400-499**: Tool configurations and setups.
- **800-899**: Workflows and process guidelines.
- **900-999**: Templates and boilerplate code.


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
