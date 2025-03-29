---
description: Stimulus Controller Standards
globs: app/frontend/controllers/**/*.js
alwaysApply: false
---
## Controller Guidelines
- Keep controllers focused and small
- Use data-controller pattern
- Follow single responsibility principle
- Document public methods
- Test complex behaviors
- Don't add explicit controller to index.js 
  It is added automatically: `const controllers = import.meta.glob("./**/*_controller.js", { eager: true });`

## Implementation Patterns
1. Data attributes for configuration
2. Clear target definitions
3. Explicit action mapping
4. Error handling

Example:
```javascript
// app/javascript/controllers/dropdown_controller.js
import { Controller } from "@hotwired/stimulus"

/**
 * Dropdown controller handles toggle menu behavior
 * @example
 * <div data-controller="dropdown">
 *   <button data-action="dropdown#toggle">Toggle</button>
 *   <div data-dropdown-target="menu">Content</div>
 * </div>
 */
export default class extends Controller {
  static targets = ["menu"]
  
  toggle() {
    this.menuTarget.classList.toggle("hidden")
  }
}

## Resources

- [Stimulus Handbook](mdc:https:/stimulus.hotwired.dev/handbook/introduction)

metadata:
  priority: high
  version: 1.0
