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

#####Less (Text file viwer)
* To view a text file, `less text_file`
* Page Up or `b` - Scroll back one page
* Page Down or space - Scroll forward one page
* `G` - Go to the end of the text file
* `1G` - Go to the beginning of the text file
* `/characters` - Search forward in the text file for an occurrence of the specified characters
* `n` - Repeat the previous search
* `h` - Display a complete list less commands and options
* `q` - Quit

#####File (Examiner)
* To use the file program, just type: `file name_of_file`


###4. A Guided Tour


###5. Manipulating Files


###6. Working With Commands


###7. I/O Redirection


###8. Expansion


###9. Permissions


###10. Job Control
