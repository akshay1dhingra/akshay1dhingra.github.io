---
layout: post
title:      "Sinatra Web-App: Wine Cellar"
date:       2018-10-26 00:31:46 +0000
permalink:  sinatra_web-app_wine_cellar
---


## Introduction
This is a Sinatra web application for a digital Wine Cellar. The purpose of this application is for the user to store their wine collection on an online database where they can access and update their collection. 

The user will be prompted to create their own unique username and associate it with their email address and password. The user will be forced to create a unique username that is not already associated with another user. After creating the user credentials, they will be prompted with choices to either add a new bottle, see their entire bottle collection or logout.  When creating a new bottle, the user will be asked to provide the bottles name, type, year and location of the item. They can also edit and delete the bottle from their collection as well. 

## App Walk-through 
The welcome page allows the visitor to choose between three options: Signup, Login, and Cellar Page. 

### Signup
The user can create their credentials by clicking on the signup link on the main page. A bug that I had uncovered during the second iteration of refactoring was when a user was able to create their credentials, but the app had no way to check if those credentials had already been taken by another user. I added a verification process where once the controller recieves the user input, it will verify if the username is already persisted in the database by another object (in this case, user). If the username already exists in the database, the user applicaiton will reload the signup page and the user will have to pick another username. 

### Login
If the user is returning back to the app, and they have already created their credentials, they may use that to sign back into the app. The verification process is placed here to ensure that a session of the app is not already in place and that another user is currently signed in. If a user is signed in, the login link will direct them straight to their wine cellar.

### Cellar Page
A verification process is placed anytime a user is loads or is redirected to the cellar page. This is to ensure that only the user who is signed in can edit, create, or delete their own bottles of wine that are associated to that account. 

Here the user can create a bottle to add to their collection. If the user fails to enter data into one or any of the fields, they will be redirected back to the same page to enter in the information again. 

The Edit page is where the user can edit one or all of the data of that specific bottle. 

From the Cellar page, the user can click on a bottle to see the bottles' details. On this page, the user can choose to delete the bottle from their collection and the user will be returned back to the Cellar page.

## Code Walk-through
In this section I will be walking through each major part of the source code. This application is structured in Model/View/Controller for the purpose of separation of concerns. 

### Model
I used ActiveRecord Ruby library for working with my SQLite3 database. ActiveRecord helps me persist and retrieve data from the database throughout my application. I used 2 migrations to create the Users table and the Bottles table. The following Models were created with the following associations:

Users have many Bottles & Bottle belongs to a User

The Users model also uses the Secure Password ActiveModel so that the user can store their passwords on the database as an encrypted hash

### Controllers
I created separate controllers and implemented RESTFUL routes to handle different tasks.

The Users controller has the following routes: 

a) /index => shows the user the index page where they can choose to see, edit, create bottles and finally logout
b) /signup => shows the user the page where they can signup to use the application
c) /login => displays the login page where the user can use their credentials to access their account
d) /logout => clears the active session and redirects the user back to the main landing page

The Bottles controller has the following routes:

a) /bottles => this page displays each of the users bottles currently associated with the account. Here they can either click on their bottle which will then display the bottles information, or they can add a new bottle to the collection. 
b) /bottles/new => here the user can add a new bottle to their wine collection
c) /bottles/:id => this page is accessed when the user clicks on a bottle from their collection while on the /bottles route.
d) /bottles/:id/edit => the user has the ability to edit any of the information associated to with an individual bottle.
e) /bottles/:id/delete => this route does not have a landing page and is accessed from the /bottles/:id route. This route deletes the bottle from the users collection

### Views
The view pages are separated between the main index landing page, user pages and bottle pages. Each of the views are rendered by meeting certain criteria that needs to be met within each route of the controller. For example, a user can be directed to their wine collection page but if they are not logged in, or if the session is somehow lost, they will be redirected to the login page instead of the bottles page.

## Conclusion
The process of building this application was very rewarding and a fantastic learning experience. Though this application is just in its prototype phase, I plan on revisiting and transcribing the code into Rails with Javascript & React as well. 




