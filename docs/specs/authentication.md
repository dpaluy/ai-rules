# Authentication Specification

## Models

- Organization
- User (Devise)
  - Added fields: organization_id, role

## Configuration

```ruby
# config/initializers/devise.rb
config.authentication_keys = [:email]
config.timeout_in = 2.hours
config.remember_for = 2.hours
config.password_length = 12..128
```

## Flows

### Registration

- Organization creation
- Admin user creation
- Welcome email
- Email verification required

### User Invitation

- Admin invites via email
- User sets password
- Auto-assigns to organization

### Password Management

- Reset via email
- Change password
- Force reset on suspicious activity

### Security

- Rate limiting: 5 attempts/15 minutes
- Session timeout: 2 hours
- Remember me: 2 weeks
- Secure password requirements
- Prevent password reuse (last 3)

### Tests

- Organization Registration
- User Authentication
- Password Reset
- Account Recovery
- Session Management
