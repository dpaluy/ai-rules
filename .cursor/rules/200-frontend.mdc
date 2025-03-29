---
description: Frontend Guidelines
globs: *.erb,*.js,*.css
alwaysApply: false
---
## Framework & Technologies
- TailwindCSS v4 for core styling
- Flowbite 2.5.2 for UI components
- Vite Ruby for build tooling
- Inter Variable font

## File Structure

app/frontend
├── components/                   # Reusable frontend components (JS or ViewComponents)
│   ├── dropdown/                 # Example: Dropdown component
│   │   ├── dropdown.js           # Dropdown component logic (if JS-based)
│   │   └── dropdown.html.erb     # Dropdown component template (if ViewComponent-based)
│   └── *                         # other components
├── controllers/
│   ├── application.js            # Stimulus setup for debug mode
│   ├── index.js                  # Registers all Stimulus controllers & imports Flowbite
│   └── sidebar_controller.js     # Sidebar toggling & submenu expansions
├── entrypoints/
│   └── application.js            # Main JS entry: imports controllers, Turbo, CSS
├── images/                       # Image assets
│   └── svg/                      # SVG icons
└── stylesheets/
│   ├── application.tailwind.css  # Tailwind imports & custom theme variables
└── utils/                        # Utility JavaScript functions
    └── helpers.js                # Example: Helper functions

## CSS Organization

**Entry Points:**
1. **`app/frontend/entrypoints/application.js`**  
   - Imports `application.tailwind.css` and any other CSS dependencies
   - Imports Stimulus controllers and Turbo
2. **`app/frontend/stylesheets/application.tailwind.css`**  
   - Tailwind configuration
   - Custom theme variables
   - Plugins like `@tailwindcss/forms` and `@tailwindcss/typography`

## Component & Stimulus Architecture

- **Stimulus Controllers** are kept in `app/frontend/controllers/`. Each handles a focused UI behavior:
  - **`dropdown_controller.js`** manages dropdown transitions and toggling  
  - **`sidebar_controller.js`** handles collapsible navigation sidebar logic  
  - **`form_validation_controller.js`** enables/disables form submit buttons based on field validity  

- **Flowbite** components are utilized for layout elements like dropdowns and modals.  
- **Tailwind** handles utility classes, spacing, typography, color, and responsiveness.

## Design Principles

1. **Clean Aesthetic**  
   Strive for a professional B2B SaaS feel. Minimal extraneous elements.
2. **Responsive & Adaptive**  
   All interfaces must look great on mobile, tablet, and desktop.
3. **Accessibility**  
   Ensure ARIA attributes, semantic HTML, and color contrast compliance.
4. **Immediate Feedback**  
   Use transitions (e.g. `transform`, `opacity`, `scale`) to signal state changes.
5. **Consistent Layout**  
   Reuse shared partials and Stimulus controllers to maintain uniform patterns.

## Best Practices

1. **Use Tailwind Utility Classes**  
   Avoid duplicating styles in custom CSS. Tailwind utility classes speed up styling and remain consistent.
2. **Keep Components Modular**  
   Each Stimulus controller or partial should focus on a single behavior or UI concern.
3. **Mobile-First Approach**  
   Build layouts starting with small screens, then scale up using Tailwind’s responsive breakpoints.
4. **Color & Spacing Tokens**  
   Reference `--color-*` and `--size-*` CSS variables whenever possible for consistent theming.
5. **Performance Optimizations**  
   Leverage code splitting in Vite, keep images compressed, and lazy-load large assets.
6. **Accessibility**  
   Provide descriptive `aria-label`s and use semantic HTML elements for screen readers.
7. **Flowbite Integration**  
   Use Flowbite UI patterns (e.g., dropdowns, modals) but override with Tailwind if needed for brand consistency.
8. "Beautify" frontend components when no strict design rules are defined.
9. Prefer double-quoted strings unless you need single quotes to avoid extra backslashes for escaping.
10. All hardcoded text should be moved to the en.yml localization file.

## References

- [TailwindCSS Documentation](mdc:https:/tailwindcss.com/docs/installation)
- [Flowbite Documentation](mdc:https:/flowbite.com/docs/getting-started/introduction)
- @Stimulus Handbook

metadata:
  priority: high
  version: 1.0
  