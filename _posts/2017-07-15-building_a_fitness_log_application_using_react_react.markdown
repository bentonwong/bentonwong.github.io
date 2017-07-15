---
layout: post
title:  "Building a Fitness Log Application Using React + React"
date:   2017-07-15 04:48:50 +0000
---


My Fitness Log is an [online log](https://github.com/bentonwong/react-redux-rails-api-fitness-log) allowing users to enter and record their daily health and fitness information such as food, workouts, weight, and any relevant notes providing context to that particular entry.  It is a simple CRUD application I built using a React and Redux front end and a Rails API backend.

![](http://i.imgur.com/DyauRy1.png)

## Key Features
1. Weight Chart
•Shows changes to the user’s recent weight over time
•Calculates and displays average weight below the chart and as a reference line
•Built with [Sparklines](https://github.com/borisyankov/react-sparklines)

2. Form
•Component that can create new posts and edit saved posts
•Calendar date picker to allow user to select the date of the post
•Built with [redux-forms](http://redux-form.com/7.0.0/)

3. Pagination
•Limits index page to display 10 posts at a time
•Pagination bar allows easy navigation and access to older posts
•Built with [Pagination](https://react-bootstrap.github.io/components.html#pagination) from React-Bootstrap

## Structure
The application consists of two separate application: (1) a React-Redux client, and (2) a Rails API.

1. The React-Redux client created with create-react-app generator has 3 container components in which one renders the index page, another one renders the create/edit post form, and a page that shows and individual post.  Four routes were established to handle each CRUD action.  When making API calls, the action creators use fetch() and  RESTful routing.

2. The Rails API was generated with one Posts model and controller with all views rendered in json to make it consumable by the client.

## Challenges

*Getting the Form component to create and edit posts*

**Problem**: Figuring out how to get a blank form to prepopulate the form fields with save post data and then call a fetch put action to persist the changes.

**Solution**: After setting up the form to create and save new posts, I studied how each interacted with the Rails API, action creators, and reducers, and then also incorporated the process used by the show page to load and individual post.   Certain pre and post processes were activated or suppressed (e.g. triggering an API call to fetch post data for editing and initializing for form fields with the data vs. not making an API call when creating a new post) by using if-else statements depending upon the presence of a params id from the url.

*Setting up the Pagination component*

**Problem**: The documentation to set up the Pagination component was not entirely clear.  The component required additional coding to control how the list was rendered on the page and how the list was retrieved from the store.

**Solution**: There is a great YouTube video [here](https://www.youtube.com/watch?v=2qxNVzmiR8Y&t=415s) that shows how to do much of the initial pagination setup. However, some of the latter steps are now obsolete since my application was using react-router v4 and query parsing was no longer supported by it.  After doing additional research, I found two relevant stackoverflow discussions on the topic [here](https://stackoverflow.com/questions/44676551/this-props-dispatch-is-not-a-function-in-react-js-component-file) and [here](https://stackoverflow.com/questions/44673079/cannot-read-property-query-of-null-in-react-js).

## Notes

This was a challenging project because it was full stack application requiring Rails, React, Redux, Javascript, HTML CSS.  I learned a lot from the process and I was very pleased with the result.  Although it seemed overwhelming at times, I just had to be patience and take each part step by step.

