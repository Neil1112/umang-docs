# Tech Stack & Code Architecture/Organisation

---

This document gives the description of the technologies involved, and the project architecture. 

## Technologies

The Project is structured in a _Monolith_ structure. Thus the production (i.e - the master branch) has:

- Single server
- Single remote database

### The Stack

The tech-stack chosen for the project is the MERN stack. MERN stands for a group of four technologies used in synergy.

- M stands for MongoDB - A NoSQL Database
- E stands for ExpressJS - A minimalist web framework for NodeJS
- R stands for ReactJS - A frontend library
- N stands for NodeJS - A Javascript Runtime Environment

### Database details

MongoDB is chosen as the database for the project. It is a NoSQL database. Its cloud solutioln named MongoDB Atlas is integrated in the project. The details for the current configuration is as follows:

- Database Type - Cloud
- Service Name - MongoDB Atlas
- Cluster Type - Shared
- Cloud Provider - Google
- Region - Mumbai (asia-south-1)
- Cluster Tier - M0 Sandbox
- Cluster Tier Pricing - FREE
- Connection String - mongodb+srv://admin:_ENTER_PASSWORD_%21@cluster0.x2jgv.gcp.mongodb.net/admin


## Version Control and Branches

Git is used as the Version Control System for the Project. It is configured as a private repository on Github.

> Github Repository - https://github.com/cjaykumar/umangwellness

### Branches

There are a total of 6 branches configured in the Project. They are as follows -

1. master
1. dev
1. dev1.1
1. rajeev-branch
1. rajeev’s-branch
1. rc 1.1

Major branches - master, dev and rc 1.1

#### master Branch

- Responsible for LIVE Production code
- Hosted on - Azure Web App Services
- Currently hosted at - https://umangprod.azurewebsites.net

#### dev Branch

- Responsible for Development code
- Hosted on - Azure Web App Services
- Currently hosted at - https://umang-dev.azurewebsites.net

#### rc1.1 Branch

- Responsible for a standby stable candidate to push immediately to master, if some bug is encountered on the production site



## Code Architecture and Organisation

The code is divided into 2 major modules - client and server.


[![fig-1]][fig-1] [fig-1]: ./../img/general/contact-us-1.png


In the above figure, the directory client represents the frontend part. The rest of the directories and files make up the server.

- The Approach is SPA - Single Page Application implemented using NodeJS as server side and ReactJS for the frontend.
- The API in the server uses the REST technology with the standard HTTP methods.


### Server Side

#### server.js

- server.js is the single entry point governing different environments [production, development, test].
- server.js is also responsible for mapping routes to their respective controllers.

#### package.json

- The package.json is responsible for maintaining 2 important things - scripts and dependencies
- Scripts are pieces of code which are run in specific scenarios to allow a custom configuration to the code.
    - For example - Scripts can be used to start the server or configure the system into test mode.
- Dependencies:
    - Dependencies are mainly pieces of softwares called packages which are developed by other programmers and published on npm.
    - Dependencies are of 2 types, namely - dependencies and devDependencies
    - devDependencies are specific to particular developer, and should play no role in project development



#### Routes and Controllers

The routes directory is responsible for maintaining and organising various api routes logically.
It is also responsible for routing a given url to its respective controller.

##### Walkthrough of an example URL - _api/admin/sendCustomEmail_

The above url is responsible for custom emails written by admin to multiple clients and counsellors existing in the system.

1. The url is parsed by the server.js middleware and will pass it to the appropriate router.

1. The url is then passed to the admin router - adminRouter.
    - The adminRouter consists of all the mappings of urls related to admin and their respective controllers.
    - The url is also differentiated by its HTTP method type - GET, POST, etc.

1. Finally, according to the url and the HTTP method defined, the router passes the query to its respective controller.

The above figure shows the sendCustomEmailController, which is responsible for sending custom emails to clients and counsellors.



##### List of routers

The list of routers currently existing in the system is shown in the figure below


#### Config Directory

The config directory contains files for specific purposes like background services, database urls, environment variables, keys for various packages, etc.


#### github/workflows

- This directory is responsible for holding github actions workflow file.
- The file dev_umang-dev.yml shown in the below example is responsible for defining all the processes and their precedence of the dev branch whenever a new code is pushed.


#### Models

