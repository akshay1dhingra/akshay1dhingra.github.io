---
layout: post
title:      "Rails w/ JS frontend project"
date:       2019-04-16 16:39:00 +0000
permalink:  rails_w_js_frontend_project
---


I chose to update my previous Rails application for this project. The application was designed to allow a user to signup or login with their facebook credentials and look up or create reviews for games that have been submitted to the application. The user can also create a new game if one hasnt already been submitted. 

The JS was added in areas of the application where it could improve the overall UX by means of manipulating the DOM. This improved the speed at which data was loaded on to the page, and another area where the user can submit data to the database via a $.post ajax request. 

I decided to use ajax to retrieve and post json data instead of vanilla js for this project. For me, the syntax is far more intuitive especially when diving several layers deep in a json object to retrieve the data that I needed. 

The application dynamically rendered two pages and a form. The first page is a list of all of the games that are persisted in the database. The second page is a list of Reviews that are associated to a particular game. And finally, the form is dynamically rendered Review once the user submits. The Review was persisted to the database using ES6 Class Constructor and rendered to the DOM using the prototype object. 

You can see my project [here](https://github.com/akshay1dhingra/gamers_unite)
