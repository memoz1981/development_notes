# The Linux Command Line - A Complete Introduction - William Shotts, 2nd Edition

## Part 1. Learning the Shell

### 1. What is Shell? 

- Bash - From GNU project. Bourne-again-shell (after UNIX shell author Steve Bourne)
- Terminal Operators - to interact with the shell

### 2. Navigating

`pwd` - print current directory name

`cd` - change directory

**some_examples**:

`cd` change to home directory

`cd ~` change to home directory

`cd ~user` change to home directory of a user

### 3. Exploring the system

`ls` list content of the directory

`file` determine file type. file name extension in linux are not indicative. use this command to determine the file type. in unix like systems -> everything is a file. 

`less` view text file contents. developed as an improvement to unix tool more and stands for "less is more"

**some_examples**:

`ls -ltr` -l option: long format output, -t option: sort according to time, -r option: reverse sorting

`file picture.jpeg` will output the type of the file (perhaps based on the metadata)

`less /etc/passwd` display the contents of the file /etc/passwd

### 4. Manipulating files and directories

#### Commands

`cp` copy files (and since directories are files this also applies to the directories)

`mv` both for moving and renaming files (and again for directories) 

`mkdir` create directory

`rm` remove files (and directories)

`ln` create hard and symbolic links

#### Wildcards

Note that all of above commands are possible with GUI - on the other hand wildcards add more usability to command line and make some tasks easier than GUI.

`*` matches any characters

`?` matches any single characters

`[characters]` matches any character that's a member of the set characters

`[!characters]` matches any characters that's NOT a member of the set characters

`[[:class:]]` matches any character that is a member of the class

**Commonly used classes**

`[:alnum:]` alphanumeric character

`[:alpha:]` alphabetic character

`[:digit:]` numeral

`[:lower:]` lowercase letter

`[:upper:]` uppercase letter

**Wildcard examples**

`*` all files

`g*` any file beginning with g

`data???` any file beginning with data followed by exactly three characters

`[abc]*` any file beginning with a, b or c

`[!abc]*` any file not beginning with a, b, c

`*[[:lower:]123]` any file ending with lowercase letter or 1 or 2 or 3

**Command Examples**

`mkdir dir1, dir2` will create dir1 and dir2 directories

`cp file1 file2` will overwrite file2 contents from file1. if file2 doesn't exist it's created.

`cp -i file1 file2` same as above, only if file2 exists user is prompted to overwrite.  

`cp file1,file2 dir` file1 and file2 are copied to dir

`cp dir1/* dir2` wildcard used to copy all contents of dir1 to dir2

`cp -3 dir1 dir2` recursively copy contents or create if doesn't exist. 

`mv file1 file2` if file2 exists it's move, if not it's rename operation

`mv file1, file2 dir` actually mv is very similar to cp except for now original is not kept

`rm file1` remove file1 silently

`rm file1 -i` remove file1 with user prompt

`rm -r file1, dir1` delete file1 and dir1 and all of it's contents. -r is required since it's a dir. 

`rm -rf file1 dir1` -f (force) to ignore non-existent files/folders

#### Hard and Symbolic Links (ln command)

There are 2 types of links: 

+ hard links - are original unix way. every file has a hard link to file name. 

+ symbolic links - are just a text pointer to the file. are more modern way. can be used both with files or directories. (similar to windows shortcut). 

`ln file link` will create a hard link

`ln -s file link` will create a symbolic link

### 5. Working with Commands

`type command` will show the type of the command (like shell built int, executable etc. )

`which executable` only for executables. will display the executable file location. 

`help` get help for shell built-ins

`--help` display help page for executables

`man` display a command's manual page

`apropos` display list of appropriate commands. will search for term in man pages. 

`info` display a commands info entry - this is GNU project alternative to man. 

`whatis` display one-line manual page descriptions

`alias` create an alias for a command

#### What are commands? 

+ en executable program

+ a command built into the shell (shell builtins)

+ a shell function

+ an alias  

##### Command notation

+ square brackets: optional items

+ vertical bar: mutually exclusive items (one or other)

