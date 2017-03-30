---
layout: post
title:  "LogMyRun Online Running Log for Teams | An ActiveRecord/Sinatra Project"
date:   2017-03-30 21:23:55 +0000
---

**Description**

[LogMyRun](https://github.com/bentonwong/sinatra-team-running-log) is an online running log I recently developed for running teams and clubs.  Runners log their workouts through their private, secure accounts.  When logging a run, runners enter workout's dates, mileage, and relevant notes.  In addition, runners can view their activity history, and edit and delete their workouts.

Since it is expected that teams will be using this application, runners can share their activities with their fellow teammates.
Users can view the running logs of other athletes on the platform.  Using the collective data of the runners, a leaderboard is provided, displaying top runners by mileage over the current month, year, or all time and the breaking them down by gender.

This is useful to coaches to track their athletes training and to athletes to motivate each other.

**Application Structure**

The application uses a model, view, controller structure.  Breaking it down:

* Models 
1. Runner - stores information about the runner (e.g. name, email, password, gender)
2. Workouts - stores information about the workouts (e.g. date, distance, notes)

* Views:
Landing Page (user login and signup)
Runners
1. Login
2. Signup

Workouts
1. Workouts Index (user’s homepage after logging in)
2. Create New Workout
3. Show Workout
4. Edit Workouts
5. Leaderboard

* Controllers
1. Application Controller (entry point)
2. Runners Controller - controls the sign up, log in, and log out processes
3. Workouts Controller - controls the creation, viewing, edit, and deletion of workouts plus display of the leaderboard
4. Concerns/Helpers - methods pertaining to security and querying database for certain workouts

**Relationship between Runner and Workout objects**

Under models, each runner has many workouts, and a workout belongs to a single runner.  Workout objects relate to a runner via the runner id.  The runner id is used to connect and identify the name and email of the runner associated with a particular workout.

For example, many of the workouts view pages utilize this relationship to display the name attribute of the runner alongside their workout data.

In the team leaderboard, the two objects work together even more.  The leaderboard divides up all the runners by gender.  This requires connecting the runner’s gender attribute to workouts.  ActiveRecord queries the database to return workouts for a certain gender and time frame.  

Using ActiveRecord’s WHERE method was perfect for this task to return the correct workouts for the requested gender and time frame:

`Workout.where("gender = ? AND workout_date >= ?", {gender, e.g. “male” : “female”, {start date for time period})`

**Opportunities to enhance the object models**

Adding attributes to each of the existing object classes can enhance the application’s utility by providing more definition about each object.  Such ideas include:

* Add birthday attribute to calculate a runner’s age to Runners
* Add type of workout (e.g. race, speed, tempo, run) attribute to Workouts

Adding an age attribute can further the grouping of runners with similar physiological characteristics in addition to gender.  Workout types would reveal the variety of the runner’s workout (the current model assumes that each runner is doing only one type of workout, which is just basic running).

