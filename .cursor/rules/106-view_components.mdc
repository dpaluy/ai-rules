---
description: ViewComponent Patterns
globs: app/views/components/**/*.{rb,html.erb}
alwaysApply: false
---
# ViewComponent Patterns

## Architecture Overview

Our ViewComponent implementation follows a hierarchical structure organized by domain and complexity. We chose ViewComponents over partials to enhance reusability, testability, and performance.

## Component Categories

1. **Base Components**: Simple, atomic UI elements like buttons, cards, and form inputs. These form the foundation of our component library.

2. **Composite Components**: Combinations of base components that form more complex UI patterns, such as search forms or notification systems.

3. **Domain Components**: Business-specific components that encapsulate domain logic and presentation, like `ProductCard` or `UserProfile`.

## Implementation Strategy

We implement progressive enhancement through a combination of ViewComponents and Stimulus controllers. This ensures basic functionality without JavaScript while enabling enhanced interactivity when available.

## Component Organization

1. **One Component Equals One Visual Element**: Each component should represent a single visual element.

2. **Use Slots for Flexible Content**: Utilize slots to allow for flexible content within components.

3. **Keep Templates Focused on Presentation**: Ensure that templates are solely responsible for presentation logic.

4. **Include Component Previews**: Provide previews for each component to facilitate development and testing.

5. **Test Rendering Scenarios**: Write tests for various rendering scenarios to ensure component reliability.

## Data Fetching and Database Queries

1. **Avoid Database Queries in Components**: Components should never make database queries directly. This violates separation of concerns and can lead to N+1 query problems.

2. **Pass Prepared Data to Components**: All data needed by a component should be passed in during initialization. Controllers or parent views should prepare and pass this data.

3. **Views are for Rendering, Not Fetching**: Components should focus solely on rendering data, not retrieving it. Data retrieval belongs in controllers, services, or query objects.

4. **Use Presenters for Complex Data Transformations**: If data needs significant transformation before display, use a presenter pattern outside the component rather than embedding this logic in the component.

5. **Consider Performance Implications**: Remember that components may be rendered multiple times in a single page. Ensure all data is efficiently pre-loaded to avoid performance bottlenecks.

## Organizing Components

- **Component Location & Structure**: All components are located in `app/view/components`. Each component is organized using a sidecar pattern, meaning each component has a dedicated folder containing the Ruby file (the component class), the HTML template, preview files (if any), and accompanying asset files (CSS, JS, etc.).

- **Sidecar Pattern Benefits**: Keeping all related files (view, logic, preview, styles, and scripts) in one folder simplifies maintenance and encourages better encapsulation.

## Style Variants & Dynamic Styling

- **Using Style Variants**: Components leverage the `ViewComponentContrib::StyleVariants` module to define dynamic styling rules. Within your component class, define a style block that outlines:

  - **Base Styles**: A set of default classes.

  - **Variants**: Groups (e.g., `size`, `color`, `disabled`) that output specific classes based on component properties.

  - **Defaults**: Preset variant values to fall back on if none are provided.

- **Example Usage in a Component Class**:

  ```ruby
  class ButtonComponent < ViewComponent::Base
    include ViewComponentContrib::StyleVariants

    style do
      base { %w[font-medium bg-blue-500 text-white rounded-full] }
      variants do
        color { primary { %w[bg-blue-500 text-white] } secondary { %w[bg-purple-500 text-white] } }
        size  { sm { "text-sm" } md { "text-base" } lg { "px-4 py-3 text-lg" } }
        disabled { yes { "opacity-75" } }
      end
      defaults { { size: :md, color: :primary } }
    end

    def initialize(size: nil, color: nil, disabled: false)
      @size = size
      @color = color
      @disabled = disabled
    end
  end
  ```

  In the corresponding template, invoke the helper:

  ```erb
  <button class="<%= style(size: @size, color: @color, disabled: @disabled) %>">Click me</button>
  ```

## Stimulus Integration

- **Component Controllers**: Each component can include a `controller.js` file inside its folder to define a Stimulus controller, allowing for per-component interactivity.

- **Helper for Controller Naming**: Your base component (e.g., `ApplicationViewComponent`) should provide a helper to generate the Stimulus controller identifier. For instance:

  ```ruby
  class ApplicationViewComponent < ViewComponent::Base
    private

    def identifier
      @identifier ||= self.class.name.sub("::Component", "").underscore.split("/").join("--")
    end

    alias_method :controller_name, :identifier
  end
  ```

  In your HTML template, assign the data attribute:

  ```erb
  <div data-controller="<%= controller_name %>">
    <!-- Component markup -->
  </div>
  ```

- **Turbo Integration**: With Turbo in your stack, components can be wrapped in Turbo Frames or Streams for enhanced partial page updates. Ensure that any dynamic behavior handled by Stimulus complements Turbo’s automatic updates. For example:

  ```erb
  <turbo-frame id="<%= controller_name %>">
    <div data-controller="<%= controller_name %>">
      <!-- Component markup -->
    </div>
  </turbo-frame>
  ```

## Testing & Dry Integration

- **RSpec Testing**: Continue writing component tests with RSpec. Test both the rendered HTML output and any interactive behavior (such as dynamic class changes from style variants) to ensure your component works as expected.

- **Using Dry for Data Validation**: If your components rely on complex data or validation, leverage Dry libraries (e.g., `Dry::Struct`, `Dry::Monads`) to enforce types and validations within your component initialization. This approach helps separate concerns between data validation and view rendering.

## Performance Considerations

Components are designed to be lightweight and cacheable. We use Russian Doll caching for nested components and implement custom cache keys for dynamic content.

## Migration Strategy

When converting existing views to components:

1. **Identify Reusable Patterns**: Look for patterns in your views that can be abstracted into components.

2. **Extract into Components**: Create components for these patterns.

3. **Replace Old Views Gradually**: Integrate the new components into your views incrementally.

4. **Maintain Backward Compatibility**: Ensure that existing functionality remains intact during the migration process.

## Final Considerations

- **Asset Organization**: Although your components reside in `app/view/components`, asset files (like CSS and JS) should be placed alongside each component. Ensure your build process (Vite or Webpack) is configured to load these files automatically.

- **Refinement & Customization**: As your project evolves, continue to refine the generator and helper methods to meet specific project needs. Tailor the sidecar pattern to integrate smoothly with your overall Rails, Stimulus, and Turbo setup.

For more detailed information, refer to the @ViewComponent documentation.

metadata:
  priority: high
  version: 1.0
