---
layout: post
title:      "Coupon Manager - Rails Portfolio Project"
date:       2018-08-01 14:51:06 -0400
permalink:  coupon_manager
---


Coupon Manager is a web-based application built on the Ruby on Rails framework. It allows users to view coupons to stores submitted by others. A user can also save single coupons to their profile for easy access. Using the powerful Ruby on Rails framework allowed me to implement new features to this application and to improve other features compared Sinatra.

### Intuitive Routes
The implementation of routes in Rails is similar to that in Sinatra, but just different enough to cause slight confusion and headaches. One of the advantages of Rails is the simplification of routes. This is because one of the pillars of the framework is *Convention over Configuration*. As founder David Heinemeier Hansson put it:
>But beyond the productivity gains for experts, conventions also lower the barriers of entry for beginners. [...] It’s possible to create great applications without knowing why everything is the way it is.

At this point, and for this project, I had no need to know every intricacy of how routes function. All I needed was for them to perform their basic function. Thankfully, Rails implements convention in this aspect by allowing resource routing. As shown below, a resourced route implements seven conventional routes in a single line of code. This is especially helpful for CRUD applications.
```ruby
# /config/routes.rb

# creates routes for index, show, new, create, edit, update, and destroy controller actions
resources :coupons 
resources :stores

# nested routes
resources :stores do
  # e.g.,  /stores/:id/coupons/new or /stores/:store_id/coupons/:id/edit
  resources :coupons, only: [:show, :index, :new, :edit]
end
```
The code above also shows an example of nested routes. Because a Coupon model object belongs to a Store model object, it logically becomes one of its children. Nested resources capture that relationship. In the Coupon Manager application, for example, a user can create a coupon that is automatically associated with a specific store by using the `/stores/:store_id/coupons/new` URL path.

### OmniAuth Authentication
Rails also opens the door to more powerful Ruby gems. Once such gem is OmniAuth. It allows an application to authenticate users using various providers, e.g., Facebook, Google. This has various advantages. For the developer, it means not having to worrying about that user's password security within the application database. For the user, it means having to remember one less password.

Once OmniAuth authenticates a user, it redirects the user request to a specific controller action where a User model object is either found or created, and linked.
