---
layout: post
title:  "Learning about the asynchronous nature of Javascript the hard way"
date:   2017-06-08 23:17:30 +0000
---



While recently working on a Rails-JS Tic Tac Toe game, I encountered unexpected bugs which I spent a long time trying to figure out.  These bugs include:

* having to click twice to get data to initially load from the database
* clicks from a previous game would persist into a new game

It drove me nuts because I could not understand what was going on.  After a while, I discovered that functions that I wanted to be called later were being called before the current function had completed its task.  That was my first true introduction to the asynchronous nature of Javascript.  

Coming from Rails, this felt out of place. Its synchronous nature had a controllable flow and order.

In my particular situation, I was performing an AJAX request and then expecting that once the request was complete, it would perform particular functions obtained from the AJAX request:

```
function loadGame(id) {
  $.getJSON("/games/" + id).done(function(response){
    board = JSON.parse(response.state);
      });
currentGame = response.id;
loadTable();
analyzePreviousGame();
};
```

Functions loadTable() and analyzePreviousGame() are dependent on board to properly work.  It worked, but not perfectly and had some noticeable hiccups similar to the issues described above.

What smoothed out those issues was moving those subsequent functions into the AJAX request’s .done callback option:

```
function loadGame(id) {
  $.getJSON("/games/" + id).done(function(response){
    board = JSON.parse(response.state);
    currentGame = response.id;
    loadTable();
    analyzePreviousGame();
  });
};
```

Afterwards, the game worked as expected and even felt snappier when loading data into the DOM.

My takeaway here is to keep in mind its asynchronous nature of JS and place subsequent functions expected to be called immediately after the completion of an immediate function or request, in its callback option.


