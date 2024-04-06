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





 
