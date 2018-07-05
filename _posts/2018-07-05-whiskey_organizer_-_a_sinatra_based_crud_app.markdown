---
layout: post
title:      "Whiskey Organizer - A Sinatra based CRUD app"
date:       2018-07-05 19:09:05 +0000
permalink:  whiskey_organizer_-_a_sinatra_based_crud_app
---


After hours and hours of coding, I like to reward myself. And what better present to enjoy that a dram of good ol' whiskey. Yes, I, like many others, have a collection of various whiskeys at home. Mine is would hardly qualify as extensive. But enough to sometimes lose track of what I drank and when I last sipped America's native drink. Hence, the Whiskey Organizer.

And that's what I built for my Sinatra portfolio application. Whiskey Organizer is a CRUD app that allows a user to create an account and add items to their collection. Each item contains a whiskey, and each whiskey has information such as brand, name, type, and the date this specific item was enjoyed by the user. Such an application involves major design decision right from the start. 

### Decision #1 – Database Schema and Design

In a Model-Views-Controller (MVC) web application, a database is essential for persisting manipulated data. Because data is the foundation of the web application, I decided to begin creating Whiskey Organizer by designing a database based on a real-world collection. A person may have a collection composed of individual items. Each item is composed of a specific whiskey. This made my model associations easier to visualize, which became my second biggest decision.

But at least now I knew that I wanted three models, represented by three respective tables: users, items, and whiskeys. The users table had columns for name, username, email, and password_digest (bcrypt gem was utilized). Whiskeys had a brand, name, and type. On a side note, I learned that some words cannot be used as column names, such as ‘type’, because they are reserved by ActiveRecord for other purposes. Therefore, I had to change the column name of ‘type’ to ‘whiskey_type’. And an item would have a column of type string that would contain the last date an item was tasted. This brought me to associations between the databases.

### Decision #2 – Database Associations

The ActiveRecord library was used in this application for object-relational mapping. This function depends on proper associations between various models and the database. Again, I based these associations on a real-world collection of whiskey items. So, a single User has many Items and, through these items, has many whiskeys. The reverse of this logic is also true. On the other hand, a single Item belongs to a single User as well as to a single Whiskey. Because I did not have a “has many” to “has many” relationship, no join table was needed in the database.

![DatabaseAssociations)](https://i.imgur.com/BSa8D2rl.png)

### Decision #3 – Controllers

I decided that each model would have its respective controller, all of which would inherit from the application controller. But not all would be created equal. For example, because Items connected Users with Whiskeys, the items controller would have the most functionality. It would be responsible to creating, reading, updating, and destroying items. The user controller would of course create users and log them in and out. The whiskey controller would be responsible for simply reading its respective model.

