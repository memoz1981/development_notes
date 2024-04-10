## The Linux Command Line - A Complete Introduction - William Shotts, 2nd Edition

This .md file contains my notes wonderful book above. I have no intention to summarize everything covered in the book - main purpose of this file is to prepare a somehow extended appendix only covering the points that are most interesting to me. Also this will help me to refresh my mind if required and just to help me and hopefully others to find out where to find what. 

Have a strong hope to complete reading the book and not to hesitate to do exercises to get most from the book. 

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
