+ `cd [-L|[-P[-e]]] [dir]`: cd command can be followed by either -L or -P, and if -P used -e can also be used. dir name is optional. 

**examples**

`type type` output: *type is a shell builtin* 

`which ls` output: */usr/bin/ls*

`which type` no output as type is builtin. which can only be used with executables. 

`help type` will display the shell help page for type builtin command

`ls --help` display help for ls executable

`man ls` display manual for ls executable using program man

`apropos partition` will display file name and section from man - same with man -k option 

`whatis ls` - will display man page title and name for ls command

`info ls` - similar to above, just from GNU project. 

`alias` will list all the set aliases

`unalias name` will remove the alias with name name

`alias foo='cd /user; ls; cd'` will create an alias named foo with corresponding action

### 6. I/O Redirection

`cat` concatenate files

`sort` sort lines of text

`uniq` report/omit repeated lines

`grep` print lines matching a pattern

`wc` print newline, word and byte counts for a file

`head` output the first part of a file

`tail` output the last part of a file

`tee` read from standard input and write to standard output and files

#### Standard Input, Output, Error

In unix like system - everything is a file - thus std input, output, and error also act like a file. By default both std output and std error are linked to the display and std input is linked to the keyboard. Those can be re-directed. 

The shell references those as numbered file streams as below: 

+ standard input 0

+ standard output 1

+ standard error 2

**examples**

`ls -l /usr/bin > trucated-out.txt` redirects the output of command `ls -l /usr/bin` to txt file rather than the screen and file is truncated before writing. Note std error is still re-directed to the standard output. if file doesn't exist an error will be displayed.

`ls -l /usr/bin >> appended-out.txt` redirects the output of command `ls -l /usr/bin` to txt file rather than the screen and appends to file (previous text will be kept). Note std error is still re-directed to the standard output. if file doesn't exist an error will be displayed.

`>out.txt` will generate an empty text file. if file exist it will be truncated. 

`>>out.txt` similar to above, but this time if file exists - it's contents will not be lost. 

`ls -l /usr/bin 2>out-error.txt` redirects standard error to output specified truncating the file

`ls -l /notexistingdir/ 2>>out-error.txt` similar to above, but appends rather than truncating

`ls l /usr/bin >out.txt 2>&1` redirects standard output and standard error to out.txt (truncating). It's possible to truncate one and append other. Also it's possible to replace ">" with "1>". Also it's possible for both to show the file name. 

`>/dev/null` it's a bit bucket in UNIX system. basically related output is ignored. 

**cat**

`cat out.txt` will show the content of out.txt without pagination. 

`cat out*.txt >outcombined.txt` will combine all files starting with out in a single file (it will do in ascending order by default)

`cat` will accept text and copy everything written to std output. press Ctrl + D for EOF

`cat >out.txt` will do same as above - this time redirected to txt file

`cat <out.txt` reverse of above - this time will read from out.txt as standard input and provide to standard output. 

`cat <out.txt >out2.txt` standard input is redirected from out.txt and standard output is redirected to out2.txt. basically writes from out.txt to out2.txt

#### Pipelines

`command1 | command2` standard output from command1 is "piped" into standard input for command2

**filters** cascaded pipelines

`ls /bin /usr/bin | sort | less` since there are 2 directories specified, sort will sort combined list and produce one sorted list, which will then be displayed using less. 

**difference between > and |** these CANNOT be used interchangeably

`command >file` command to file

`command1 | command2` command to command

**uniq** removes duplicates

`ls /bin /usr/bin | sort | uniq | less` similar to above, with duplicates removed

**grep pattern filename** print (std out) lines matching a pattern. pattern can be simple text or regular expressions. (-i to ignore case, -v to show not matching)

`grep ory Readme.md` will display the line containing string "ory"

`ls /bin /usr/bin | grep zip` will display all the files under directories whose name contains zip

**head/tail** to print (std out) only specified head/tail lines. by default they print first or last 10 lines, which can be overriden using -l lineCount. 

`head out.txt` will print (std out) first 10 lines

`head -l 20 out.txt` 20 lines this time

