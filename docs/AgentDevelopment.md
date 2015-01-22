Agent Development
=====================

# Getting Started

# How to Guides
## Agent CLI Tool

## Extending the Agent
Concept
--------
An Extension is an Object that adds on reusable configuration elements. These configuration elements are call plugins. An extension may provide one or more plugins to the agent or an application. Plugins are used to build runtime components (Sources, Services, Pipelines, Handlers, etc). Extensions are meant to be small reusable chuncks of code that follow in the tradition of Node Modules but conform to a specific interface so they can be loaded by node.js an the agent.

Specification
-----------

An extension must be formally specified in an app or agent configuration file.

###Spec Rules
* An Extension specification MUST include a module or a file key
* A module and file attributes are mutually exclusive
* An Extension specification MAY include (configuration) options
* 

````
extensions: [     
  { module : 'module-id', options : {enabled : true, silent: true}},
  { file   : './path/to/file', options : {env : debug}},
],
````
__Notes on the module id__

Module and file really do the same thing. They are both included for semantic reasons. In general, they are used as follows:

 * module indicates this is a packaged module resolves using the node module algorithm living (most likely) in the node_modules folder of the agent or app directory.
 * file points at a at a JS file that exports a proper extension interface, the root directory of a CommonJS package (the directory containing the package.json

###Options

An extension may receive options at attachment time. Options provide a means for declaring environment specific configuration data to the extension. 

__Note__: Options are not resolved so they SHOULD NOT include references.

###Resolution Rules

* A file path is resolved relative to the specifying containers home directory
* A module or file path that points at a CommonJS package will use the main file or index.js as the extension entry point

For complete detailed information check out the [nodejs docs](http://nodejs.org/api/modules.html) 

###Visibility Rules

* If the extension is loaded by the agent then the agent and all applications can use the extensions plugins. 
* If the extension is declared by the app then only the app can use the extension's plugins.
* If the extension is declared by both the app and the agent the app will use the plugins provided by the extension declared by the app.

Implementation
---------

* An Extension MUST declare a name
* An Extension SHOULD declare a version
* An Extension MAY declare a description
* An Extension MAY declare a provider
* An Extension MUST be either and object of a function that produces an object
* An Extension MUST expose a method named attach that takes a call callback

####Prototypical Extension

````
module.exports = {
	
	name    : 'my-extension',
	version : 'major.minor.patch',
	provider: 'my organization',
 
	attach: function(options, callback){
        }	
}
````

####Prototypical Extension Module

````
module.extension = function(){
        'use strict';
	return {
		... prototypical extension
	}
}
````

###Binding Mechanism

The attach method adds plugins to a particular container

####Attach Signature

````
attach(options, function(err))
````

argument | type     | required | description
-------- | ------   | ---------| -----------
options  | object   | optional | provides the env specific configurations
callback | function | required | provides a way of returning an runtime error to the container

Callback takes the form of cb(err). The callback MUST be called.

####Context

The value of `this` provides the mechanism for adding plugins to the container. `this` provides the following binding method:

````
this.registerPlugin(namespace, plugin)
`````

argument | type               | required | description
-------- | ------             | ---------| -----------
namespace| string, array      | required | unique naming
plugin   | object or function | required | provides a way of returning an runtime error to the container

####Prototypical Attachment

````
   attach: function(options, callback){
	var container = this;
	try{
             container.registerPlugin(namespace, object)
       	     container.registerPlugin([ns, ns, ns], object)
       	     callback && callback()
	} catch (err){
	     callback && callback(err)
	}
   }	
````

## Agent Integration

Agent Development
=====================

# Getting Started

# Agent CLI Tools

The agent cli provides administrators, support team members, and developers a tool for interacting with an agent.

##Installation

The agent cli is installed via a platform specific installer or via node package manager (NPM). The cli prefers to be installed globally.

````
$> npm install -g agent-cli
````

##General Usage

The general structure of any agent command is as follows:

````
$> npm install agent-cli [options] <action> [arguments]
````

###Options

Options are prefixed with `-` or `--` to separate them from arguments. Each action defines the options it uses, but the options are consistent in naming and usage across the commands.

####Common Options

long | short | arg    | description
------| --------- | ------ | -------------
--help | none | none   | print help about the command
--verbose | -v | none   | print more detailed output
--quiet   | -q   | none   | print essential output
--config  | -f  | path   | specifies the agent's configuration file
--home    | -h    | path   | specifies the agent's working directory
--force   | -F   | none   | directive to override safety logic

###Arguments
The cli interprets the first argument (non-option) as the action. All subseuqent arguements are command specific. 


Each action is described below.


##Informational Commands

###help

The command line provides built in helper functions.

####Navigation Help
For a descriptive list of the commands 

````
$> npm install agent-cli --help
````

####Action Specific Help

Action specific help can be requested using the following structure.

````
$> npm install agent-cli <action> --help
````

###version

Print version information.

````
$> agent-cli --version 
$> agent-cli -V
````
The output is a simple version identifier following the semantic versioning rules of major, minor, and build.

````
vM.m.b
````

###info

CLI splash screen for the agent.

````
$> agent-cli info
````

##Lifecycle Commands

Lifecycle commands allow an administrator to change and check the run state of an agent.

###start

Attempts to start an agent.

````
$> agent-cli start [options] 
````

####Options

long | short | arg    | deacription
------| --------- | ------ | -------------
--verbose | -v   | none   | print more detailed output
--quiet   | -q   | none   | print essential output
--config  | -f   | path   | specifies the agent's configuration file
--home    | -h   | path   | specifies the agent's working directory


###status

Provides status about a running agent.

````
$> agent-cli status [options] 
````

####Options

long | short | arg    | deacription
------| --------- | ------ | -------------
--verbose | -v   | none   | print more detailed output
--quiet   | -q   | none   | print essential output
--config  | -f   | path   | specifies the agent's configuration file

###stop

Gracefully shutdown the agent.

````
$> agent-cli stop [options] 
````

####Options

long | short | arg    | deacription
------| --------- | ------ | -------------
--verbose | -v   | none   | print more detailed output
--quiet   | -q   | none   | print essential output
--config  | -f   | path   | specifies the agent's configuration file

##Diagnostic Commands

Diagnostic commands are used by an admin to troubleshoot an agent having trouble entering a running state or to test environmental specific details uniformly across platforms.

###check-core

Used to check the version of agent-core being used and where that file is located on the file system.

````
$> agent-cli check-core [options]
````

####Options

long | short | arg    | deacription
------| --------- | ------ | -------------
--config    | -f   | path   | specifies the agent's configuration file

###check-config

Used to check for configuration problems in the agent. The agent will load and process all configuration files, but will not enter into a ready state. This command is safe to run even if there is a currently running agent.

````
$> agent-cli check-cofig [options]
````

####Options

long | short | arg    | deacription
------| --------- | ------ | -------------
--config    | -f   | path   | specifies the agent's configuration file

###check-connection

Used to check for configuration problems in the agent.

````
$> agent-cli check-connection [options]
````
####Options

long | short | arg    | deacription
------| --------- | ------ | -------------
--config    | -f   | path   | specifies the agent's configuration file


The provided URL will go through the following checks:

1. Check the URL format
2. Check the DNS resolution from the agent's host
3. Check the TCP port is reachable by opening up a connection on host:port
4. Issue a HTTP GET against the ping endpoint of the system

###check-route

Used to check for network problems (firewalls & proxy rules) from the perspective of the agent runtime. 

````
$> agent-cli check-route <scheme://host:port/path>
````

The provided URL will go through the following checks:

1. Parse
2. DNS resolve of host/IP
3. TCP port reachable by opening up a connection on host:port
4. If scheme is http of https then issue a HTTP GET against the specified URL


##Usage Commands

###console

````
$> agent-cli console
````

##Configuration Commands

###reset

A reset command is used to reset the agent's state.

````
$> agent-cli reset
````

long | short | arg    | deacription
------| --------- | ------ | -------------
--home    | -h   | path   | specifies the agent's working directory
--HARD    | -H   | path   | destroy all state

###revoke

````
$> agent-cli revoke
````

A revoke command will revoke the agent's access token but leave all other agent data intact.


# How To Extend The Agent
##Concept

An Extension is an Object that adds on reusable configuration elements. These configuration elements are call plugins. An extension may provide one or more plugins to the agent or an application. Plugins are used to build runtime components (Sources, Services, Pipelines, Handlers, etc). Extensions are meant to be small reusable chuncks of code that follow in the tradition of Node Modules but conform to a specific interface so they can be loaded by node.js an the agent.

##Specification

An extension must be formally specified in an app or agent configuration file.

###Spec Rules
* An Extension specification MUST include a module or a file key
* A module and file attributes are mutually exclusive
* An Extension specification MAY include (configuration) options
* 

````
extensions: [     
  { module : 'module-id', options : {enabled : true, silent: true}},
  { file   : './path/to/file', options : {env : debug}},
],
````
__Notes on the module id__

Module and file really do the same thing. They are both included for semantic reasons. In general, they are used as follows:

 * module indicates this is a packaged module resolves using the node module algorithm living (most likely) in the node_modules folder of the agent or app directory.
 * file points at a at a JS file that exports a proper extension interface, the root directory of a CommonJS package (the directory containing the package.json

###Options

An extension may receive options at attachment time. Options provide a means for declaring environment specific configuration data to the extension. 

__Note__: Options are not resolved so they SHOULD NOT include references.

###Resolution Rules

* A file path is resolved relative to the specifying containers home directory
* A module or file path that points at a CommonJS package will use the main file or index.js as the extension entry point

For complete detailed information check out the [nodejs docs](http://nodejs.org/api/modules.html) 

###Visibility Rules

* If the extension is loaded by the agent then the agent and all applications can use the extensions plugins. 
* If the extension is declared by the app then only the app can use the extension's plugins.
* If the extension is declared by both the app and the agent the app will use the plugins provided by the extension declared by the app.

###Implementation

* An Extension MUST declare a name
* An Extension SHOULD declare a version
* An Extension MAY declare a description
* An Extension MAY declare a provider
* An Extension MUST be either and object of a function that produces an object
* An Extension MUST expose a method named attach that takes a call callback

###Prototypical Extension

````
module.exports = {
	
	name    : 'my-extension',
	version : 'major.minor.patch',
	provider: 'my organization',
 
	attach: function(options, callback){
        }	
}
````

###Prototypical Extension Module

````
module.extension = function(){
        'use strict';
	return {
		... prototypical extension
	}
}
````

##Binding Mechanism

The attach method adds plugins to a particular container

###Attach Signature

````
attach(options, function(err))
````

argument | type     | required | description
-------- | ------   | ---------| -----------
options  | object   | optional | provides the env specific configurations
callback | function | required | provides a way of returning an runtime error to the container

Callback takes the form of cb(err). The callback MUST be called.

###Context

The value of `this` provides the mechanism for adding plugins to the container. `this` provides the following binding method:

````
this.registerPlugin(namespace, plugin)
`````

argument | type               | required | description
-------- | ------             | ---------| -----------
namespace| string, array      | required | unique naming
plugin   | object or function | required | provides a way of returning an runtime error to the container

###Prototypical Attachment

````
   attach: function(options, callback){
	var container = this;
	try{
             container.registerPlugin(namespace, object)
       	     container.registerPlugin([ns, ns, ns], object)
       	     callback && callback()
	} catch (err){
	     callback && callback(err)
	}
   }	
````


# Creating Agent Apps
##Agent App Structure

You can create an application for the agent by following the steps below. 

###App Structure

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

###Starting Structure
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

####Descriptive Info
This contains identification information for your app.

#####Sample
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


####Logger Info

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


####Settings
Your app can optionally contain a settings object. These values have the highest precedence in processing the settings.

#####Sample
````
[ {property: 'keys:consumerKey', value: 'wWbo8MBQ0nQ' }]
````

Property | Type | Required | Description | 
------| --------- | ------ | -------------
property | string | Yes   | Your name for your property| 
value | string, function, Boolean, number, object | Yes	   | The value of your setting

