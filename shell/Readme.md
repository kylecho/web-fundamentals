#Learning the Shell [Link](http://linuxcommand.org/lc3_learning_the_shell.php)

This is a summary from the resource written by William E. Shotts, Jr. Original can be found from [here](http://linuxcommand.org/lc3_learning_the_shell.php)

###1. What Is "The Shell"?
It is a user interface available on a Unix-like system such as Linux. We have graphical user interfaces (GUIs) in addition to command line interfaces (CLIs) such as the shell.

On most Linux systems a program called bash(an enhanced version of the original Unix shell program, sh) acts as the shell program.

Terminal is a program called a terminal emulator. It opens a window and lets you interact with the shell. It gives you access to a shell session.


###2. Navigation
* `cd ..` to change the working directory to the parent.
* `cd` will change the working directory to your home directory.
* `cd -` changes the working directory to the previous one.
* File names that begin with `.` are hidden. `la -a` will display all.
* File names in Linux, like Unix, are case sensitive.
* Limit the punctuation characters to period, dash and underscore when naming a file. Do not embed spaces in file names.


###3. Looking Around
* `ls` List the files in the working directory.
* `ls /bin` List the files in the /bin directory
* `ls -l` List the files in the working directory in long format.
* `ls -l /etc /bin` List the files in the /bin directory and the /etc directory in long format.
* `ls -la ..` List all files (including hidden) in the parent of the working directory in long format.

####Visualization:

```
-rw-------   1 bshotts  bshotts       576 Apr 17  1998 weather.txt
drwxr-xr-x   6 bshotts  bshotts      1024 Oct  9  1999 web_page
-rw-rw-r--   1 bshotts  bshotts    276480 Feb 11 20:41 web_site.tar
-rw-------   1 bshotts  bshotts      5743 Dec 16  1998 xmas_file.txt

----------     -------  -------  -------- ------------ -------------
    |             |        |         |         |             |
    |             |        |         |         |         File Name
    |             |        |         |         |
    |             |        |         |         +---  Modification Time
    |             |        |         |
    |             |        |         +-------------   Size (in bytes)
    |             |        |
    |             |        +-----------------------        Group
    |             |
    |             +--------------------------------        Owner
    |
    +----------------------------------------------   File Permissions
```

####Less (Text file viwer)
* To view a text file, `less text_file`
* Page Up or `b` - Scroll back one page
* Page Down or space - Scroll forward one page
* `G` - Go to the end of the text file
* `1G` - Go to the beginning of the text file
* `/characters` - Search forward in the text file for an occurrence of the specified characters
* `n` - Repeat the previous search
* `h` - Display a complete list less commands and options
* `q` - Quit

####File (Examiner)
* To use the file program, just type: `file name_of_file`


###4. A Guided Tour

* `cd` into each directory.
* Use `ls` to list the contents of the directory.
* If you see an interesting file, use the `file` command to determine its contents
* For text files, use `less` to view them.

####Interesting directories and their contents

* `/bin` - contains most of the programs for the system. The /bin directory has the essential programs that the system requires to operate.
* `/etc` - contains the configuration files for the system.
* For full example, visit the original link.

###5. Manipulating Files

* `cp` - copy files and directories
* `mv` - move or rename files and directories
* `rm` - remove files and directories
* `mkdir` - create directories

The benefit of manipulating files using commands comes from the the power and flexibility. While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command line programs.

For example, how would you copy all the HTML files from one directory to another, but only copy files that did not exist in the destination directory or were newer than the version in the destination directory? Pretty hard with a file manager, pretty easy with the command line:
`cp -u *.html destination`

####Wildcards

* `*` - Matches any characters
* `?` - Matches any single character
* `[characters]` - Matches any character that is a member of the set characters.
* `[:alnum:]` - Alphanumeric characters
* `[:alpha:]` - Alphabetic characters
* `[:digit:]` - Numerals
* `[:upper:]` - Uppercase alphabetic characters
* `[:lower:]` - Lowercase alphabetic characters
* `[!characters]` - Matches any character that is not a member of the set characters

####Examples of wildcard matching

* `*` - All filenames
* `g*` - All filenames that begin with the character "g" 
* `b*.txt` - All filenames that begin with the character "b" and end with the characters ".txt"
* `Data???` - Any filename that begins with the character "Data" followed by exactly 3 more characters
* `[abc]*` - Any filename that begins with "a" or "b" or "c" followed by any other characters
* `[[:upper:]]*` - Any filename that begins with an uppercase letter. This is an example of a character class.
* `BACKUP.[[:digit:]][[:digit:]]` - Another example of character classes. This pattern matches any filename that begins with the characters "BACKUP." followed by exactly two numerals.
* `*[![:lower:]]` - Any filename that does not end with a lowercase letter.

You can use wildcards with any command that accepts filename arguments.

####The `cp` program copies files and directories

* `cp file1 file2` - Copies the contents of file1 into file2. If file2 does not exist, it is created; otherwise, file2 is overwritten with the contents of file1.
* `cp -i file1 file2` - Like above however, since the `-i` (interactive) option is specified, if file2 exists, the user is prompted before it is overwritten with the contents of file1.
* `cp file1 dir1` - Copy the contents of file1 (into a file named file1) inside of directory dir1.
* `cp -R dir1 dir2` - Copy the contents of the directory dir1. If directory dir2 does not exist, it is created. Otherwise, it creates a directory named dir1 within directory dir2.

####The `mv` command moves or renames files and directories depending on how it is used

* `mv file1 file2` - If file2 does not exist, then file1 is renamed file2. If file2 exists, its contents are replaced with the contents of file1.
* `mv -i file1 file2` - If file2 exists, the user is prompted before it is overwritten with the contents of file1.
* `mv file1 file2 file3 dir1` - The files file1, file2, file3 are moved to directory dir1. If dir1 does not exist, mv will exit with an error.
* `mv dir1 dir2` - If dir2 does not exist, then dir1 is renamed dir2. If dir2 exists, the dir1 is moved within directory dir2.

####The `rm` command removes (deletes) files and directories

* `rm file1 file2` - Delete file1 and file2.
* `rm -i file1 file2` - The user is prompted before each file is deleted.
* `rm -r dir1 dir2` - Directories dir1 and dir2 are deleted along with all of their contents.

####Be careful with rm!

Linux does not have an undelete command. Once you delete something with rm, it's gone. You can inflict terrific damage on your system with rm if you are not careful, particularly with wildcards.

Before you use rm with wildcards, try this helpful trick: construct your command using ls instead. By doing this, you can see the effect of your wildcards before you delete files. After you have tested your command with ls, recall the command with the up-arrow key and then substitute rm for ls in the command.

####The `mkdir` command is used to create directories

* `mkdir directory...`

####Using commands with wildcards

* `cp *.txt text_files` - Copy all files in the current working directory with names ending with the characters ".txt" to an existing directory named text_files.
* `mv my_dir ../*.bak my_new_dir` - Move subdirectory my_dir and all the files ending in ".bak" in the current working directory's parent directory to an existing directory named my_new_dir.
* `rm *~` - Delete all files in the current working directory that end with the character "~". Some applications create backup files using this naming scheme.


###6. Working With Commands


###7. I/O Redirection


###8. Expansion


###9. Permissions


###10. Job Control
