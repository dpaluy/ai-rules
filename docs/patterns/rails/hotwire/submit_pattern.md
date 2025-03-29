# Hotwire Stimulus Submit Pattern

## Overview
This pattern utilizes Hotwire's Turbo Streams and Stimulus to create dynamic, interactive forms that update specific DOM elements (e.g., dropdown menus) without full page reloads. Ideal for real-time interactions, such as dynamically updating city options based on the selected country, this pattern involves Stimulus controllers for JavaScript event handling, programmatic form submissions, and Turbo Streams for server-driven DOM updates.

## Context
- **When to Use:**
  - Responsive, single-page-app-like behaviors in web apps (e.g., cascading dropdowns).
- **Problem:**
  - Traditional submissions reload the entire page, causing poor user experience.
- **Solution:**
  - Use Stimulus for minimal JavaScript interaction and Turbo Streams for efficient DOM updates driven by server-side actions.

## Forces

### Benefits
- Enhanced user experience (fewer reloads).
- Simplified JavaScript via Stimulus's declarative model.
- Leverages server-side rendering, simplifying logic.

### Trade-offs
- Requires server-side Turbo Stream integration.
- Adds complexity to very basic forms.
- Dependency on Hotwire libraries.

## Structure

### Components
- **HTML Form:** Contains Stimulus attributes (`data-controller`, `data-action`, `data-target`).
- **Stimulus Controller:** Handles JavaScript-driven form submissions and DOM updates.
- **Server-Side Controller:** Processes submissions, fetches data, and returns Turbo Stream responses.
- **Turbo Stream Template:** DOM update instructions.
- **Routing:** Links form submissions to server-side actions.

### Relationships
- Stimulus interacts with HTML through `data-target` and triggers submissions.
- Server-side responses update DOM via Turbo Streams.

## Implementation

### 1. HTML Form Setup
```html
<form data-controller="form-submitter">
  <div>
    <label for="country_id">Country:</label>
    <select id="country_id" name="country_id" data-form-submitter-target="country" data-action="change->form-submitter#requestSubmit">
      <option value="">Select a country</option>
      <!-- Options dynamically or server-side rendered -->
    </select>
  </div>

  <div>
    <label for="city_id">City:</label>
    <select id="city_id" name="city_id" data-form-submitter-target="city">
      <option value="">Select a city</option>
      <!-- Dynamically updated via Turbo Stream -->
    </select>
  </div>
</form>
```
- `data-controller`: Stimulus connection
- `data-target`: Identifies elements for Stimulus
- `data-action`: Binds Stimulus actions

### 2. Stimulus Controller
```javascript
// app/javascript/controllers/form_submitter_controller.js
import { Controller } from "@hotwired/stimulus"

export default class extends Controller {
  static targets = ["country", "city"]

  submit({ params }) {
    params.submitter ?
      this.element.requestSubmit(this.#get(params.submitter)) :
      this.element.requestSubmit()
  }

  cancel() {
    this.cancelTarget?.click()
  }

  preventAttachment(event) {
    event.preventDefault()
  }

  #get(id) {
    return document.getElementById(id) || this.#notFound(id)
  }

  #notFound(id) {
    throw new Error(`Element with ID "${id}" not found`)
  }
}
```
- Targets DOM elements and handles submissions.

### 3. Server-Side Controller
```ruby
# app/controllers/your_controller.rb
class YourController < ApplicationController
  def update_cities
    @cities = City.where(country_id: params[:country_id])
    respond_to do |format|
      format.turbo_stream do
        render turbo_stream: turbo_stream.replace(
          "city_select",
          partial: "cities/select",
          locals: { cities: @cities }
        )
      end
      format.html { redirect_to your_path }
    end
  end
end
```
- Returns updated DOM via Turbo Stream.

### 4. Turbo Stream Template
```erb
<!-- app/views/your/_select.turbo_stream.erb -->
<%= turbo_stream.replace "city_select" do %>
  <select id="city_id" name="city_id" data-form-submitter-target="city">
    <option value="">Select a city</option>
    <% cities.each do |city| %>
      <option value="<%= city.id %>"><%= city.name %></option>
    <% end %>
  </select>
<% end %>
```
- Provides DOM replacement with updated data.

### 5. Routing
```ruby
# config/routes.rb
Rails.application.routes.draw do
  resources :your_resource, only: [] do
    post :update_cities, on: :collection
  end
end
```

### 6. Test and Validate
- Confirm dynamic updates and responsiveness.

## Example
- Selecting "USA" dynamically updates city options without reloading the page.
