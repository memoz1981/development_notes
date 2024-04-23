# The Linux Command Line - A Complete Introduction - William Shotts, 2nd Edition

## Part 2. Configuration and Environment***

### 11. The Environment

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

##### Which files should we modify

+ If the changes are applicable to a user only, then it would be safe to add those under user directory files. This is SAFE approach to take. (i.e. under `~/.profile`, `~/.bashrc` etc.) 

+ If PATH variable is being modified and/or if a new environment setting is being introduced and/or you are system admin and want to change all user settings, then variables can be added globally (`/etc/profile` or `/etc/bash.bashrc`)

##### Text editors - just tools to perform the changes

Fall under 2 main categories: 

+ Graphical (GNOME and KDE both come with GUI text editors)

+ Text based (nano, vi and emacs)

**Note:** On most Linux systems vi is replaced by vim (vi improved)

`text_editor_program_name file_name` should open the file in corresponding text editor

`nano ~/.bashrc` will open the file in nano editor - after changes are applied...

`source ~/.bashrc` will force bash to re-read the modified file. Same could be achieved by closing and re-opening the terminal. (Actually in my case changes worked straightaway :) 

### 12. A gentle introduction to VI

#### Introduction to vi

**Note:**vi - pronounced "vee eye". comes from word visual as previous editors were line based, and only one line could be edited at a time. 

Note that by default vi compatibility mode is opened. To have vim opened (with improved functionality) when typing vi, below 2 ways can be followed:

+ add `vi='vim'` to .bashrc file

+ `echo "set nocp" << ~/.vimrc` command should do the work (don't ask how)

`vi foo.txt` either will open foo.txt or if it doesn't exist will create and open

**Note:** if no changes done to the file and/or force quit is used without any changes to file - file will not be created... 

#### Modes

**Note:** vi is a modal editor - it starts in `command mode` - every key is a command. 

`i` to switch to insert mode 

`ESC` will exit from insert mode. 

`:` ex command

`:w` will save the document (in command mode)

`:q` quit the editor

`:q!` force quit (will ignore the changes)

**Note:** vim documents refers to command mode as normal mode, and ex commands are called command mode.

#### Moving the cursor around

Similar to less. (while in command mode) 

`0` to the beginning of current line

`^` first non-space char on current line

`$` to the end of current line

`w` to the beginning of next word or punctuation chars

`W` similar to above, ignores punctuation chars

`b` to the beginning of previous word or punctuation chars

`B` similar to above, ignores punctuation chars

`xG` to the xth line

`G` to the last line

#### Basic Editing

`u` in command mode will undo last action (vi supports limited undo)






















