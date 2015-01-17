Extending the Agent
===========

Concept
--------
An Extension is an Object that adds on configuration elements to the agent or an application in the form of plugins.

Plugin
A plugin is an Object.  In reality, it is a namespaced set of functions used to instantiated runtime components (Service, Source, Pipeline, etc)
Capability
A capability is a Function. This type of extension is intended to be the moral equivalent of a static function. It should encapsulate globally aware stateless behavior that can be injected into a runtime component.
A capability SHOULD have no awareness of the container, configuration providers, or runtime components.
It receives all its state as input and loses the state when it returns.
A capability should be added to an app by an extension during the attach function.
Model
Specification
Applications can load application specific extensions in order.

Specification
-----------
````
extensions: [     
  { module : 'file1', options : {enabled : true}},
],
````
###Module Id

 * module  => resolves using the node module algorithm
 * file    => expects a path to point at a JS file that exports a proper module, the root directory of a CommonJS package (the directory containing the package.json

Specification Rules
* module and file extensions are mutually exclusive
* When a module is declared then the system will invoke the function that returns an object
When an extension is declared then the system expects to receive an object 
Options are not resolved so they cannot include references.
Resolution Rules
* Modules are resolved relative to the containers home
* A Module is assumed to be a Javascript file with a .js extension. 
* A module MAY include the JS extension, but if not then the extension is assumed
* A module that does not end in .js MUST include the extension

###Options

A plugin may receive options at attachment time. Options provide a means for declaring environment specific configuration data to the extension. 

Implementation
---------


Prototypical Extension
````
module.exports = {
	
	name    : 'my-extension',
	version : 'major.minor.patch',
	provider: 'my organization',
 
	attach: function(options, callback){
	
		var container = this;
 
    container.registerPlugin(namespace, )
    container.registerPlugin([ns, ns, ns], object)
 
		if(error){
			callback(err)
		} else {
			callback()
		}
    }	
}
````

Prototypical Extension Module

````
module.extension = function(){
	return {
		... prototypical extension
	}
}
````

attach(options, function(err))
The attach method is intended to add configuration elements to the system - (default/safe) settings, plugins, and capabilities. 
init(function(err))
The init method is called after all extensions have attached to the app. It is the preferred place to add event listeners to the application or programmatically add runtime elements to an application.
detach(function(err))
The detach method is used to clean up event handlers the extension may have registered.
Events
An extension can add event handlers to the app event bus. 
Wiring 
Load the extension
Attach Configuration Elements
Initialized Runtime Elements
