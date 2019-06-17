---
layout: post
title:      "PostgreSQL in Rails Applications"
date:       2019-06-17 15:31:36 +0000
permalink:  postgresql_in_rails_applications
---

![PostgreSQL Logo](https://zdnet4.cbsistatic.com/hub/i/r/2018/04/19/092cbf81-acac-4f3a-91a1-5a26abc1721f/resize/370xauto/ce84e38cb1c1a7c5a2c9e4c337e108ba/postgresql-logo.png)

For a recent application build, I needed to decide on a relational database to use. The application itself was relatively simple. It had a need for user profiles, data persistance, and a few simple SQL queries. Rails, by default, includes SQLite as its choice for database. And don't let the "Lite" aspect of it fool you. SQLite can be a quite powerful tool. However, PostgreSQL is another open-source system that is widely used in production. While PostgreSQL is not as light and requires more space, configuration, and a DB server to operate, I ultimately sided with it for this application. The deciding factor was its compatibility and relatively simple integration with Heroku and Heroku deployed apps, which is what I ultimately was planning for this app.

Therefore, if you're planning a Rails application and are even remotely thinking of possibly hosting it on Heroku, then I would strongly suggest starting your app with PostgreSQL. It will save you much time come deployment time. And, if there is one thing I've learned, it's that switching database systems at deployment time is a pain in the rear. So, how to start a Rails application with PostgreSQL? You can follow the steps below.

## First things first: Install PostgreSQL
Not super fun, but totally necessary...

1) Head over to the [PosgresSQL download page](https://www.postgresql.org/download/) and choose the correct package for your OS. There are other ways of installing PostgreSQL, such as through Homebrew for macOS. However, the downloaded packages take care of downloading and installing the most commonly used and needed tools, along with both graphical and command line modes.

2) Once PostgreSQL is installed, open it up and make sure the server is running. You shouldn't have to do any additional server configuration at this moment.
## Create Rails Application with PostgreSQL
Now the fun part...

3) Use the following command to create a Rails application. This will create your standard application files and configure/connect your app to PostgreSQL. Of course, you can also add other needed options here, such as `--api` or `--no-test-framework`.
``` bash
rails new [insert-application-name] --database=postgresql
``` 
4) Once the application has been built, you will have to then create the database that will be used by the application. With SQLite, running migrations will automatically create the database. Not so with PostgreSQL. To do so, simply run:
```bash
rails db:create
```
That's it! At this point, if everything was successful, you should be able to open up PostgreSQL and see your newly created databases up and running. Happy coding!
