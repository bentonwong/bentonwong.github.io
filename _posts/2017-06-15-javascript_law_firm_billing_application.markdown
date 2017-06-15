---
layout: post
title:  "Javascript Law Firm Billing Application"
date:   2017-06-14 22:42:10 -0400
---


**Summary**

I recently had the opportunity to improve on my earlier [Rails Law Firm Billing](https://github.com/bentonwong/law-firm-billing-software) application by adding Javascript features to it [here](https://github.com/bentonwong/js-law-firm-billing-software).  The Javascript improvements utilizes jQuery, AJAX, and Active Model Serialization to provide APIs allowing the application to render JSON data in response to an AJAX request.  These new front end features allow for a more dynamic user experience where certain pages are updated without a page reload.

**New Javascript Features**

*Displaying Client Profiles*
* Allows users to sift (i.e. navigate to the next client) through a collection of clients from a client's show page; no page reload is required to display the next client, and is rendered by making an AJAX get request and the response is displayed using a handlebars template.
* A concatenate feature takes the two separate client phone and email data fields and merging them into one line with appropriate labels; this feature is a method on the JS prototype of the client's model object.

*Lawyer Show Page Improvements*
* API provides information on each lawyer is available, revealing the many clients, matters, and time entries each individual lawyer has; Active Model Serializer was used to generate the custom JSON that is rendered through the API.
* The resulting JSON has information about a lawyer's cases and clients, which is rendered on the lawyer’s show page after an object is created on it.
* A method on the lawyer prototype was implemented to calculate how many hours have been bills so far by the lawyer supervising the case, which is appended to the end of the table row of the associated matter.

*Time Entries On Matter Show Page*
* Each matter (legal case) has many time entries which lawyers use to track each task in order to later bill the client on the matter’s show page.
* All the time entries for that matter are listed on the matter's show page, using jQuery to make an AJAX get request.
* New time entries can be entered directly on that matter's show page and those new entries, if valid, are appended to the list without a page reload.
* Responses from every successful AJAX requests are translated into a model, and a method on each time entry prototype instantaneously calculates the attorney fee on that time entry object, which is then appended to the end of each time entry row.

**Process**

I broke this project into 3 steps:
1. Plan out the new Javascript features by reviewing the original Rails application and making decisions on where to implement the new features.

2. Code the features by:
-Building the Javascript features alongside the Rails implementation of it to make sure the new features worked as expected
-Making the new features function first
-Deprecate those Rails features that were replaced by Javascript
-Refactor and organize related Javascript features into separate files to make the code more readable

3. Testing
This project was challenging because this involved working between 3 different stacks (Javascript, HTML, and Rails).
I had to perform extensive testing to make sure that the new Javascript features worked the similarly to the Rails features the Javascript code replaced.

Such testing included reseting the database to ensure that the program worked when no lawyers, clients, and matters are in the system.  Under that use case, I discovered that additional error checking logic needed to be implemented, which was then added to address them.

