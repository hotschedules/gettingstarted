Building mobile apps
=====================
# app-tools
app-tools is a command line tool, bundled with rbc-cli, that allows app developers to quickly generate
an app and publish it to the cloud so that it can be viewed on the mobile container.

### Getting Started

1. `npm install -g rbc-cli`
2. Create a directory for your workspace and `cd` into it.
3. `rbc-cli init` This will create a rbc-project.json which will house all your environment info. It will
also create an /apps directory where your apps will reside.
4. `rbc-cli new [ENVIRONMENT NAME]` This will create a new environment entry in rbc-project.json.
5. Open up rbc-project.json and fill in information about your new environment. <br>
```
// Example
{
     "environments": {
           "[ENVIRONMENT NAME]": {
               "uri": "[API ENDPOINT]",
               "user": "[USERNAME]",
               "password": "[PASSWORD]",
               "namespace": "[NAMESPACE]"
          }
     },
     "default": "[ENVIRONMENT NAME]"
}
```
Once you do this, all commands will be used under the default environment unless you specify otherwise with the -e flag.


Please refer to [rbc-cli.md](rbc-cli.md) for more details on how to install rbc-cli and set up
your project and environment.


## `app-tools` Commands
##### app-tools new-app <app name> [-t (custom (default) || angular) --title --description]
This command creates a skeleton app project in the /apps directory of your project. The two skeleton projects to choose
from are: custom (a vanilla html, css, javascript app) and angular (an angular app with a built-in testing framework using
jasmine and testem and javascript task runner using grunt).

**Example Command Usages**
* app-tools new-app myApp
* app-tools new-app myApp -t angular
* app-tools new-app myApp --title My App --descripton This app does something.

##### app-tools publish-app [-e -n -u -p]*
This command publishes the skeleton app to the cloud.

**Example Command Usages**
* app-tools publish-app
* app-tools publish-app -e devEnv
* app-tools publish-app -n myNamespace -u myUsername -p myPassword

##### app-tools list-apps [-e -n -u -p]*
This command list all the apps that you can see in your specified environment.

**Example Command Usages**
* app-tools list-apps
* app-tools list-apps -e devEnv
* app-tools list-apps -n myNamespace -u myUsername -p myPassword

##### app-tools add-profile <full profile name> [-e -n -u -p]*
This command adds a profile to your app. Users with this profile can then use your app.

**Example Command Usages**
* app-tools add-profile myNamespace.profileName
* app-tools add-profile myNamespace.profileName -e devEnv
* app-tools add-profile myNamespace.profileName -n myNamespace -u myUsername -p myPassword

##### app-tools remove-profile <full profile name> [-e -n -u -p]*
This command removes a profile from your app.

**Example Command Usages**
* app-tools remove-profile myNamespace.profileName
* app-tools remove-profile myNamespace.profileName -e devEnv
* app-tools remove-profile myNamespace.profileName -n myNamespace -u myUsername -p myPassword

##### app-tools list-profiles [-e -n -u -p]*

This command lists all the profiles that are associated with your app.

**Example Command Usages**
* app-tools list-profiles
* app-tools list-profile -e devEnv
* app-tools list-profile -n myNamespace -u myUsername -p myPassword

*command must be run in the directory of the app you are want to publish/update.

## Contract
* html file must be called index.html. It must reside in the root of the app folder.
* If you want to include an app icon for the menu screen,
 icon.* must be located at the root of the app folder.

## Process of Development
1. `rbc-cli init`
2. Put in environment credentials to rbc-project.json
1. See help on app-tool commands: `app-tools --help`
2. Create a new app project by downloading a project skeleton: `app-tools new-app [APP NAME]` (NOTE: The
optional flag (-t custom | angular) allows the user to pick between a custom project or an angular project. It defaults to custom if none specified.)
3. `cd` into your newly created app directory
4. Develop
4. Move production ready files into /www directory: `cp * www`. This directory is where production ready code will live.
5. Publish your app: `app-tools publish-app`. This command will zip up whatever is in /www and send it to the cloud.
6. Check to make sure your app was uploaded by checking if the cloud has created a record for your app. In your browser go to the following link: [API ENDPOINT]/apps/[APP NAME]
9. Add a profile to your app: `app-tools add-profile [PROFILE]`
9. See the list of profiles your app is associated with: `app-tools list-profiles`
10. View your app in the browser: [API ENDPOINT]/apps/[APP NAME]/index.html (NOTE: you need to be logged in as a user that has the same profile you just assigned to you app.)
11. Make further changes to your app: `vi www/index.html` and change something like the word “Welcome” to “Hi” in line 28.
12. Republish your app: `app-tools publish-app`
13. Refresh your app in the browser. You should be able to see the changes you just made.