- Models in the code resemble the structure of database collections in MongoDB.
- They are responsible for defining the data-fields, the type related to the data-fields, defining relationships between two models, defining required and default fields, etc.
- The list of model currently defined is as follows -

- Models are used throughout the code for maintaining consistency in the data-fields for a particular document.



### Client Side

The client directory contains all the code needed to create and manage the frontend part of the system.

The structure of the client directory is as follows -

- The directory that is of the most interest to us, is the src directory.
- build, node_modules and public directories are of not that much interest to us.
- package.json is another file that is important to us.


#### package.json

- The package.json is responsible for maintaining the dependencies and scripts for the client side.
- The current package dependencies for the client side is shown in the figure below -

- The scripts for the client side are shown in the following figure -

- The two important scripts here are start and sitemap.
- start is used to run the client side and sitemap is used to generate a sitemap automatically.


#### src directory

- The src directory contains all the important code.
- The directory named assets, contains media files for the pages.


##### index.js

- This file, like the server.js, is the single entry point for the client side.
- It is responsible for rendering the root element in the document.
- We abstract its logic in another file named App.js.
- The index.js wraps the App component by AuthProvider and ThemeProvider.
- Thus allowing all the files and components in the app to use the services offered by AuthProvider and ThemeProvider.


##### App.js

- Like the routing middleware in the server.js which is responsible for matching a given URL to its given controller, the App.js  maps a given URL to its respective UI component.
- It also takes into account what URL requires what kind of role access.
- If the role access requirement is not met, it does not allow the URL to be accessed and falls back to the home page.
- There are 3 types of routes defined - Route, UnPrivateRoute and PrivateRoute
    - Route - It is accessible whether the user is signed in or not. Thus it makes sense to use it for all static pages.
    - PrivateRoute - PrivateRoute takes an array of roles as its parameter to determine which role(s) is/are allowed access to a specific URL.
    - UnPrivateRoute - While PrivateRoute are only visible after signing in; the UnPrivateRoute cannot be accessed after signing in. They are used for URLs similar to Sign Up, Sign In, Forget Password, etc - which are used only at the time of signing in. Once the user is signed in, these URLs makes no sense, and hence must be hidden from the user


#### HOCs

- The HOC directory stands for - Higher Order Components.
- These are custom components that are made upon existing components to achieve some specific results.
- The HOC includes - NetworkDetector, PrivateRoute and UnPrivateRoute
- The NetworkDetector is responsible for determining active Internet connection. If the Internet somehow goes inactive, the NetworkDetector will let the UI components know about it. The UI component can then handle how it wants to interpret the information and display it to the user.
- PrivateRoute as mentioned earlier, is a mean to provide a role based access to various components
- UnPrivateRoute is a means to disable certain URLs after a user has signed in.


#### Services

- Services are meant to abstract and organise the logic for exchanging requests with the server.
- They help us in -
    - Reducing the amount of code caused by repeating the same code by mentioning it at the same place.
    - Allowing any component to access the services. Hence allowing the components to concentrate more upon their custom logic.
    - Easily Tested and limiting the error to them. Hence components can rely on them without worrying about testing the logic and preventing the errors.
    - Allows us to organise all the services related to a particular domain under one hood. For example, we can group all the services offered by Admin under one hood, as can be seen in the below figure.


#### contexts

- The context directory is responsible for maintaining some information and making it accessible across all components.
- There are 3 contexts currently deployed - AuthContext, SelectedCounsellorContext and ThemeContext.

##### AuthContext

- AuthContext lets a component know whether a user has signed in or not.
- It also lets the component know what role access the user has.
- It also lets the component know about the selected timezone by the user.
- It lets the components know that the site is under maintenance or is updated to a newer version.

##### SelectedCounsellorContext

- The SelectedCounsellorContext, lets the components of the client know whether the client has selected a counsellor or not.
- If the client has selected the counsellor, then it also let’s the components know the details about the counsellor.
- It is developed to avoid recursive calls to the API for fetching counsellor information everytime a client component requests for it.

##### ThemeContext

- The ThemeContext serves as a single destination to mention the theme related fields.
- It also solves the problem of updating the theme everywhere, if it changes.
- It allows us to mention the theme fields at one place, and reuse them in all the components.
- Currently the ThemeContext manages colors, fontFamily, fontSize and a custom theme for buttons, paragraphs, texts, forms, etc.
