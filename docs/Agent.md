Bodhi-Agent’s Command Line Interface
=====================

The agent-cli includes a command line interface to perform some basic functions.
This interface is available from a terminal window or command line prompt by calling  >`agent-cli`.
Command Usage: agent-cli [options] [command]

Here is the following list of Command Line Interface commands:
#####Info
	agent-cli info
   
**info–** This command will get the information about the agent (e.g. version number, what type of agent it is, etc…)
info [options]

* -h, --help - displays the usage information for the info command

**Command Usage Examples:**

	agent-cli info –h
	agent-cli info --help

#####Start

	agent-cli start -h
	
**start** – This command will start the agent if the agent has not started or has been stopped

start [options]

* -h, --help - displays the usage information for the command
* --config <file> - will attempt to use the fully qualified shared configuration fiile that is provided (e.g. C:\RBC Link\package.json)
* --port <port> - the will start the agent setting the management port for the admin interface
* -v, --verbose – Will run the start command in verbose mode to provide more information

**Command Usage Examples:** 

	agent-cli start –h
	agent-cli start --help
	agent-cli start
	agent-cli start –-config C:\RBC Link\package.json
	agent-cli start –-port 4444
	agent-cli start –v,
	agent-cli start --verbose

#####Stop

	agent-cli stop –h

**stop** - This command will stop a running agent on the system

stop [options]
* -h, --help - displays the usage information for the command
* -p, --port <port> - the api port
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**

	agent-cli stop –h
	agent-cli stop --help
	agent-cli stop –p 4444
	agent-cli stop –-port 4444
	agent-cli stop -v
	agent-cli stop --verbose

#####Status
	
	agent-cli status –h

**status**   - This command set the status of a running agent on the system
status [options]

* -h, --help - displays the usage information for the command
* -p, --port <port> - this will get the status of the agent on the specified management port
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**

	agent-cli status –h
	agent-cli status --help
	agent-cli status –p 4444
	agent-cli status –-port 4444
	agent-cli status -v
	agent-cli status --verbose


#####Diagnostics
	
	agent-cli diagnostics –h

**diagnostics** – This command will test the agent’s configuration
diagnostics [options]

* -h, --help - displays the usage information for the command
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**

	agent-cli diagnostics –h
	agent-cli diagnostics --help
	agent-cli diagnostics -v
	agent-cli diagnostics –verbose

#####Check-Connection
	
	agent-cli check-connection –h

**check-connection** - Test the outbound connection to the cloud
check-connection [options] <scheme>://<host>:<post>

* -h, --help - displays the usage information for the command
* -v, --verbose – Will run the check-connection command in verbose mode to provide more information

**Command Usage Examples:**

	agent-cli check-connection –h
	agent-cli check-connection --help
	agent-cli check-connection http://www.google.com
	agent-cli check-connection http://www.google.com:5555
	agent-cli check-connection -v
	agent-cli check-connection --verbose

#####Setup
	
	agent-cli setup –h

**setup** – This command will launch the setup console
setup [options]

* -h, --help - displays the usage information for the command
* --home <dir> – Will run the setup command using the fully qualified path of the working directory of the agent

**Command Usage Examples:**

	agent-cli setup –h
	agent-cli setup --help
	agent-cli setup –-home C:\RBC Link
	agent-cli setup -v
	agent-cli setup --verbose

#####Reset
	
	agent-cli reset –h

**reset** – This command will reset the agent’s identity
[options]

* -h, --help - displays the usage information for the command
* --home <dir> – Will run the reset command using the fully qualified path of the working directory of the agent
* -f, --force - this will force the agent to reset regardless of the state that it is currently in
* -h, --hard - this will reset the agent’s name and namespace
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**

	agent-cli reset –h
	agent-cli reset --help
	agent-cli reset –-home C:\RBC Link
	agent-cli reset –f
	agent-cli reset –-force
	agent-cli reset –-h
	agent-cli reset --hard
	agent-cli reset -v
	agent-cli reset --verbose

#####Console
	
	agent-cli console –h

**console** –This command launches the web management console
[options]

* -h, --help - displays the usage information for the command

**Command Usage Examples:**

	agent-cli console –h
	agent-cli console --help
	agent-cli console

###Management Console
The agent-cli includes a web management console. This console is available from an internet browser on port 4444 of the local network interface.

[http://localhost:4444](http://localhost:4444)    -- or --    [http://127.0.0.1:4444](http://127.0.0.1:4444)

The management console provides three distinct applications:

1. The Setup Wizard
2. The Configuration & Monitoring Console
3. A Restful API
 
Usage: [http://127.0.0.1:4444/<app>](http://127.0.0.1:4444/<app>)

   Applications:
   
   [http://127.0.0.1:4444/setup](http://127.0.0.1:4444/setup)
   
       provide the initial configuration
       
   [http://127.0.0.1:4444/console](http://127.0.0.1:4444/console)
    
       Get the status of a running agent
       
   [http://127.0.0.1:4444/api](http://127.0.0.1:4444/api)
   
       Get the status of a running agent
       
