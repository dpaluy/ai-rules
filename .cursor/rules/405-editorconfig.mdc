---
description: 
globs: 
alwaysApply: true
---
# EditorConfig Compliance Guidelines

## Context
- Applied when generating or modifying any code files
- Used to ensure consistent formatting across the codebase
- Referenced when creating new files or editing existing ones

## Requirements
- All generated code must comply with the project's EditorConfig rules
- Follow specific formatting rules for different file types
- Maintain consistent indentation, line endings, and character encoding
- Respect file-specific exceptions defined in the configuration

## Formatting Guidelines

### General File Formatting
- Use UTF-8 character encoding for all files
- Use 2 spaces for indentation (not tabs) for most files
- Ensure all files end with a newline character
- Use LF (Unix-style) line endings
- Remove trailing whitespace from all lines except in Markdown files

### File-Specific Rules
- For Makefiles: Use tabs for indentation instead of spaces
- For Markdown files: Preserve trailing whitespace where needed for line breaks
- For vendor files: Preserve original formatting without modifications

### Code Generation Practices
- When generating new files, apply the correct formatting automatically
- When suggesting code edits, maintain the project's indentation style
- Ensure all code blocks in documentation follow the same formatting rules
- Add final newlines to all generated files

## Examples

<example>
# Good: Properly formatted Ruby code
class User < ApplicationRecord
  validates :name, presence: true
  
  def full_name
    "#{first_name} #{last_name}"
  end
end
</example>

<example type="invalid">
# Bad: Improperly formatted Ruby code
class User < ApplicationRecord
    validates :name, presence: true
    
    def full_name
        "#{first_name} #{last_name}"
    end
end
</example>

## Implementation Guidelines
- When generating code, automatically apply 2-space indentation
- Always add a final newline to files
- Never use tabs except in Makefiles
- Preserve trailing whitespace in Markdown files for line breaks
- Don't modify the formatting of vendor files

metadata:
  priority: high
  version: 1.0
