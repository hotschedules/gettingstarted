Agent CLI
===========

The agent cli provides administrators, support team members, and developers a tool for interacting with an agent.

##Installation

The agent cli is installed via a platform specific installer or via node package manager (NPM). The cli prefers to be installed globally.

````
$> npm install -g agent-cli
````

##General Usage

The general structure of the a command is as follows:

````
$> npm install agent-cli [options] <action> [arguments]
````

###Options

Options are prefixed with `-` or `--` to separate them from arguments. Each action defines the options it uses, but the options are consistent in naming and usage across the commands.

####Common Options

long | short | arg    | deacription
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
