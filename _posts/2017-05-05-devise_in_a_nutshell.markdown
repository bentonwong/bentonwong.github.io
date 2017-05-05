---
layout: post
title:  "Devise in a Nutshell"
date:   2017-05-05 19:57:30 +0000
---


Devise adds authentication functionality to other Rails applications.  It has generators for creating controllers, views, and routes that handle such user authentication features, such as user sign in and sign out, registration, and password recovery, among other things.  

It has 10 modules, which developers can pick and choose to implement within the authenticated user model, that include:

* Database Authenticatable: checks whether user has entered the correct password, and encrypts user passwords before saving to the database
* Omniauthable: allows users to sign up/log in with their accounts from popular sites such as Google, Facebook, etc.
* Confirmable: provides email confirmation process during sign up
* Recoverable: allows for password reset
* Registerable: provides user registration, and account editing and deletion
* Rememberable: remembers the user from a saved cookie when the user returns the site
* Trackable: records user sign in, timestamps, and IP address
* Timeoutable: expires inactive user sessions
* Validatable: checks for valid email and password
* Lockable: locks the account after multiple failed sign in attempts

If properly installed, developers gain methods such as, but not limited to:

* valid_password?(password)
* user_signed_in?
* current_user
* user_session

Installing Devise requires:

1. Adding “gem ‘devise’” to the Gemfile
2. Executing the following shell commands
```
bundle install
rails generate devise: install
rails generate devise <class name of user model>
rake db:migrate
rails generate devise:views <class name of user model>
```
3. Configure views, such as login, registration, etc. in the /app/views/users
4. Configuring Devise by changing the global config file at: config/initializers/devise.rb
* Change “config.scoped_views” to “true” to allow customization of devise generated views such as the login form, or registration forms
* Change other settings as directed by its enclosed documentation
* Set up user roles in the user model, such as an “admin”, which adds helper methods (e.g. .admin?, .role) via “enum role: [:normal, :moderator, :admin]”
* Subtract undesired Devise modules in the user model
5. Add “authenticate_user!” to controllers (e.g. ApplicationController)
* This verifies that a logged in user only has access to specified or all controller actions via a “before_filter :authenticate_user!” placed within a controller 
* Non-logged in users are redirected to Devise’s own sign-in page

Like ActiveRecord, Devise adds another layer of abstraction to Rails applications.  It reduces work in having to develop authentication code.  However, if one runs into issues, debugging can be difficult since the code is not easily visible and there is heavy dependence on what Devise generates.  Nevertheless, Devise is a great authentication solution for most purposes.
