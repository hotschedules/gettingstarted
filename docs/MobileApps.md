Building Mobile Apps
=====================
## Overview
This tutorial will show you how to quickly create a new app and publish it to the cloud. By the end of this tutorial you should be able to see your newly created app in the mobile container.

## How Do I Build a Mobile App

### Download bodhi-cli

bodhi-cli is a command line tool that will help facilitate building apps and publishing it. 

You can download this tool at: https://github.com/redbookconnect/rbc-cli-tools. 

Click "Download ZIP" located at the bottom of the right side menu.

### Install bodhi-cli

Unzip the tool and `cd` into it.

Install the tool. 

```
$> sudo npm link
```

### Set up your environment

Create a new directory for your rbc-cli project anywhere you want.

```
$> mkdir [PROJECT NAME]
$> cd [PROJECT NAME]
```

Initiate a rbc-cli project in a new directory.
```
$> rbc-cli init
```
Put in environment credentials to rbc-project.json. The rbc-project.json file was created by the step above.
```
$> bodhi new <environment> -s <api endpoint> -n <namespace> -u <username> -p <password>
```

Check to see if we set up the environment correctly.

```
$> bodhi view <environment>
{
  "uri":<uri>,
  "user":<username>,
  "password":<password>,
  "namespace":<namespace>
}
```

### Create a new app

Create a new app project with a project skeleton in /apps/[APP NAME].

```
$> app-tools new-app [APP NAME] -t [PROJECT TYPE] -m [TYPE NAME (if using app-generator)]
```

*NOTE: [PROJECT TYPE] should be one of the following values:
 * custom: this will create a very simple skeleton app that uses no frameworks
 * angular: this will create a angular skeleton app
 * app-generator: this will generate a list-detail app that displays 20 records of the type you specified through the -m flag.
 
*NOTE: Each project type will have a README.md that further explains how the that skeleton app works. It will exist in the root of the app folder after you run the `new-app` command.

### Develop

Start developing your app in /apps/[APP NAME].

### Add a type to your app profile

Once you know which types a user would need to use your app, edit the app's profile definition. Users that have that profile can use the app.

```
$> app-tools add-type-to-profile [TYPE NAME] -s -i -U -d -a
```

* -s = select
* -i = insert
* -U = username
* -d = delete
* -a = aggregate

View the definition of the profile.

```
$> app-tools view-profile
```

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
     "select": {}
    }
  }
 }
}
```

### Publish

Move production ready files into /apps/[APP NAME]/www. This directory is where production ready code will live.

Publish your app.
```
$> app-tools publish-app
```
*NOTE: This command will zip up whatever is in /www and send it to the cloud.

*NOTE: The profile is automatically assigned to the publisher.

Check to make sure your app was uploaded by checking if the cloud has created a record for your app. In your browser go to the following link: 

[API ENDPOINT]/apps/[APP NAME]
 
### Check your app
View your app in the browser:

[API ENDPOINT]/apps/[APP NAME]/index.html 

*NOTE: you need to be logged in as the user you just created in the above step.

View your app in the container by logging in as the user you just created.

### Update app

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
