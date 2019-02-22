---
layout: post
title:      "Rails Collection Select for Form Helpers"
date:       2019-02-22 02:38:20 +0000
permalink:  rails_collection_select_for_form_helpers
---


The official Ruby on Rails documentation is great for many things. It mostly allows for an introduction into concepts and implementations, along with some helpful examples. However, one area where it less than lackluster, is the Form Helpers section. As a technical coach at Flatiron School, I assist other students who are having difficulty understand or implement a concept. And the `collection_select` form helper is one of the biggest culprits of hang ups. `collection_select` allows the form builder to create an HTML `select` tag with various `option` tags nested inside, which allows a user to choose one option from the selection. This is what the documentation provides: 
```ruby
<%= f.collection_select(:city_id, City.all, :id, :name) %>
```
That's all. No further explanation, that I could find. APIDock does go a little further:
```ruby
# collection_select(method, collection, value_method, text_method)
```
A little better. More detail regarding options and parameters to pass in. Many of my students have come to me saying the same thing, "I've read the documentations, but they don't tell me much about the correct implementation". I'll admit that was me as well. So, in response, I'm hoping that I can explain Rails' `collection_select` to help others who may be wishing to use it.

Let's start with a basic example. I have a post that belongs to an author, and an author has many posts. We can assume that associations have been properly built in our database and models. 

According to the docs, the first option we pass in to `collection_select` is the "method on the instance object that will be selected". Therefore, our form to create a new post would roughly look like this:
```ruby
<%= form_for @post  do |f| %>
  <%= f.text_field :title %>
  <%= f.text_area :content %>
  <%= f.collection_select :author_id %>
  <%= f.submit %>
<% end %>
```
Why the option `:author_id`? Because a post belongs to an author, Rails and ActiveRecord build that association by adding an `author_id` column/attribute to all Post objects and giving us a similarly named method. Therefore, it's as if we were calling `@post.author_id`. 

Second, we have to specify a collection, or where we want to receive our selections from. In our case, we want users to have the option to select from all existing authors in our database. Therefore, our collection select now looks like this:
```ruby
<%= f.collection_select :author_id, Author.all  %>
```
Up next is the value method. This option will dictate what the `value` attribute of out `option` HTML tag will contain (e.g. - `<option value="1">Hemingway</option>`). In our case, we want the value to be equal to the id of the selected object. And the final required fourth option is the text method. This option determines what text is displayed in the form. We want our users to see the author's name.
```ruby
<%= f.collection_select :author_id, Author.all, :id, :name  %>
```
results in:
```html
<select name="post[author_id]" id="post_author_id">
  <option value="1">Hemingway</option>
  <option value="2">Shakespeare</option>
  <option value="3">Dickens</option></select>
</select>
```
Collection select is extremely helpful when used in forms, even if its implementation is not straightforward. I hope that by seeing the above example, students will be able to better comprehend the structure and implementation of Rails' `collection_select` form helper.
