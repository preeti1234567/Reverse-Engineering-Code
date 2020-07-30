# Reverse Engineering Code

The purpose of this work is to go through the codebase and explain the details of the code. 


## server.js 
a) The purpose of this file is to include all the packages required to run this application 
1. Express- provides tooling for HTTP servers
2. express-session - for create a session middleware
3. passport package with passport-local which is defined in passport.js file

b) Setting up the port

c) Require models for syncing

d) By using the package we are creating the express app,

e) We are using the inbuilt middleware method of express.urlencoded() for data parsing, to recognize the incoming Request Object as strings or arrays

f) We are using the inbuilt method of express.json(), to recognize the incoming Request Object as json object

g) We are using the middleware function to serve static files such as images, CSS files, and JavaScript files

h) We are using sessions to  keep track of our user's login by giving session ID over cookies.

i) Initiate the passport middleware 

j) For persistent login session middleware (passport.session()) is used

k) Requires routes file by express package

l) Syncs our database and log a message to the user upon success

## modals
*index.js*
1. 'use strict'statement -It helps you to write cleaner code and preventing from using undeclared variables.
2. import filesystem, path, sequelize modules, path for extracting the filename as module, setting the environmental variable  
from the node process if present else development environment which is used to connect to database,
3. Read all the file from directory(models) having .js as extension, except the basefile where this code lies (file!=basename)
4. For each file, 
    1. read the file 
    2. import the model e.g.(user.js import user model) using sequlize
    3. store the model in db object with modelname as key and model object as value e.g.( user is key and usermodelObject is value)
5. For each key(modelname) in the db object, associate key with the db object.
6. Attach db object to sequelize 

*user.js*
1. require bcrypt for storing hash in a password
2. Creates a user modal by exporting a function which accepts the argument of sequelize (which has the connection to my db) and Datatypes. In the sequelize we are creating an object of column as key and value as object of db type/constraint as key and its value as value
3. User model has method to validate password which accept an argument password which is used to compare using bcrypt.comparesynce against the user model password
4. Using hooks we are hashing the password before user is created with email and password

## config
*middleware*: authenticated route is determine. If the user is login in, user's request will responded and can enter the restricted route and if not logged in redirect them to the login page

*config.json*: which contain the environmental variable of development, test and production with details of database connection at their respective environment.

*passport.js* 
1) We require passport npm package and passport-local package. This module let us authenticate using a username and password in your Node.js applications. By plugging into Passport, local authentication can be easily integrated into any application or framework that supports middleware.
we are initializing the local strategy module to know the passport that we want login with a username/email and password. In this case only email is needed to sign in. So passport using localStrategy will initiate a function (which has argument of email, password, callbackfuntion) where it is check that if user's email and password matches it will return the dbuser object.

2) we are using serializer and deserializer method to keep authentication state across HTTP requests.

## public
### js
*login.js*
 1) this file contains code for on ready function we are having a pointer which points to the login form with emailinput and passwordinput.
2) on submitting the loginForm we are getting the email and password.
3) if we have the user information of email and password then we are running the login function where we are passing the parameter for user email and user password
4) That function post to our api/login route and replaces the current resources with the one at the provided URL.
5)If there is an error catch method will console log the error.

*member.js*

1)this file checks which user is logged in and gives the updated HTML on the page

*signup.js*

1) This file processing is similar to login.js. In this we are pointing to the signupForm and on submitting the signup form with email and password and then send it to the function where it post to the sign-up route and if successful redirect to the resources with the one at the provided URL.
2) the catch function throw an error and fadeIn (400) determine changes in the opacity  for that period of time.

## routes
### api routes
*4 api routes have been set*

- "/api/login" post route for if the user has valid login credentials send to the member page.

- "/api/signup" post route, if the user signup succesfully create a user or send a status code of 401 

- "/logout" get route for loggin user out that is back to "/" route

- "/api/user_data" get route for getting some data about our user to used client side. If the req.user, return empty object, user is not log in and an empty object is returned in the res.json. Otherwise the user email and id are returned.

### html routes
*3 routes have been set.*

- "/" get route if the user already has an account send them to member page if not redirect to the signup.html page

- "/login" get route if the user has login then send it to member page else redirect to the login.html 

- "/members" get route we add our isAuthenticated middleware to this route and if a user who is not logged in tries to access this route they will be redirected to the signup page.If successfully authenticated he can access the members.html












## Submission on BCS

You are required to submit the following:

* A link to a Google Doc or video explaining the application in `Develop/`. 

_Note: Don't forget to change the sharing settings on your Google Doc._

- - -
© 2019 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
