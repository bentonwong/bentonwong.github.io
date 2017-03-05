---
layout: post
title:  "My First Ruby Gem: Real Time BART Departures Info via CLI"
date:   2017-03-05 01:33:59 +0000
---


After a couple days of work, I created and published a gem that provides real time BART train departure times via the command line interface (CLI).

## What is BART?
![](http://imgur.com/3MjQXPV)
Source: bart.gov

BART (http://www.bart.gov), which stands for Bay Area Rapid Transit, is the elevated and subway train system serving the San Francisco Bay Area. As a convenience provided to its riders, BART pushes real time departure information on its website so riders may see when the next trains are arriving at a specific BART station (see: https://www.bart.gov/schedules/eta).

## Why Create This App?

To make this information more readily accessible, I wrote a Ruby CLI application (http://www.github.com/bentonwong/rt_bart), and created and published a gem, which has been published as ‘gobart’ to the RubyGems.org website (https://rubygems.org/gems/gobart).

Although mobile apps and the bart.gov website are available, riders only have to type 2 strings into a CLI to pull real time BART train data:  (1) users would type “gobart”.  (2), they type in the 4 letter code for their desired station. And voila, the real time departure data for all the trains at the particular station are displayed for the user.  The user also sees additional information about their station such as advisories, number of trains running systemwide, see recent searches, and optional station information.  This gem is geared more for frequent BART riders who do not want to miss their train nor do they want to wait around at the station, while having this information accessible at their fingertips.

![](http://imgur.com/9dzDV1ohttp://)
Source: Benton Wong

## The Process

### Setting user requirements

As a frequent rider of BART, keeping constant tabs on when trains are arriving and any delays saves me time. To this end, I wanted riders to:

1. Retrieve real time departure data for any BART station within 5 seconds from the CLI in order to get the information faster from a website or mobile app.
2. Have easy to read information in order to make a quick decision on when to leave for the BART station to catch a particular train. 

### Coding the application

The application was written in Ruby, using bundler.io to set up the gem.  Most of work was put into coding the libraries.  The libraries consisted of a controller, an object class, and an information scraper. 

The **controller** obtains the user’s input (i.e. the BART station that the user wants departure information for), makes calls to other classes to request and send back information, and displays the desired station information.   The controller is the most complex of all the libraries since all of its inputs requires validation code and continues to prompt the user until proper input is provided.  Also, it has to convert and display the large set of values in an user-friendly and easily readable format.  Departure data is displayed as a list, sorted by destination with times right below each destination and the length of those trains.  Below that, any station advisories (e.g. delays, police activity, medical emergencies) and the number of trains running systemwide are displayed.

The **class object library** named Station, which is called by the controller, instantiates the desired BART station as an object to manage all the information related to it.  The object has properties such as station name, station information, advisories, and most importantly, its real-time status information. Also, the class stores all of the instances created in that session so that a new instance is not created if the user searches for that station again and it reduces the number of calls to the BART website as the object is initialized with station website information.  Having instances of stations as objects allows for flexible storage management options, controlling scraping requests, and receiving back that information.

The **scraper library** consists of class methods for scraping information from the BART website for all the above information using *Nokogiri* and *open-uri*.  This was the most challenging part of the project.  Initially, scraping the http site itself was challenging.  The pages auto-refreshed every minute and scraping the destination, times, and train length information proved futile.  Upon further investigation, BART provids a public API (http://api.bart.gov) that made it easy to retrieve the desired information through a parsable XML page displayed on its site.  After signing up for my own developer’s key and figuring out how to make API calls by inserting the correct variables into API, the application could now access specific station information include the desired train status information.  It took much experimenting with the right css selectors and reading developer message boards to extract the desired information.

### Publishing to RubyGems.org

Since I put so much work into it, I felt that I should share it.  There were some useful websites explaining how to do this.  At first, I received a lot of errors with the *rake install*.  I spent much time here editing the application’s gemfile to get the settings right in order to perform a successful build.  After successfully packaging the gem, I signed up for my own RubyGems.org account and uploaded the gem to that website.

Within the first hour after publishing the gem, the application had already about dozen downloads.  Exciting!

## Final Thoughts
I learned quite a bit through this exciting and somewhat challenging project: how to tap into an API, learned more about using class objects, and application design.  It is rewarding to see it up on RubyGems.org and other users actually downloading it.

Since it can save a user’s search history during a session, I hope to revisit it and make smart feature-like improvements on it in the future.

