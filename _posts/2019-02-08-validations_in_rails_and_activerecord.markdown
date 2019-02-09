---
layout: post
title:      "Validations in Rails and ActiveRecord"
date:       2019-02-08 20:20:58 -0500
permalink:  validations_in_rails_and_activerecord
---


Databases are great! Actually, let's be more specific: databases with valid data are great. Databases with missing or invalid data are not. It can be a pain in the neck trying to deal with invalid data. Validations allow us to ensure that only valid data is saved into our database. A very simple example would be dealing with users. In many cases, a user must have a name, an email, etc. And we don't want to save a user without those details. How can Rails help us?
```ruby
class User
  validates :name, presence: true
end

User.create(name: "Isaac Villicana").valid?  #=> true
User.create(name: nil).valid?  #=> false
```
Fortunately, Rails makes it simple for us to provide that validation. In the example above, we require a user to have a name in order to be successfully saved to the database. Yet, in this same example, a name of `1#&67g23sxs&` would still be considered valid. Let's change that to only allow letters. And, while we're at it, we should make sure that our emails are unique (not two users can have the same email).
```ruby
class User
  validates :name, :email, presence: true
  validates :email, uniqueness: true
  validates :name, format: { with: /\A[a-zA-Z]+\z/, message: "may only have letters"}
end

  user = User.create(name: "1#&67g23sxs&").valid? #=> false
  user.errors.full_messages #=> ["Email is invalid", "Name may only have letters"]
```
We added a format option, and using RegEx, we ensure that only letters are accepted. We also added a message to inform the user of the error. Notice that, although ActiveRecord instantiated a new `User` object, it is not saved to the database. This allows us access to the collection of errors, which we can then use to display them to the user.

