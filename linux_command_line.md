## The Linux Command Line - A Complete Introduction - William Shotts, 2nd Edition

This .md file contains my notes wonderful book above. I have no intention to summarize everything covered in the book - main purpose of this file is to prepare a somehow extended appendix only covering the points that are most interesting to me. Also this will help me to refresh my mind if required and just to help me and hopefully others to find out where to find what. 

Have a strong hope to complete reading the book and not to hesitate to do exercises to get most from the book. 

### 1. What is Shell? 

- Bash - From GNU project. Bourne-again-shell (after UNIX shell author Steve Bourne)
- Terminal Operators - to interact with the shell

### 2. Navigating

`pwd` - print current directory name

`cd` - change directory

*some_examples*:
`cd` change to home directory

`cd ~` change to home directory

`cd ~user` change to home directory of a user

### 3. Exploring the system

`ls` list content of the directory

`file` determine file type. file name extension in linux are not indicative. use this command to determine the file type. in unix like systems -> everything is a file. 

`less` view text file contents. developed as an improvement to unix tool more and stands for "less is more"

*some_examples*:

`ls -ltr` -l option: long format output, -t option: sort according to time, -r option: reverse sorting

`file picture.jpeg` will output the type of the file (perhaps based on the metadata)

`less /etc/passwd` display the contents of the file /etc/passwd

### 4. Manipulating files and directories

`cp` copy files (and since directories are files this also applies to the directories)

`mv` both for moving and renaming files (and again for directories)

`mkdir` create directory

`rm` remove files (and directories)

`ln` create hard and symbolic links





 
