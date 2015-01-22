Building mobile apps
=====================
## Overview

## How Do I Build a Mobile App

### Set up an environment
Initiate a rbc-cli project in a new directory.
```
$> rbc-cli init
```
Put in environment credentials to rbc-project.json. The rbc-project.json file was by the step above.
```
$> vi rbc-project.json
```

### Create new app

Create a new app project with a project skeleton in /apps/[APP NAME].

```
$> app-tools new-app [APP NAME] -t [PROJECT TYPE]
```

*NOTE: [PROJECT TYPE] should be one of the following values:
 * custom
 * angular
 * app-generator
 
### Develop

Start developing your app in /apps/[APP NAME].

### Add Profile

Once you know which types a user would need to use your app, specify the profile definition in your app's package.json. Users that have that profile can use the app.

Example profile attribute in your package.json:
```
{
 ...
 "profile": {
  "name": "myAppProfile",
  "dml": {
    "Store: {
     "select": {},
     "update": {},
     "insert": {},
     "delete": {}
    },
    "Application": {
     "select": {},
     "update": {},
     "insert": {},
     "delete": {}
    }
  }
 }
}
```
*NOTE: For the time being, the type Application MUST be included with all the functions (select, update, insert, delete) in order for the user to be able to see the app.

### Publish

Move production ready files into /apps/[APP NAME]/www. This directory is where production ready code will live.
```
$> cp * www
```

Publish your app.
```
$> app-tools publish-app
```
*NOTE: This command will zip up whatever is in /www and send it to the cloud.

Check to make sure your app was uploaded by checking if the cloud has created a record for your app. In your browser go to the following link: [API ENDPOINT]/apps/[APP NAME]
 
### Create a user with the new profile

Create a user with the new profile so that you can see the app.

*NOTE: You need admin rights to create a new user.

```
$> curl -is -X POST -H Content-Type:application/json -u [USERNAME]:[PASSWORD] -d '{"username":"[NEW USERNAME]","password":"[NEW PASSWORD]","email":"[USER EMAIL]","profiles":["[FULL PROFILE NAME]"]}' [URL]
```
 
### Check you app
View your app in the browser: [API ENDPOINT]/apps/[APP NAME]/index.html 

*NOTE: you need to be logged in as the user you just created in the above step.

View your app in the container by logging in as the user you just created.

### Update App

Make further changes to your app.

Republish your app.
```
$> app-tools publish-app
```

Refresh your app in the browser. You should be able to see the changes you just made.

## Contract
* html file must be called index.html. It must reside in the root of the app folder.
* If you want to include an app icon for the menu screen,
 icon.* must be located at the root of the app folder.

 Please see [rbc-cli.md](./rbc-cli.md) for information on app-tools commands.
