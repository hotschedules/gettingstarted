Building Mobile Apps
=====================
## Overview

### Scope

This tutorial will show you how to quickly create a new app and publish it to the cloud. By the end of this tutorial you should be able to see your newly created app in the mobile container.

### Intended Audience

This tutorial is designed for a new developer looking to create a new app, publish it to the cloud, and see it in their mobile container. The tutorial assumes the developer already has npm and node installed on his or her computer. It also assumes the developer already has valid credentials for a namespace.

## How Do I Build a Mobile App

### Download bodhi-cli

bodhi-cli is a command line tool that will help facilitate building apps, publishing apps, and assigning a creating a profile for the app. 

You can download this tool at: https://github.com/redbookconnect/rbc-cli-tools. 

Click "Download ZIP" located at the bottom of the right side menu.

### Install bodhi-cli

Unzip the tool and `cd` into it.

Install the tool. 

```
> sudo npm link
```

### Set up your environment

Create a new directory for your bodhi-cli project anywhere you want.

```
> mkdir <project-name>
> cd <project-name>
```

Initiate a bodhi-cli project in a new directory.

```
> bodhi init
```

Put in environment credentials to rbc-project.json. The rbc-project.json file was created by the step above.

```
> bodhi new <environment> -s <api-endpoint> -n <namespace> -u <username> -p <password>
```

Check to see if we set up the environment correctly.

```
> bodhi view <environment>
{
  "uri":<uri>,
  "user":<username>,
  "password":<password>,
  "namespace":<namespace>
}
```

*Check out other environment commands [here](../rbc-cli.md).

### Create a new app

Create a new app project with a project skeleton in /apps/\<app-name\>.

```
> app-tools new-app <app-name> -t <project-type> -m <type-name (if -t = app-generator)>
```

\<project-type\> should be one of the following values:
 * custom: this will create a very simple skeleton app that uses no frameworks
 * angular: this will create a angular skeleton app
 * app-generator: this will generate a list-detail app that displays the 20 most recent records of the type you specified through the -m flag.
 
Each project type will have a README.md that further explains how the that skeleton app works. It will exist in the root of the app folder after you run the `new-app` command.

### Develop

Start developing your app in /apps/\<app-name\>.

### Add a type to your app profile

Once you know which types a user would need to use your app, edit the app's profile definition. Users that have that profile can use the app.

```
> app-tools add-type-to-profile <type-name> [type-action-options]
```

Type Action Options:

* --select
* --insert
* --username
* --delete
* --aggregate

If you created an app-generator app, the type you specified with the -t flag will be automatically added to the local app profile definition.

View the definition of the profile.

```
> app-tools view-profile-def
```

Example profile attribute in your package.json:
```
{
 ...
 "profile": {
  "name": "appName",
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

Move production ready files into /apps/\<app-name\>/www. This directory is where production ready code will live.

If you are using app-generator or angular skeleton app, `grunt prod-build` will do this step for you. Please see their respective README.md files for more information on other helpful grunt commands.

Publish your app.

```
> app-tools publish-app [env-options]
```

This command will zip up whatever is in /www and send it to the cloud. This command will also automatically assign the app profile to the publisher.

You can only publish an app if you have the admin profile. The app's name also has to be unique to the namespace; if it is not and if you are not listed as the developer of the existing app, when you publish, app-tools will inform you an app of that name already exists and will ask you whether or not you want to proceed and overwrite the existing app. If you are listed as the developer of the existing app, app-tools will publish your new app and overwrite the existing app in the cloud.

Check to make sure your app was uploaded by checking if the cloud has created a record for your app. In your browser go to the following link: 

\<api-endpoint\>/\<namespace\>/apps/\<app-name\>
 
### Check your app
View your app in the browser:

\<api-endpoint\>/apps/\<namespace\>/\<app-name\>/index.html 

*NOTE: you need to be logged in as the user you just created in the above step.

View your app in the container by logging in as the user you just created.

### Update app

Make further changes to your app.

Republish your app.

```
> app-tools publish-app [env-options]
```

If someone published the same app before you and is listed as the developer in the app's meta data in the cloud, you will be prompted on whether or not you want to overwrite that app. This is to prevent someone accidently overwriting apps.

Refresh your app in the browser. You should be able to see the changes you just made.

### Give another user access to your app

Add your app profile to an existing user.

```
> app-tools add-profile-to-user <username> [env-options]
```

*Note: you need to do this as an admin.

## Contract
* html file must be called index.html. It must reside in the root of the app directory.
* index.html, LICENSE, and package.json must be in the root of the app directory.
* If you want to include an app icon for the menu screen, icon.* must be located at the root of the app directory.

 Please see [rbc-cli.md](rbc-cli.md) for documentation on app-tools commands.
