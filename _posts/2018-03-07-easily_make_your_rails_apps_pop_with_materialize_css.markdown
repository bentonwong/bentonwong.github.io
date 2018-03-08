---
layout: post
title:      "Easily Make Your Rails Apps Pop with Materialize CSS"
date:       2018-03-08 04:56:32 +0000
permalink:  easily_make_your_rails_apps_pop_with_materialize_css
---


The default styling and elements provided by Rails are very functional, but can be a bit plain and spartan.

It can be vastly improved without doing too much front end work using [Materialize](http://www.materializecss.com), which describes itself as "a modern responsive CSS framework based on Material Design by Google".

On a recent Ruby on Rails web application that I created, an employee scheduling app, Materialize significantly enhanced the look of the app:

![](https://i.imgur.com/Nfe4D4R.png)

## Adding Materialize to a Rails App in 3 Easy Steps

1) Add gem 'materialize-sass'  & bundle install it

Add this gem to the app's gemfile:
```
gem 'materialize-sass'
```

Then, install it by executing the following command in the directory's terminal:
```
bundle install
```

2) Change the application stylesheet file extension from .css to .scss

In the assets/stylesheets directory, there should be an application.css file. Change its extension to .scss so it becomes application.scss

3) Add '@import "materialize";' to the newly modified 'application.scss', which should now look like this:

```
/*
 * This is a manifest file that'll be compiled into application.css, which will include all the files
 * listed below.
 *
 * Any CSS and SCSS file within this directory, lib/assets/stylesheets, or any plugin's
 * vendor/assets/stylesheets directory can be referenced here using a relative path.
 *
 * You're free to add application-wide styles to this file and they'll appear at the bottom of the
 * compiled file so the styles you add here take precedence over styles defined in any other CSS/SCSS
 * files in this directory. Styles in this file should be added after the last require_* statement.
 * It is generally better to create a new file per style scope.
 *
 *= require_tree .
 *= require_self
 */
 @import "materialize";
```
## Restart the rails server to see the improvements
After restarting the rails server, we instantly see subtle changes as Materialize applies some default styling. Here, we see changes such as removal of the underlining from underneath hyperlinks, applying color to the edit link, adding a horizontal line to the index page table, and changing the default text color from harsh black to a softer gray.  Even the forms look a bit cleaner.

![](https://i.imgur.com/RZHYcsh.png)

![](https://i.imgur.com/dTodmVW.png)

## Materialize Has Many More Customizable Options
Materialize makes it easy to incorporate cool looking design elements directly into view pages such as navigation bars, buttons, forms, icons, tooltips, modals, grid layouts to name a few.  Adding elements and getting them to work often requires putting special materialize key words in the class of an html element and adding some simple javascript code.  The Materialize site is the best guide on adding elements to apps.  

There are also, a couple of recommended blog post below to check out specifically related to incorporating Materialize into Rails apps.  If adding a `form_for` helper, the last link below is a very good guide on modifying the `form_for` syntax to play nicely with Materialize.

## Helpful Links
* http://materializecss.com/
* https://www.youtube.com/watch?v=A4pv_NZV2XA
* https://medium.com/@bruce.sarah.a/add-style-to-your-rails-app-with-materialize-30ef8d320ac0
* https://medium.com/@katedoesdev/materialize-forms-6f626eab5516



