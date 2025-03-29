# Rails AI Rules: A Template for AI-Assisted Development

A comprehensive collection of rules, patterns, and standards designed to guide AI assistants in developing high-quality Ruby on Rails applications effectively.

## Overview

This repository provides structured guidelines, best practices, and standard procedures to ensure consistent, maintainable, and robust code production when leveraging AI tools like Cursor and Cline for Rails development. It serves as a template and reference for teams aiming to standardize their AI-assisted workflows.

## How Rules are Organized

This project distinguishes between different types of rules and documentation:

1.  **Generic Documentation (`docs/`)**:
    *   Contains foundational knowledge, architectural decisions, patterns, specifications, and workflows applicable to the project regardless of the specific AI tool being used.
    *   Files like `docs/architecture.md`, `docs/patterns/`, `docs/specs/`, `docs/tdd.md`, and `docs/erd.mmd` provide essential context for both human developers and AI assistants.
    *   AI tools should be configured to reference these documents for background information and project standards.

2.  **Cursor-Specific Rules (`.cursorrules`, `.cursor/rules/*.mdc`)**:
    *   These files are formatted specifically for use with the Cursor IDE.
    *   They might contain rules leveraging Cursor's specific features or syntax (like `.mdc` files).
    *   Refer to Cursor's documentation for how to integrate these rules effectively. The `.cursorrules` file is generally deprecated in favor of the `.cursor/rules/` directory structure.

3.  **Cline-Specific Rules (`.clinerules`)**:
    *   This file contains rules formatted for use with the Cline tool.
    *   It defines project-specific instructions, preferences, and constraints directly consumable by Cline.

## Integrating Rules with AI Tools

-   **Cursor:** Place `.mdc` rule files within the `.cursor/rules/` directory in your project root. Cursor will automatically pick them up.
-   **Cline:** Ensure the `.clinerules` file is present in the project root. Cline uses this file for its configuration.
-   **Generic Docs:** Both tools can be instructed (often within their specific rule files or prompts) to consult the `docs/` directory for broader context, patterns, and architectural guidelines.

## Project Structure Overview

-   **`README.md`**: This file - provides an overview and explains rule organization.
-   **`.clinerules`**: Rules specifically for the Cline AI tool.
-   **`.cursorrules` / `.cursor/rules/`**: Rules specifically for the Cursor IDE (prefer `.cursor/rules/*.mdc`).
-   **`docs/`**: Generic documentation (architecture, patterns, specs, TDD, ERD, decisions). Essential context for any AI or developer.
-   **`LICENSE`**: Project license information.
-   **`CONTRIBUTING.md`**: (Optional) Guidelines for contributing to this ruleset.

## Key Concepts & Technologies

This ruleset assumes a modern Rails development stack. Key technologies and concepts are detailed within `docs/architecture.md` and relevant pattern/spec files. Examples include:

-   Ruby on Rails (Version specified in `docs/architecture.md`)
-   Hotwire (Turbo & Stimulus)
-   ViewComponents
-   TailwindCSS
-   RSpec
-   Service Objects
-   Background Job Framework (Specified in `docs/architecture.md`)

## Getting Started with This Template

1.  **Clone/Fork:** Start with this repository as your base.
2.  **Customize `docs/`:** Update generic documentation (`architecture.md`, `erd.mmd`, patterns, specs) to match your project.
3.  **Configure AI Rules:**
    *   Populate/modify `.cursor/rules/` with `.mdc` files for Cursor.
    *   Populate/modify `.clinerules` for Cline.
    *   Ensure AI rule files reference the `docs/` for context where needed.
4.  **Integrate:** Set up your AI tools to use the configured rules.
5.  **Communicate:** Ensure your team understands the structure and how to use/maintain the rules and documentation.

## License

This project template is available as open source under the terms of the [MIT License](LICENSE).
