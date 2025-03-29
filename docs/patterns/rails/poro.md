# Implementing the PORO Pattern in Ruby

## Introduction
This guide provides detailed instructions on how to implement the **Plain Old Ruby Object (PORO) pattern** in a Ruby on Rails application. This pattern is useful for encapsulating business logic in lightweight, testable objects without tying them to ActiveRecord.

## Use Case: Reputation System for `Account`
We'll create a `Reputation` class that handles reputation-related logic for an `Account`, keeping the `Account` model clean and maintainable.

## **Step 1: Define the `Account` Model**
Create or modify the `Account` model to include the `Reputable` module.

```ruby
class Account < ApplicationRecord
  include Reputable
  # Other Account logic
end
```

- `Account` inherits from `ApplicationRecord`, meaning it is an ActiveRecord model.
- It **includes `Reputable`**, which will define the reputation-related behavior.

## **Step 2: Create the `Reputable` Module**
Modules (concerns) allow us to keep the main model clean while extending its functionality.

```ruby
module Account::Reputable
  def reputation
    @reputation ||= Account::Reputation.new(self)
  end
end
```

### **Key Details:**
- `reputation` is **lazily initialized**, meaning an `Account::Reputation` object is only created when first accessed.
- `self` (the current `Account` instance) is passed into the `Reputation` class so it can operate on it.

## **Step 3: Implement the `Reputation` PORO**
The `Account::Reputation` class encapsulates all reputation-related logic.

```ruby
class Account::Reputation
  def initialize(account)
    @account = account
  end

  def flag_as_unmistakably_bot
    # Business logic for flagging the account
  end

  def clear_bot_status
    # Business logic for clearing bot status
  end
end
```

### **Key Details:**
- This class **is not an ActiveRecord model**; it is a PORO.
- It takes an `Account` instance in its `initialize` method.
- It defines methods for reputation-related operations.

## **Step 4: Usage in Application Code**
Now, we can use this pattern within our Rails application.

```ruby
account = Account.find(1)
account.reputation.flag_as_unmistakably_bot
account.reputation.clear_bot_status
```

- `account.reputation` returns an instance of `Account::Reputation`.
- Methods on `Reputation` can be called directly on `account.reputation`.

## **Benefits of This Approach**
### ✅ **Separation of Concerns**
Keeps the `Account` model focused on persistence while moving business logic elsewhere.

### ✅ **Encapsulation**
All reputation-related logic is neatly organized within the `Account::Reputation` class.

### ✅ **Lightweight & Testable**
Since the `Reputation` class does not depend on ActiveRecord, it can be easily tested in isolation.

### ✅ **Reusable & Maintainable**
Other models can include `Reputable` without duplicating logic.

## **Extending the Pattern**
- **Persistence:** If reputation data needs to be stored, you can introduce an `AccountReputation` ActiveRecord model.
- **Multiple Reputation Types:** The `Reputation` class can be expanded to handle different scoring systems.
- **Service Objects:** If reputation logic becomes complex, consider extracting services that operate on `Reputation`.

## **Use PORO When:**
A **Plain Old Ruby Object (PORO)** is a simple class used to encapsulate **domain logic** within objects. Use a PORO if:

1. **Encapsulating Business Logic** – When logic belongs to a domain entity (e.g., handling reputation, user roles, or pricing calculations).
2. **Maintaining State** – If you need instance variables to store and manipulate data across multiple methods.
3. **Object-Oriented Design** – When modeling a concept as an object that interacts with other domain objects.
4. **Reusability Across the Codebase** – When the logic needs to be used in multiple places but remains tied to an entity.
5. **Independence from Rails** – If logic can exist outside of ActiveRecord and does not require database transactions.


## **Conclusion**
This PORO pattern is an elegant way to separate business logic from database models, making the application **more scalable, testable, and maintainable**.
