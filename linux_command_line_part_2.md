# The Linux Command Line - A Complete Introduction - William Shotts, 2nd Edition

## Part 2. Configuration and Environment***

### The Environment

#### What is stored in the Environment? 

The shell stores two basic types of information in the environments: 

+ environment variables

+ shell variables

**Note:** with bash it's hard to distinguish between above. 

In addition to variables, shell stores, some programmatic data:

+ aliases

+ shell functions

##### Examining the environment

`set` builtin bash command to show both shell and environment variables

`printenv` will display only environment variables

**Note:** both best viewed when pipelined to less. 

`printenv USER` will print only the value of corresponding env. variable

`echo $USER` will print the value of corresponding env. variable. Not seem to be working for shell variables. 

`alias` this will show the configured aliases (not visible with `set`/`printenv` commands)

#### How is the environment established

When we log on to the system: 

+ bash program starts

+ bash reads a series of configuration scripts called startup files (common to all users)

+ bash reads startup files under user directory - that are user specific

+ the exact sequence depends on the kind of the shell session used. 

**Note:** This is for log on only - when the computer boots bash doesn't have any role. 

There are 2 kinds of shell sessions. 

+ a login shell session - typically it will prompt username/password etc.

+ a non-login shell - when a new terminal is opened etc. 

**startup files for login shells**

`/etc/profile` - global configuration script, applies to all users

`~/.bash_profile` - a user's personal startup file, may extent/override global configuration script settings. 

`~/.bash_login` - is read when .bash_profile script is missing

`~/.profile` - if above 2 are missing, this file is read. 

**startup files for non-login shells**

**Note:** in addition to below, non-login shells inherit startup files from login shells (their parent process) as well

`/etc/bash.bashrc` global

`~/.bashrc` users personal startup file, may extent/override global configuration script settings. 

**Note:** `~/.bashrc` is the most important one, and almost always it's indirectly read by login shell as well

##### What is a startup file

**Note:** As I understood it, and as chat gpt3 pointed out - below can be a pseudo correct summary of relationship between startup scripts and variables: 

+ default env variables are initialized by system (bash + environment variables)

+ application env variables are managed by corresponding applications

+ user specific env variables can be added to startup scripts. 

+ startup scripts are able to dynamically assign/modify variables @ startup. 

#### Modifying the environment









