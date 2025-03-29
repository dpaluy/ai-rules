---
description: Turbo Frame Standards
globs: app/views/**/*.html.erb
alwaysApply: false
---
## Turbo Features
- Turbo Drive for navigation
- Turbo Frames for partial page updates
- Turbo Streams for real-time updates

## Best Practices
- Use semantic frame IDs
- Keep frame content focused
- Handle loading states
- Consider mobile experience

## Frame Organization
1. Clear naming conventions
2. Proper nesting structure
3. Loading state handling
4. Mobile-first approach
   
Example:

<%# app/views/products/index.html.erb %>
<%= turbo_frame_tag "products-list" do %>
  <div class="space-y-4">
    <%= render ProductList::Component.new(products: @products) %>
  </div>
  
  <div data-controller="infinite-scroll">
    <%= turbo_frame_tag "products-pagination" do %>
      <%= render "pagination", pagy: @pagy %>
    <% end %>
  </div>
<% end %>

## Implement Lazy-Loading Turbo Frames

Load UI components on-demand using Turbo Frames to improve initial page load performance.

### Core Implementation
1. Replace eager-loaded components with lazy Turbo frames
2. Define frame source endpoint for component content
3. Render component content within matching frame tag

### Code Pattern

Main template:

```ruby
turbo_frame_tag "component_#{id}", loading: :lazy, src: endpoint_path

turbo_frame_tag "component_#{@id}" do
  # Component content
end
```

metadata:
  priority: high
  version: 1.0