`ls /bin /usr/bin | sort | tail -l 20` will print last 20 sorted alphabetically

**`tail -f /var/log/messages` allows to monitor logs realtime (since logs are appended). Ctrl+C to exit**

**tee** with plumbing in mind (pipelines), tee is an intermediate connector. 

`ls /usr/bin | tee out.txt | sort` the output of ls command will be passed to both std in of sort as well as specified txt file. 

### 7. Seeing the world as shell sees it

Expansion and quoting are explained under this section. 

`echo` display a line of text

#### Expansion

Commands are "expanded" before shell acts upon it. Good example is wildcards. 

`echo *` would print the files in current directory, i.e. * in this case is expanded to files under current directory. **(note it will NOT display hidden files)**

**pathname expansion** This is the mechanism by which wildcards work. 

`echo [[:upper:]]*` will display any files starting with uppercase character 

`echo /usr/*/share` will display all matching directory names (which are also files in UNIX like systems) - note that "/" characters are important when using wildcards for directories - as the names of the directories are not just text... 

**tilde expansion** home directory of a user (if user not specified current user)

`cd ~foo` expands to `cd /home/foo`

**aithmetic expansion** shell allows arithmetic to be performed by expansion, thus shell can be used as a calculator. `$((expression))` will be evaluated by arithmetic expansion.  

`echo 2 plus 2 makes $((2+2))` output: 2 plus 2 makes 4

**brace expansion** probably coolest expansion. basically anything in braces {..} is evaluated. can have comma sep lists or .. for ranges.

`echo front-{A,B,C}-back` will output front-A-back front-B-back front-C-back

`echo {1..12}-{2020..2024}` will output all months-years between 2020 and 2024 

`echo {Z-A}` guess...

**parameter expansion** ability to store and use small amount of variables. environmental variables are an example to this. Will be covered under scripting expensively. 

`echo $USER` will display user

`printenv | sort | less` will print env. variables sorted alphabetically

