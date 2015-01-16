Building mobile apps
=====================

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

## Contract
* html file must be called index.html. It must reside in the root of the app folder.
* If you want to include an app icon for the menu screen,
 icon.* must be located at the root of the app folder.

 Please see [rbc-cli.md](./rbc-cli.md) for information on app-tools commands.