rbc-cli-tools
=============

Command Line Tools for the RBC Cloud

##Installation

The cli tools require a nodejs runtime and are installed using the node package manager (npm).

````
> npm install -g rbc-cli
````

Not that on *nix based systems and Macs, a global install command MUST be run using sudo.

One the tools are installed, verify the installation using the version command. The command SHOULD respond with a semantic version of the tools: M is the major version, m is the minor version, and b is the build increment.

````
> rbc-cli -V
  M.m.b
````

##General Str

###Common Usage

````
<rbc-tool> [options] <command> [arguments ..]
````
The first entry is the name of the tool. The second argument is the command. All further arguments are interpretted in the context of the command.

Options can be specified anywhere on the command line __AFTER__ the tool designation. The following commands are considered equivalent.

````
rbc-cli -e my-environment -v command
````
````
rbc-cli -v command -e my-environment
````
````
rbc-cli command -v -e my-environment
````

###Processing Options

The following switch are universal and have consistent semantics across the tools.

long    | short | meaning
----    | ----- | -------
version | V     | request the version of a tool
help    | H     | request help in the form of usage instructions
verbose | v     | execute the command with intermediate output
debug   | d     | execute the command in debug mode
force   | f     | force the command to ignore saftey considerations
no-color| C     | do not use color

##Project Commands

* pwd
* init

###pwd

__Aliases__: _home_

This command will print the home directory of the current project.

#####Arguments

None.

#####Return

Platform specific directory path of the current project.

#####Sample

````
> rbc-cli pwd
/path/to/project/root
````

###init

This command will establish the current directory as a new project by creating a new rbc-project.json file. This command will fail safely if an existing rbc-project.json file exists up the directory tree. A user may create a project in a subfolder by using the --force command line option.

````
> rbc-cli init [-f]
/path/to/new/project/root
````

#####Arguments

None.

#####Return

Platform specific directory path to the newly initialized project.

##Environment Commands

### General Command Signature

````
> rbc-cli <action> <environment> [env-options] [processing-options]
````

###Commands

* new
* rename
* copy
* edit
* remove
* set-default
* get-default
* list
* view
* whoami
* whereami
* uri
* user
* namespace

###Environment Options

long      | short | meaning
----      | ----- | -------
uri       | s     | request help in the form of usage instructions
username  | u     | execute the command with intermediate output
password  | p     | execute the command in debug mode
namespace | n     | force the command to ignore saftey considerations

###new

__Aliases__: _create_

This command will create a new environment in the project

#####Arguments

1. environment name - the name of the environment to create

#####Return

The name of the newly created environment

#####Signature

````
> rbc-cli new <env-name> [env-options] [processing-options]
<env-name>
````

###rename

__Aliases__: _mv_, _move_

This command will rename an existing environment and optionally update its configuration if environment options are present.

#####Arguments

1. from - the name of the environment to rename
2. to   - the new name for the environment

#####Return

The new name of the existing environment

#####Signature

````
> rbc-cli rename <from> <to> [env-options] [processing-options]
<env-name>
````

###copy

__Aliases__: _cp_, _clone_

This command will copy an existing environment and optionally update the copy with new setting if environment options are present.

#####Arguments

1. from - the name of the environment to copy
2. to   - the name of the new environment

#####Return

The new name of the newly created environment

#####Signature

````
> rbc-cli copy <from> <to> [env-options] [processing-options]
<from>
````

###edit

__Aliases__: _update_, _modify_

This command changes an exiting environment's settings based on the environment options are supplied.

#####Arguments

1. environment - the name of the environment to change

#####Return

The name of the environment that was modified

#####Signature

````
> rbc-cli edit <environment> [env-options] [processing-options]
<env-name>
````

###remove

__Aliases__: _rm_, _del_

#####Arguments

1. environment - the name of the environment to remove

#####Return

The name of the environment that was removed

#####Signature

````
> rbc-cli remove <environment> [env-options] [processing-options]
<env-name>
````

###set-default

Establish the default environment to use for all remote commands.

#####Arguments

1. environment - the name of the environment to be the default

#####Return

The name of the environment that is now the default

#####Signature

````
> rbc-cli set-default <environment> [processing-options]
<environment>
````

###get-default

Print the default environment for the current project

#####Arguments

None

#####Return

The name of the default environment

#####Signature

````
> rbc-cli get-default <environment> [processing-options]
<environment>
````
###list

__Aliases__: _ls_, _ll_, _dir_

Print the names of a project's environments

#####Arguments

1. environment - the name of the environment to remove

#####Return

A JSON array containing the names

#####Signature

````
> rbc-cli list <environment> [processing-options]
[
  "env",
  "env2"
]
````

###view

__Aliases__: _display_, _print_, _show__

Print the structure of the named enviroment

#####Arguments

1. environment - the name of the environment to remove

#####Return

A JSON object representation of the current environment.

#####Signature

````
> rbc-cli view <environment> [processing-options]
{
  "uri":"uri",
  "user":"user",
  "password":"password",
  "namespace":"namespace",
}
````

###Special Print Commands

The following commands can be used to print/return a specific value of environment configuration.

command  | prints
------   | -------
user     | the name of the user
username | the name of the user
whoami   | the name of the user
whereami | the base uri stem uri + namespace
uri      | the envrionment's base uri
url      | the envrionment's base uri
namespace| the envrionment's namespace
namespace| the envrionment's namespace


#####Signatures

These commands have three possible signatures

Preferred

````
> rbc-cli <cmd> <environment> [processing-options]
````

Acceptable

````
> rbc-cli <cmd> -e <environment-name>
````

Default (uses the default environment if set)

````
> rbc-cli cmd
````

