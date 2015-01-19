Agent App Structure
===========

You can create an application for the agent by following the steps below. 

##App Structure

Apps have 9 major categories:

* Descriptive Information
* Logger Settings
* App Settings
* Extensions
* Services
* Sources
* Pipelines
* Handlers
* The init function

These categories are described below. 

##Starting Structure
1. Create a file called app.js.
2. Insert the following code into the app.js file.

````
  //- Descriptive Information
  name   : 'app-name',
  version: '0.0.1',
  
  //- Logger Settings
  logger : {
    filename: 'logger-filename.log',
    level   : '' // The level of logging for the app
  },
  
  //- App Settings
  settings: [
    {property  : '',
     value     : ''},
  ],
  
  //- Extensions
  extensions: [
    {file      : ''}
  ],
  
  //- Services
  services: [
  	{
  	 name     : '',
  	 provider : '',
  	} 
  ],

  //- Sources
  sources: [
    { 
    name   : '',
    factory: '',
    provider: {
        bind: '',
        listen : '',
        close  : ''
      },
      bindings: {'eventName'}
    }
  ],
  
  //- Pipelines
  pipelines: [
    {
      name: 'name-of-pipeline',
      subscriptions: ['name-of-event-that-the-pipeline-subscribes-to'],
      steps: [
        {fn: 'extension:name-of-function', props: {key: 'value'},
        {fn: 'extension:name-of-function', props: {key: 'value'},
      ]
    }
  ],

  //- Handlers
  handlers: [
  	name: 'name-of-handler',
  	subscriptions: 'name-of-event-the-handler-subscribes-to',
  	fn: '',
  	props: { name: '$key:value' }

  ],

  //- init function, this function is executed after the agent is done with setup
  init: function(done) {
    // statements here
    done();
  }
  
}
````

###Descriptive Info
This contains identification information for your app.

####Sample
````
  name   : 'app-name',
  version: '0.0.1',
  dir    : '',
  enabled: 

````

Property | Type | Required |   Description | 
------| --------- | ------ | -------------
name | string | Yes   | Your name for the application | 
version | string | Yes	   | The version number for the application
dir | string | Yes | Root filesystem path for the application
enabled | Boolean | Preferred | Whether the app is enabled or not
provider | string | Preferred | Your organization's name


###Logger Info

These properties determine the log filename and amount of detail that would be recorded to the log file. 

The levels of logging are as follows, listed from the least amount of detail to the most.

1. error
2. warning
3. info
4. verbose
5. debug

Note: The logger cannot include a reference to the settings, since it is loaded prior to the settings.

Property | Type | Required | Description | 
------| --------- | ------ | -------------
level | string | Yes   | Your name for the application | 
version | string | Yes	   | The version number for the application


###Settings
Your app can optionally contain a settings object. These values have the highest precedence in processing the settings.

####Sample
````
[ {property: 'keys:consumerKey', value: 'wWbo8MBQ0nQ' }]
````

Property | Type | Required | Description | 
------| --------- | ------ | -------------
property | string | Yes   | Your name for your property| 
value | string, function, Boolean, number, object | Yes	   | The value of your setting