**command substitution** will substitute output of one command and pass to other. $(command) will expand to the output of the command. (in older shell programs \`command\` would do same)

`file $(ls -d /usr/bin/* | grep zip)` file command will be applied to all files of the output of the pipeline filter

#### Quoting 

Ability to supress unwanted expansions using different quotes. 

**double quotes** ignores all expansions except for paramneter expansion, arithmetic expansion and command substitution. (as it doesn't ignore $, \ and \`)

`ls -l two words.txt` file name has a space - but this would end up with an error as it will try to display info for file name two 

`ls -l "two words.txt"` will do the job

**Note: Word splitting in std input treats spaces, tabs and newlines as delimiters between words. Double quotes will stop work splitting behaviour**

`echo $(cal)` will display the calendar text with word splitting (this format lost)

`echo "$(cal)"` will keep the format. 

**single quotes** will ignore all expansions. 

`echo '$(ls)'` will just display $(ls)

**escaping characters** will quote a single character. Also it will suppress characters having a special meaning ($, |, & etc.)

`mv bad&filename goodfilename` since special character is used & will cause an error

`mv bad\&filename goodfilename` will do the job

**backslash escape sequences** \n newline, \t tab, \b b***ackslash etc. (-e should be used with echo to interpret these) 

`echo "hello \nworld"` hello and world will be display in 2 lines

### 8. Advanced keyboard tricks

#### Command line editing

bash uses a library called Readline for command line editing. 

**cursor movement**

CTRL + A move cursor to beginning of line

CTRL + E ...to end of line

ALT + F forward one word

ALT + B backward one word

CTRL + L same as clear

**modifying text**

CTRL + D delete one character at cursor location

ALT + L make from cursor to end of the word lowercase

ALT + U ...uppercase

**cutting (killing) and pasting (yanking)**

CTRL + K kill from cursor to end of line

CTRL + U kill from beginning of line to cursor

ALT + D kill from cursor to end of word

ALT + BACKSPACE kill from cursor to beginning of word. If at the beginning, kills previous word

CTRL + Y yank text from the kill ring (buffer) to the cursor location

#### Completion

This is auto completion feature of the Readline. 

TAB auto-completion. If more than one match or no match - then nothing is auto completed. 

#### Using History

bash keeps the history - by default last 500 commands (in modern distros up to 1000). In my case it's definitely more than 2000 (I had 1756 lines)  

**searching history**

history | less view contents of the command history

history | grep /usr/bin

CTRL + R reverse (from last command backwards) incremental search. press Ctrl + R and as you type the search iteratively finds first maching result (most recent one)

**history expansion**

!! repeat last command (equivalent to up arrow then ENTER)

!!number repeat history list item number

!string repeat last history list item starting with string

!?string repeat last history list item containing the string

### 9. Permissions

One of the main differences of UNIX like systems from MS-DOS like systems is that they are not only multitasking systems, but also multiuser systems, i.e. more than one user is able to use the computer (and simultaneously as well). 

**commands**

id display user identity

chmod change a file's mode

umask set the default file permissions

su run a shell as another user

sudo execute a command as another user

chown change a file's owner

chgrp change a file's group ownership

passwd change a user's password

#### Owners, group members and everybody else (world)

UNIX security system has following role definitions: 

**owner** owns files and directories, may provide access to groups and/or world 

**group** set of users with certain access level

**world** default priviledges

`id` will display uid, gid and assigned groups of current user

`id user` will display same info that user

**Note:** /etc/passwd will contain user information and /etc/group will contain group info. 

#### Reading, writing and executing

When running ls command, first 10 characters are the file attributes as below: 

+ first character is the file type

+ remaining characters called file mode, represent rwx permissions for owner, group and world respectively. 

**file types**

`\-`   regular file

`d`   directory

`l`   symbolic link. with symbolic link attributes are defaulted to all access - real attributes are present for the actual file pointed. 

`c`   a character special file. a streaming device, i.e. terminal, /dev/null etc. 

`b`   a block special file, i.e. hard drive, dvd drive etc. 

**permission attributes for files**

`r` allow a file to be opened and read.

`w` allows a file to be written to or truncated. rename permission is managed by directory attributes. 

`x` allows a file to be treated as a program and be executed. 

**permission attributes for directories**

`r` allow directory contents to be listed (only if `x` attribute is set)

`w` allows files within a directory to be created, renamed or deleted. (only if `x` attribute is set)

`x` allows a directory to be entered (`cd directory`). Also seems that without this permission nothing is really possible for a directory. 

**chmod octal representation**

only owner can run chmod. (and perhaps the root user).  

`chmod 600 foo.txt` this is the octal representation. 600 === (110)(000)(000) === (rw-)(---)(---)

**Note: Seems it's possible to chmod for a directory even from within a directory - in that case not sure how to restore back the right. hope it will be covered in upcoming sections**

**chmod symbolic representation**

Has 3 parts as below: 

+ who `u` for owner, `g` group, `o` others, `a` all. if not present it means all. 

+ which operation `-` remove,  `+` add, `=` set exact permission

+ permissions `r`,`w`,`x`

**examples**

`chmod u+x foo.txt` add execute permission to owner

`chmod +x foo.txt` add execute permission to all

`chmod a=r,o+x` will set read permissions for all users, and additionally execute permission for owner

**Note: chmod operations on symbolic links have no effect, by default all permissions are set**

**umask** command to change default permissions when creating a file 

`umask` will show current setting

`umask 0002` will set umask value to 0002. 

**mask values**

(000)(100)(010)(001) === first octal for special permissions, remove read from owner, remove write from group and remove execute from all. 

`umask 0421; touch a.txt; ls -lah a.txt` --w-r--rw-

**some special permissions** 

setuid bit (octal 4000) - program can be run as root user (effective uid is changed to root)

setgid bit (octal 2000) - when applied to a directory, newly created files within directory will be given group ownership of the file. 

sticky bit (octal 1000) - when applied to directory, prevents users from deleting/renaming files, unless they are either directory owner, file owner or superuser. 

`chmod u+s program` or `chmod 4744` applies setuid bit to an executable. ls -lah would reveal `-rws......` 

`chmod g+s dir` or `chmod 2744` applies setgid bit to a directory. ls -lah would reveal `drwxrws...`

`chmod +t dir` or `chmod 1744` would apply sticky bit to a directory. ls -lah would reveal `drwxr-xr-t`

**setgid and sticky bit can be applied to same directory using `chmod 3744` as well**

#### Changing identities

Sometimes we would want to run a command (or set of commands) under a different identity. There are 3 basic ways to do it: 

1) log out and log in

2) su command (allows running a new shell session or run a single command under different user)

3) sudo command

`su [-[l]] user` a new login shell session for user. l is optional. if user is not specified it starts superuser session. 

`su -c 'command'` run a command as a different user. command should be in '' to have expansion in new shell rather than current one. 

`sudo command` will run a command in current shell. main difference from `su` is that it doesn't require to know superuser password, current user password may be prompted. 

`sudo -i` will start an interactive sudo session

`exit` will leave the sessions above

**chown** command is used to change file owner or group for a file. 

`chown [owner][:[group]] file...` general command usage 

`chown bob file` change file owner to bob

`chown bob:mygroup file` change owner to bob, group to mygroup

`chown :admins file` change group to admins group

`chown bob: file` change owner to bob, group owner to login group of user bob

**in older UNIX systems chown was used only for files, thus `chgrp` command was present to change ownership of group. usage is similar to chown**

#### Changing the password

`passwd` change password of current user

`passwd user` change password of the specified user

### 10. Processes

#### Commands

`ps` report a snapshot of current process

`top` display tasks

`jobs` list active jobs

`bg` place a job in the background

`fg` place a job in the foreground

`kill` send a signal to the process

`killall` kill processes by name

`shutdown` shut down or reboot the system

#### How a Process Works

+ @ startup -> kernel starts processes + program called init

+ init will run a series of scripts called init scripts (located in /etc)

+ these scripts start all the system services

+ many of these services are **deamon programs** - i.e. background programs without any user input

+ parent process / child process -> program launching other programs

+ kernel maintains info about each process:  

a. each process is assigned a process ID (PID)

b. init is assigned PID of 1

c. memory assigned to each process

d. process's readyness to resume execution

e. like files, processes have owners, user IDs, effective user IDs etc. 

#### Viewing Processes

##### ps command

`>ps` will just list processes associated with current terminal session. 

**Note:** the columns `TTY` stands for **teletype** and showing controlling terminal session

**Note:** the column `TIME` shows amount of CPU time consumed by corresponding process

`>ps x` shows all processes

**Note:** the column `STAT` is added - short for state. below are the possible values:

+ `R` running or ready-to-run 

+ `S` sleeping - it's waiting for an event (keystroke, network packet etc.)

+ `D` uninterruptible sleep. waiting for I/O like a disk drive

+ `T` stopped. the process has been instructed to stop. 

+ `Z` a defunct or "zombie" process. child process that's temrinated by parent by not cleaned up yet by its parent.

+ `<` a high priority process. this property of process is called "niceness". a process with high priority is said to be less nice. 

+ `N` a low priority process. (a nice process). will be served only after less nice processes are served. 

`>ps aux` with more information including processes for all users. below additional columns are visible: 

+ `USER` user id

+ `%CPU` CPU usage in percent

+ `%MEM` memory usage in percent

+ `VSZ` virtual memory size

+ `RSS` resident set size. amount of RAM in kB

+ `START` time when the process has started

**Some useful commands**

`>ps aux | sort -rk 3 | less` sort by CPU usage in descending order, paged with less

`>px aux | sort -rk 4 | less` similar to above, this time for memory %

`ps ux -u mehdi | sort -rk 3 | less` only for user mehdi (note that using root doesn't seem to work, filter can be used)

`ps ux | awk '$1="root"' | sort -rk 3 | less` filter only by root

##### top command

Main difference from **ps** is that top lists processes dynamically, updating (by default) every 3 seconds. 

**fields**

+ `top section - load average` average number of runnable processes over 1-last 60 seconds, 2-last 5 mins, 3-last 15 mins

+ `%Cpus(s)`

a. `us` user

b. `sy` system (kernel)

c. `ni` nice processes

d. `id` idle

e. `wa` waiting for I/O

**Note:** to quit top press `q`

#### Controlling processes

`xlogo` will start a program called xlogo and it will not return until it's closed, or `CTRL + C` is pressed to interrupt - just to demonstrate how processes are run. 

`xlogo &` will start xlogo as a background process returning the shell. we will get associated PID as command output. Command `ps` can be used to verify this. 

`jobs` will display the jobs initialized from current terminal. Important notes:

+ it will not display PID

+ this is terminal specific - when ran from a different terminal, nothing will be displayed. 

`fg %1` will bring backround task `1` to foreground (number `1` from jobs or when initializing the process). So after this shell will not return until the program is closed, or `CTRL + C` is pressed.

`CTRL + Z` this will move foreground task xlogo to stopped state (T state). it will be unresponsive, except for functionality provided by OS (I think...)

**Note:** to move process out of this state, either `fg %1` or `bg %1` can be used. 

#### Signals

Signal are one of the several ways OS communicates with programs/processes. 

`CTRL + C` will send a `INT` (interrupt) signal to associated process

`CTRL + Z` will send a `TSTP` (terminal stop) to associated process

##### kill 

`kill -signal PID | %jobspec` will send the specified signal to the PID / or job number. if signal is not specified default is `TERM` (terminate). Note that for signal - integer signal number of signal identifier can be used. 

`kill -l` will list all available signal options

**common signals:**

+ `1` HUP (hang up) - this is from old good days when terminals were using phone lines. This will signal to the process that the controlling terminal has hang up (similar to closing terminal screen). Deamon processes (i.e. Apache web server) use this to re-initialize and thus to re-read the configuration. 

+ `2` INT (interrupt) - same as `CTRL + C`. will usually terminate the program. 

+ `9` KILL (kill) - this is not sent to program, rather sent to Kernel to immediate terminate the program. no opportunity is given to the program to clean up.  

+ `15` TERM (terminate) - this is default if no signal is specified

+ `18` CONT (continue) - will restore a process after STOP or TSTP signal. This signal is used by fg and bg commands. 

+ `19` STOP (stop) similar to KILL command, it's handler by Kernel and cannot be ignored. 

+ `20` TSTP (terminal stop) the differences from STOP is that it's handled by program, and can be ignored. 

+ `3` QUIT (quit)

+ `11` SEGV (segmentation violation)

+ `28` WINCH (window change) - signal sent by system to the program when a window changes its size. some programs will re-draw themselved to fit to new size (like less and top)

##### killall

provides ability to send signal to multiple programs/processes. 

`killall [-u user] [-signal] name...` it can be used with user and/or process name

`killall -u mehdi` not something that you would want to try - as it would kill everything by (not sure what this 'by' means though) user "mehdi"

`killall -u mehdi xlogo` will kill the program xlogo under user mehdi. 

**Note:** Seems that ps command also lists last received signals. 

#### Shutting down the system

shutting down === orderly termination of all the processes and performing some vital house keeping (sync all mounted file systems etc.)

`sudo reboot` reboot

`sudo halt` stops all processes and halts the CPU, leaving the system powered on. manual intervention is required. 

`sudo poweroff` half + power off

`sudo shutdown -h` halt

`sudo shutdown -r` reboot

`sudo shutdown -r +1 "system will be rebooted after 1 minute"` a time span can be passed to shutdown command. The command will be shown to logged in users. 

**Note:** `shutdown -c` will cancel scheduled shutdowns

#### More process related commands

`pstree` outputs a process list in a tree pattern showing parent/child relationship

`pstree -u mehdi` same for only user mehdi

`vmstat` memory/cpu snapshot of the system resources. 

`vmstat 5` real time vmstat with 5 sec time delay

`xload` real time system load program (graphical)

`tload` similar to xload but draws the graph in terminal

**Note:** running `vmstat 2 &` will cause a real problem - the bash will be pseudo returned - and every time CTRL + C is done it will return and then disappear. I could then run fg and then CTRL + C to exit. 


















