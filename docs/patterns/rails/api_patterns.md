# API Client Pattern in Ruby on Rails

## Overview
This pattern leverages `class_attribute` to define inheritable API configurations for different clients while maintaining a shared base configuration.

## Implementation

### **Step 1: Define the Base API Client**
```ruby
class ApiClient
  class_attribute :headers, default: { "Content-Type" => "application/json" }
end
```
- Sets a default `headers` hash using `class_attribute`.
- Allows subclasses to inherit and modify their own headers.

### **Step 2: Create Specific API Clients**
```ruby
class GitHubClient < ApiClient
  self.headers = headers.merge({ "Accept" => "application/vnd.github.v3+json" })
end

class TwitterClient < ApiClient
  self.headers = headers.merge({ "User-Agent" => "RubyCademy" })
end
```
- Each subclass extends `headers` without modifying the base class.
- `GitHubClient` adds an `Accept` header.
- `TwitterClient` adds a `User-Agent` header.

### **Step 3: Usage & Expected Output**
```ruby
ApiClient.headers
# => { "Content-Type" => "application/json" }

GitHubClient.headers
# => { "Content-Type" => "application/json", "Accept" => "application/vnd.github.v3+json" }

TwitterClient.headers
# => { "Content-Type" => "application/json", "User-Agent" => "RubyBot" }
```
- Each subclass maintains its own version of `headers` while keeping the base default.

## Benefits
✅ **Encapsulation**: Shared configuration in the base class, extended by subclasses.
✅ **Avoids Shared State Issues**: Subclasses maintain independent copies of attributes.
✅ **Reusable & Maintainable**: Easily extend for new API clients without modifying existing ones.

This approach ensures structured API client management while keeping configurations flexible and scalable.
