Bodhi-Agent’s Command Line Interface
=====================

The rbc-agent includes a command line interface to perform some basic functions.
This interface is available from a terminal window or command line prompt by calling  >`rbc-agent`.
Command Usage: rbc-agent [options] [command]

Here is the following list of Command Line Interface commands:
#####rbc-agent info -h
**info–** This command will get the information about the agent (e.g. version number, what type of agent it is, etc…)
info [options]
* -h, --help - displays the usage information for the info command

**Command Usage Examples:**
* rbc-agent info –h
* rbc -agent info --help

#####rbc-agent start –h
**start** – This command will start the agent if the agent has not started or has been stopped
start [options]
* -h, --help - displays the usage information for the command
* --config <file> - will attempt to use the fully qualified shared configuration fiile that is provided (e.g. C:\RBC Link\package.json)
* --port <port> - the will start the agent setting the management port for the admin interface
* -v, --verbose – Will run the start command in verbose mode to provide more information

** Command Usage Examples:** 
* rbc-agent start –h
* rbc-agent start --help
* rbc-agent start
* rbc-agent start –-config C:\RBC Link\package.json
* rbc-agent start –-port 4444
* rbc-agent start –v,
* rbc-agent start --verbose

#####rbc-agent stop –h
**stop** - This command will stop a running agent on the system
 stop [options]
* -h, --help - displays the usage information for the command
* -p, --port <port> - the api port
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**
* rbc-agent stop –h
* rbc-agent stop --help
* rbc-agent stop –p 4444
* rbc-agent stop –-port 4444
* rbc-agent stop -v
* rbc-agent stop --verbose

#####rbc-agent status –h
**status**   - This command set the status of a running agent on the system
status [options]
* -h, --help - displays the usage information for the command
* -p, --port <port> - this will get the status of the agent on the specified management port
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**
* rbc-agent status –h
* rbc-agent status --help
* rbc-agent status –p 4444
* rbc-agent status –-port 4444
* rbc-agent status -v
* rbc-agent status --verbose


#####rbc-agent diagnostics –h
**diagnostics** – This command will test the agent’s configuration
diagnostics [options]
* -h, --help - displays the usage information for the command
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**
* rbc-agent diagnostics –h
* rbc-agent diagnostics --help
* rbc-agent diagnostics -v
* rbc-agent diagnostics –verbose

#####rbc-agent check-connection –h
**check-connection** - Test the outbound connection to the cloud
check-connection [options] <scheme>://<host>:<post>
* -h, --help - displays the usage information for the command
* -v, --verbose – Will run the check-connection command in verbose mode to provide more information

**Command Usage Examples:**
* rbc-agent check-connection –h
* rbc-agent check-connection --help
* rbc-agent check-connection http://www.google.com
* rbc-agent check-connection http://www.google.com:5555
* rbc-agent check-connection -v
* rbc-agent check-connection --verbose

#####rbc-agent setup –h
**setup** – This command will launch the setup console
setup [options]
* -h, --help - displays the usage information for the command
* --home <dir> – Will run the setup command using the fully qualified path of the working directory of the agent

**Command Usage Examples:**
* rbc-agent setup –h
* rbc-agent setup --help
* rbc-agent setup –-home C:\RBC Link
* rbc-agent setup -v
* rbc-agent setup --verbose

#####rbc-agent reset –h
**reset** – This command will reset the agent’s identity
[options]
* -h, --help - displays the usage information for the command
* --home <dir> – Will run the reset command using the fully qualified path of the working directory of the agent
* -f, --force - this will force the agent to reset regardless of the state that it is currently in
* -h, --hard - this will reset the agent’s name and namespace
* -v, --verbose – Will run the command in verbose mode to provide more information

**Command Usage Examples:**
* rbc-agent reset –h
* rbc-agent reset --help
* rbc-agent reset –-home C:\RBC Link
* rbc-agent reset –f
* rbc-agent reset –-force
* rbc-agent reset –-h
* rbc-agent reset --hard
* rbc-agent reset -v
* rbc-agent reset --verbose

#####rbc-agent console –h
**console** –This command launches the web management console
[options]
* -h, --help - displays the usage information for the command

**Command Usage Examples:**
* rbc-agent console –h
* rbc-agent console --help
* rbc-agent console

###Management Console
The rbc-agent includes a web management console. This console is available from an internet browser on port 4444 of the local network interface.

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
       
