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

* `type` - Display information about command type
* `which` - Locate a command
* `help` - Display reference page for shell builtin
* `man` - Display an on-line command reference

####What Are "Commands?"
Commands can be one of 4 different kinds:

* **An executable program** - like all those files we saw in /usr/bin. Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in scripting languages such as the Shell, Perl, Python, Ruby, etc.
* **A command built into the shell itself** - Bash provides a number of commands internally called shell builtins. The `cd` command, for example, is a shell builtin.
* **A shell function** - These are miniature shell scripts incorporated into the environment.
* **An alias** - Commands that you can define yourselves, built from other commands.

####Identifying Commands

* `type` - The `type` command is a shell builtin that displays the kind of command the shell will execute, given a particular command name. It is used like this: `type command`
* `which` - Sometimes there is more than one version of an executable program installed on a system. To determine the exact location of a given executable, the `which` command is used. `which` only works for executable programs.

#### Getting Command Documentation

* `help` - Bash has a built-in help facility available for each of the shell builtins. To use it, type "help" followed by the name of the shell builtin. For example `help cd`
* `man` - Most executable programs intended for command line use provide a formal piece of documentation called a manual or man page. It is used like this: `man program`


###7. I/O Redirection

Many commands such as `ls` print their output on the display. By using some special notations we can redirect the output of many commands to files, devices, and even to the input of other commands.

####Standard Output

By default, standard output directs its contents to the display. To redirect standard output to a file, the `>` character is used like this:

`ls > file_list.txt`

In this example, the `ls` command is executed and the results are written in a file named file_list.txt. Each time the command above is repeated, file_list.txt is overwritten. If you want the new result to be appended to the file, use `>>` like this:

`ls >> file_list.txt`

####Standard Input

Many commands can accept input from standard input. By default, standard input gets its contents from the keyboard, but it can be redirected. To redirect standard input from a file, the `<` character is used like this:

`sort < file_list.txt`

In the above example, we used the `sort` command to process the contents of file_list.txt. The results are output on the display since the standard output was not redirected. We could redirect standard output to another file like this:

`sort < file_list.txt > sorted_file_list.txt`

As you can see, a command can have both its input and output redirected. The order of the redirection does not matter.

####Pipelines

You can connect multiple commands together with pipelines. With pipelines, the standard output of one command is fed into the standard input of another.

`ls -l | less`

In this example, the output of the `ls` command is fed into `less` By using this `| less` trick, you can make any command have scrolling output.

By connecting commands together, you can accomplish many things. Some examples are:

* `ls -lt | head` - Displays the 10 newest files in the current directory.
* `du | sort -nr` - Displays a list of directories and how much space they consume, sorted from the largest to the smallest.
* `find . - type f -print | wc -l` - Displays the total number of files in the current working directory and all of its subdirectories.

####Filters

Filters take standard input and perform an operation upon it and send the results to standard output.

* `sort` - Sort standard input then outputs the sorted result on standard output.
* `uniq` - Given a sorted stream of data from standard input, it removes duplicate lines of data.
* `grep` - Examines each line of data it receives from standard input and outputs every line that contains a specified pattern of characters.
* `fmt` - Reads text from standard input, then outputs formatted text on standard output.
* `pr` - Takes text input from standard input and splits the data into pages with page breaks, headers and footers in preparation for printing.
* `head` - Outputs the first few line of its input. Useful for getting the header of a file.
* `tail` - Outputs the last few lines of its input. Useful for things like getting the most recent entries from a log file.
* `tr` - Translates characters. Can be used to perform tasks such as upper/lowercase conversions or changing line termination characters from one type to another.
* `sed` - stream editor. Can perform more sophisticated text translation than `tr`.
* `awk` - An entire programming language designed for constructing filters.

####Performing tasks with pipelines

1. Printing from the command line

Linux provides a program called `lpr` that accepts standard input and sends it to the printer. It is often used with pipes and filters.

`cat poorly_formatted_report.txt | fmt | pr | lpr`

`cat unsorted_list_with_dupes.txt | sort | uniq | pr | lpr`

In the first example, we use `cat` to read the file and output it to standard output, which is piped into the standard input of `fmt`. `fmt` formats the text and outputs it to standard output, which is piped into the standard input of `pr`. `pr` splits the text into pages and outputs it to standard output, which is piped into the standard input of `lpr`. `lpr` takes its standard input and sends it to the printer.

2. Viewing the contents of tar files

Often you will see software distributed as a gzipped tar file. This is a traditional Unix style tape archive file (created with `tar`) that has been compressed with gzip. You can recognize these files by their traditional file extensions, ".tar.gz" or ".tgz". You can use the following command to view the directory of such a file on a Linux system:

`tar tzvf name_of_file.tar.gz | less`


###8. Expansion

An example of expansion is `*`. With expansion, you type something and it is expanded into something else before the shell acts upon it.
```
echo *
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```
The shell exapnds the `*` into something else (un this instance, the names of the files in the current working directory) before `echo` command is executed. When the enter key is pressed, the shell automatically expands any qualifying characters on the command line before the command is carried out, so the `echo` command never saw the `*`, only its expanded result.

####Pathname Expansion

The mechanism by which wildcards work is called pathname expansion.

````
[me@linuxbox me]$ ls

Desktop
ls-output.txt
Documents Music
Pictures
Public
Templates
Videos

[me@linuxbox me]$ echo D*
Desktop Documents

[me@linuxbox me]$ echo *s
Documents Pictures Templates Videos

[me@linuxbox me]$ echo [[:upper:]]*
Desktop Documents Music Pictures Public Templates Videos

[me@linuxbox me]$ echo /usr/*/share
/usr/kerberos/share /usr/local/share
````

####Tilde Expansion

As you may recall from our introduction to the cd command, the tilde character (“~”) has a special meaning. When used at the beginning of a word, it expands into the name of the home directory of the named user, or if no user is named, the home directory of the current user:
```
[me@linuxbox me]$ echo ~
/home/me
```
If user “foo” has an account, then:
```
[me@linuxbox me]$ echo ~foo
/home/foo
```

####Arithmetic Expansion

The shell allows arithmetic to be performed by expansion. This allow us to use the shell prompt as a calculator:
````
[me@linuxbox me]$ echo $((2 + 2))
4
````
Arithmetic expansion uses the form:
`$((expression))`

Examples:
```
[me@linuxbox me]$ echo Five divided by two equals $((5/2))
Five divided by two equals 2

[me@linuxbox me]$ echo with $((5%2)) left over.
with 1 left over.
```

####Brace Expansion

Perhaps the strangest expansion is called brace expansion. With it, you can create multiple text strings from a pattern containing braces. Here's an example:

```
[me@linuxbox me]$ echo Front-{A,B,C}-Back
Front-A-Back Front-B-Back Front-C-Back
```

Patterns to be brace expanded may contain a leading portion called a preamble and a trailing portion called a postscript. The brace expression itself may contain either a comma-separated list of strings, or a range of integers or single characters. The pattern may not contain embedded whitespace. Here is an example using a range of integers:

```
[me@linuxbox me]$ echo Number_{1..5}
Number_1 Number_2 Number_3 Number_4 Number_5
```

A range of letters in reverse order:

```
[me@linuxbox me]$ echo {Z..A}
Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
```

Brace expansions may be nested:


```
[me@linuxbox me]$ echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```

So what is this good for? The most common application is to make lists of files or directories to be created. For example, if you were a photographer and had a large collection of images you wanted to organize into years and months, the first thing you might do is create a series of directories named in numeric “Year-Month” format. This way, the directory names will sort in chronological order. You could type out a complete list of directories, but that's a lot of work and it's error-prone too. Instead, you could do this:

```
[me@linuxbox me]$ mkdir Photos
[me@linuxbox me]$ cd Photos
[me@linuxbox Photos]$ mkdir {2007..2009}-0{1..9} {2007..2009}-{10..12}
[me@linuxbox Photos]$ ls

2007-01 2007-07 2008-01 2008-07 2009-01 2009-07
2007-02 2007-08 2008-02 2008-08 2009-02 2009-08
2007-03 2007-09 2008-03 2008-09 2009-03 2009-09
2007-04 2007-10 2008-04 2008-10 2009-04 2009-10
2007-05 2007-11 2008-05 2008-11 2009-05 2009-11
2007-06 2007-12 2008-06 2008-12 2009-06 2009-12
```

####Parameter Expansion

To invoke parameter expansion and reveal the contents of USER you would do this:

```
[me@linuxbox me]$ echo $USER
me
```

To see a list of available variables, try this:

```
[me@linuxbox me]$ printenv | less
```

####Command Substitution

Command substitution allows us to use the output of a command as an expansion:

```
[me@linuxbox me]$ echo $(ls)
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

An example:

```
[me@linuxbox me]$ ls -l $(which cp)
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp
```

Here we passed the results of which cp as an argument to the ls command, thereby getting the listing of of the cp program without having to know its full pathname. We are not limited to just simple commands. Entire pipelines can be used (only partial output shown):


```
[me@linuxbox me]$ file $(ls /usr/bin/* | grep bin/zip)

/usr/bin/bunzip2:
/usr/bin/zip:      ELF 32-bit LSB executable, Intel 80386, version 1 
(SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.15, stripped
/usr/bin/zipcloak: ELF 32-bit LSB executable, Intel 80386, version 1
(SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.15, stripped
/usr/bin/zipgrep:  POSIX shell script text executable
/usr/bin/zipinfo:  ELF 32-bit LSB executable, Intel 80386, version 1
(SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.15, stripped
/usr/bin/zipnote:  ELF 32-bit LSB executable, Intel 80386, version 1
(SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.15, stripped
/usr/bin/zipsplit: ELF 32-bit LSB executable, Intel 80386, version 1
(SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.15, stripped
```

####Quoting

Now that we've seen how many ways the shell can perform expansions, it's time to learn how we can control it. Take for example:

```
[me@linuxbox me]$ echo this is a     test
this is a test
```

or:

```
[me@linuxbox me]$ [me@linuxbox ~]$ echo The total is $100.00
The total is 00.00
```

In the first example, word-splitting by the shell removed extra whitespace from the echo command's list of arguments. In the second example, parameter expansion substituted an empty string for the value of “$1” because it was an undefined variable. The shell provides a mechanism called quoting to selectively suppress unwanted expansions.

####Double Quotes

The first type of quoting we will look at is double quotes. If you place text inside double quotes, all the special characters used by the shell lose their special meaning and are treated as ordinary characters. The exceptions are “$”, “\” (backslash), and “`” (back- quote). This means that word-splitting, pathname expansion, tilde expansion, and brace expansion are suppressed, but parameter expansion, arithmetic expansion, and command substitution are still carried out. Using double quotes, we can cope with filenames containing embedded spaces. Say you were the unfortunate victim of a file called two words.txt. If you tried to use this on the command line, word-splitting would cause this to be treated as two separate arguments rather than the desired single argument:

```
[me@linuxbox me]$ ls -l two words.txt

ls: cannot access two: No such file or directory
ls: cannot access words.txt: No such file or directory
```

By using double quotes, you can stop the word-splitting and get the desired result; further, you can even repair the damage:

```
[me@linuxbox me]$ ls -l "two words.txt"
-rw-rw-r-- 1 me me 18 2008-02-20 13:03 two words.txt
[me@linuxbox me]$ mv "two words.txt" two_words.txt
```

There! Now we don't have to keep typing those pesky double quotes. Remember, parameter expansion, arithmetic expansion, and command substitution still take place within double quotes:

```
[me@linuxbox me]$ echo "$USER $((2+2)) $(cal)"

me 4
February 2008
Su Mo Tu We Th Fr Sa
                1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29
```

word-splitting is suppressed and the embedded spaces are not treated as delimiters, rather they become part of the argument. Once the double quotes are added, our command line contains a command followed by a single argument. The fact that newlines are considered delimiters by the word-splitting mechanism causes an interesting, albeit subtle, effect on command substitution. Consider the following:

```
[me@linuxbox me]$ echo $(cal)
February 2008 Su Mo Tu We Th Fr Sa 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
[me@linuxbox me]$ echo "$(cal)"

February 2008
Su Mo Tu We Th Fr Sa
                1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29
```

In the first instance, the unquoted command substitution resulted in a command line containing thirty-eight arguments. In the second, a command line with one argument that includes the embedded spaces and newlines.

####Single Quotes

If you need to suppress all expansions, you use single quotes. Here is a comparison of unquoted, double quotes, and single quotes:

```
[me@linuxbox me]$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/ls-output.txt a b foo 4 me
[me@linuxbox me]$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text ~/*.txt {a,b} foo 4 me
[me@linuxbox me]$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```

####Escaping Characters

Sometimes you only want to quote a single character. To do this, you can precede a character with a backslash, which in this context is called the escape character. Often this is done inside double quotes to selectively prevent an expansion:

```
[me@linuxbox me]$ echo "The balance for user $USER is: \$5.00"
The balance for user me is: $5.00
```

It is also common to use escaping to eliminate the special meaning of a character in a filename. For example, it is possible to use characters in filenames that normally have special meaning to the shell. These would include “$”, “!”, “&”, “ “, and others. To include a special character in a filename you can to this:

```
[me@linuxbox me]$ mv bad\&filename good_filename
```

To allow a backslash character to appear, escape it by typing “\\”. Note that within single quotes, the backslash loses its special meaning and is treated as an ordinary character.

####More Backslash Tricks

If you look at the man pages for any program written by the GNU project, you will notice that in addition to command line options consisting of a dash and a single letter, there are also long option names that begin with two dashes. For example, the following are equivalent:

```
ls -r
ls --reverse
```

Why do they support both? The short form is for lazy typists on the command line and the long form is mostly for scripts though some options may only be long form. I sometimes use obscure options, and I find the long form useful if I have to review a script again months after I wrote it. Seeing the long form helps me understand what the option does, saving me a trip to the man page. A little more typing now, a lot less work later. Laziness is maintained.

As you might suspect, using the long form options can make a single command line very long. To combat this problem, you can use a backslash to get the shell to ignore a newline character like this:

```
ls -l \
   --reverse \
   --human-readable \
   --full-time
```

Using the backslash in this way allows us to embed newlines in our command. Note that for this trick to work, the newline must be typed immediately after the backslash. If you put a space after the backslash, the space will be ignored, not the newline. Backslashes are also used to insert special characters into our text. These are called backslash escape characters. Here are the common ones:

* `\n` - newline: Adding blank lines to text
* `\t` - tab: Inserting horizontal tabs to text
* `\a` - alert: Makes your terminal beep
* `\\` - backslash: Inserts a backslash
* `\f` - formfeed: Sending this to your printer ejects the page

The use of the backslash escape characters is very common. This idea first appeared in the C programming language. Today, the shell, C++, perl, python, awk, tcl, and many other programming languages use this concept. Using the echo command with the -e option will allow us to demonstrate:

```
[me@linuxbox me]$ echo -e "Inserting several blank lines\n\n\n"
Inserting several blank lines



[me@linuxbox me]$ echo -e "Words\tseparated\tby\thorizontal\ttabs."
Words separated   by  horizontal  tabs
[me@linuxbox me]$ echo -e "\aMy computer went \"beep\"."

My computer went "beep".

[me@linuxbox me]$ echo -e "DEL C:\\WIN2K\\LEGACY_OS.EXE"

DEL C:\WIN2K\LEGACY_OS.EXE
```


###9. Permissions

The Unix-like operating systems, such as Linux differ from other computing systems in that they are not only multitasking but also multi-user.

This lesson will cover the following commands:

* `chmod` - modify file access rights
* `su` - temporarily become the superuser
* `sudo` - temporarily become the superuser
* `chown` - change file ownership
* `chgrp` - change a file's group ownership

To see the permission settings for a file, we can use the ls command. As an example, we will look at the bash program which is located in the /bin directory:

```
[me@linuxbox me]$ ls -l /bin/bash


-rwxr-xr-x 1 root root  316848 Feb 27  2000 /bin/bash
```

Here we can see:

* The file "/bin/bash" is owned by user "root"
* The superuser has the right to read, write, and execute this file
* The file is owned by the group "root"
* Members of the group "root" can also read and execute this file
* Everybody else can read and execute this file

```
-rwxr-xr-x   1 root     root       316848 Feb 27  2000 /bin/bash
----------     -------  -------  -------- ------------ -------------
| |  |  |         |        |         |         |             |
| |  |  |         |        |         |         |         File Name
| |  |  |         |        |         |         |
| |  |  |         |        |         |         +---  Modification Time
| |  |  |         |        |         |
| |  |  |         |        |         +-------------   Size (in bytes)
| |  |  |         |        |
| |  |  |         |        +-----------------------        Group
| |  |  |         |
| |  |  |         +--------------------------------        Owner
| |  |  |
| |  |	+------------------------------------------   Read, write, and execute permissions for all other users
| |  |
| |  +---------------------------------------------   Read, write, and execute permissions for the group owner of the file
| |
| +------------------------------------------------   Read, write, and execute permissions for the file owner
|
+--------------------------------------------------   File type: "-" indicates regular file "d" indicates directory

```

####chmod

The chmod command is used to change the permissions of a file or directory. To use it, you specify the desired permission settings and the file or files that you wish to modify. There are two ways to specify the permissions. In this lesson we will focus on one of these, called the octal notation method.

It is easy to think of the permission settings as a series of bits (which is how the computer thinks about them). Here's how it works:

```
rwx rwx rwx = 111 111 111
rw- rw- rw- = 110 110 110
rwx --- --- = 111 000 000
```

and so on...

```
rwx = 111 in binary = 7
rw- = 110 in binary = 6
r-x = 101 in binary = 5
r-- = 100 in binary = 4
```

Now, if you represent each of the three sets of permissions (owner, group, and other) as a single digit, you have a pretty convenient way of expressing the possible permissions settings. For example, if we wanted to set some_file to have read and write permission for the owner, but wanted to keep the file private from others, we would:

```
[me@linuxbox me]$ chmod 600 some_file
```

Here is a table of numbers that covers all the common settings. The ones beginning with "7" are used with programs (since they enable execution) and the rest are for other kinds of files.

* `777` - (rwxrwxrwx) No restrictions on permissions. Anybody may do anything. Generally not a desirable setting.
* `755` - (rwxr-xr-x) The file's owner may read, write, and execute the file. All others may read and execute the file. This setting is common for programs that are used by all users.
* `700` - (rwx------) The file's owner may read, write, and execute the file. Nobody else has any rights. This setting is useful for programs that only the owner may use and must be kept private from others.
* `666` - (rw-rw-rw-) All users may read and write the file.
* `644` - (rw-r--r--) The owner may read and write a file, while all others may only read the file. A common setting for data files that everybody may read, but only the owner may change.
* `600` - (rw-------) The owner may read and write a file. All others have no rights. A common setting for data files that the owner wants to keep private.

####Directory Permissions

The chmod command can also be used to control the access permissions for directories. Again, we can use the octal notation to set permissions, but the meaning of the r, w, and x attributes is different:

* `r` - Allows the contents of the directory to be listed if the x attribute is also set.
* `w` - Allows files within the directory to be created, deleted, or renamed if the x attribute is also set.
* `x` - Allows a directory to be entered (i.e. `cd` `dir`).

Here are some useful settings for directories:

* `777` - (rwxrwxrwx) No restrictions on permissions. Anybody may list files, create new files in the directory and delete files in the directory. Generally not a good setting.
* `755` - (rwxr-xr-x) The directory owner has full access. All others may list the directory, but cannot create files nor delete them. This setting is common for directories that you wish to share with other users.
* `700` - (rwx------) The directory owner has full access. Nobody else has any rights. This setting is useful for directories that only the owner may use and must be kept private from others.

####Becoming The Superuser For A Short While

It is often necessary to become the superuser to perform important system administration tasks, but as you have been warned, you should not stay logged in as the superuser.

```
[me@linuxbox me]$ su
Password:
[root@linuxbox me]#
```

After executing the `su` command, you have a new shell session as the superuser. To `exit` the superuser session, type exit and you will return to your previous session.

In some distributions, most notably Ubuntu, an alternate method is used. Rather than using `su`, these systems employ the `sudo` command instead. With `sudo`, one or more users are granted superuser privileges on an as needed basis. To execute a command as the superuser, the desired command is simply preceeded with the `sudo` command. After the command is entered, the user is prompted for the user's password rather than the superuser's:

```
[me@linuxbox me]$ sudo some_command
Password:
[me@linuxbox me]$
```

####Changing File Ownership

You can change the owner of a file by using the `chown` command. Here's an example: Suppose I wanted to change the owner of some_file from "me" to "you". I could:

```
[me@linuxbox me]$ su
Password:
[root@linuxbox me]# chown you some_file
[root@linuxbox me]# exit
[me@linuxbox me]$
```

Notice that in order to change the owner of a file, you must be the superuser. To do this, our example employed the `su` command, then we executed `chown`, and finally we typed `exit` to return to our previous session.

chown works the same way on directories as it does on files.

####Changing Group Ownership

The group ownership of a file or directory may be changed with `chgrp`. This command is used like this:

```
[me@linuxbox me]$ chgrp new_group some_file
```

In the example above, we changed the group ownership of some_file from its previous group to "new_group". You must be the owner of the file or directory to perform a `chgrp`.


###10. Job Control

As with any multitasking operating system, Linux executes multiple, simultaneous processes. Well, they appear simultaneous, anyway. Actually, a single processor computer can only execute one process at a time but the Linux kernel manages to give each process its turn at the processor and each appears to be running at the same time.

There are several commands that can be used to control processes. They are:

* `ps` - list the processes running on the system
* `kill` - send a signal to one or more processes (usually to "kill" a process)
* `jobs` - an alternate way of listing your own processes
* `bg` - put a process in the background
* `fg` - put a process in the forground

####A Practical Example

You might not know this, but most (if not all) of the graphical programs can be launched from the command line. Here's an example: there is a small program supplied with the X Window system called `xload` which displays a graph representing system load. You can excute this program by typing the following:

```
[me@linuxbox me]$ xload
```

Notice that the small `xload` window appears and begins to display the system load graph. Notice also that your prompt did not reappear after the program launched. The shell is waiting for the program to finish before control returns to you. If you close the `xload` window, the `xload` program terminates and the prompt returns.

####Putting A Program In The Background

Now, in order to make life a little easier, we are going to launch the xload program again, but this time we will put it in the background so that the prompt will return. To do this, we execute xload like this:

```
[me@linuxbox me]$ xload &
[1] 1223

[me@linuxbox me]$
```

In this case, the prompt returned because the process was put in the background.

Now imagine that you forgot to use the "&" symbol to put the program into the background. There is still hope. You can type Ctrl-z and the process will be suspended. The process still exists, but is idle. To resume the process in the background, type the bg command (short for background). Here is an example:

```
[me@linuxbox me]$ xload
[2]+ Stopped xload

[me@linuxbox me]$ bg
[2]+ xload &
```

####Listing Your Processes

Now that we have a process in the background, it would be helpful to display a list of the processes we have launched. To do this, we can use either the jobs command or the more powerful ps command.

```
[me@linuxbox me]$ jobs
[1]+ Running xload &

[me@linuxbox me]$ ps
PID TTY TIME CMD
1211 pts/4 00:00:00 bash
1246 pts/4 00:00:00 xload
1247 pts/4 00:00:00 ps

[me@linuxbox me]$
```

####Killing A Process

Suppose that you have a program that becomes unresponsive; how do you get rid of it? You use the kill command, of course. Let's try this out on xload. First, you need to identify the process you want to kill. You can use either jobs or ps, to do this. If you use jobs you will get back a job number. With ps, you are given a process id (PID). We will do it both ways:

```
[me@linuxbox me]$ xload &
[1] 1292

[me@linuxbox me]$ jobs
[1]+ Running xload &

[me@linuxbox me]$ kill %1

[me@linuxbox me]$ xload &
[2] 1293
[1] Terminated xload

[me@linuxbox me]$ ps
PID TTY TIME CMD
1280 pts/5 00:00:00 bash
1293 pts/5 00:00:00 xload
1294 pts/5 00:00:00 ps

[me@linuxbox me]$ kill 1293
[2]+ Terminated xload

[me@linuxbox me]$
```

####A Little More About kill

While the `kill` command is used to "kill" processes, its real purpose is to send signals to processes. Most of the time the signal is intended to tell the process to go away, but there is more to it than that. Programs (if they are properly written) listen for signals from the operating system and respond to them, most often to allow some graceful method of terminating. For example, a text editor might listen for any signal that indicates that the user is logging off, or that the computer is shutting down. When it receives this signal, it saves the work in progress before it exits. The `kill` command can send a variety of signals to processes. Typing:

```
    kill -l
```

will give you a list of the signals it supports. Most are rather obscure, but several are useful to know:

* `1` SIGHUP - Hang up signal. Programs can listen for this signal and act upon it. This signal is sent to processes running in a terminal when you close the terminal.
* `2` SIGINT - Interrupt signal. This signal is given to processes to interrupt them. Programs can process this signal and act upon it. You can also issue this signal directly by typing Ctrl-c in the terminal window where the program is running.
* `15` SIGTERM - Termination signal. This signal is given to processes to terminate them. Again, programs can process this signal and act upon it. This is the default signal sent by the kill command if no signal is specified.
* `9`	SIGKILL - Kill signal. This signal causes the immediate termination of the process by the Linux kernel. Programs cannot listen for this signal.

Now let's suppose that you have a program that is hopelessly hung and you want to get rid of it. Here's what you do:

1. Use the `ps` command to get the process id (PID) of the process you want to terminate.
2. Issue a `kill` command for that PID.
3. If the process refuses to terminate (i.e., it is ignoring the signal), send increasingly harsh signals until it does terminate.

```
[me@linuxbox me]$ ps x | grep bad_program
PID TTY STAT TIME COMMAND
2931 pts/5 SN 0:00 bad_program

[me@linuxbox me]$ kill -SIGTERM 2931

[me@linuxbox me]$ kill -SIGKILL 2931
```

In the example above I used the `ps` command with the x option to list all of my processes (even those not launched from the current terminal). In addition, I piped the output of the `ps` command into `grep` to list only list the program I was interested in. Next, I used `kill` to issue a SIGTERM signal to the troublesome program. In actual practice, it is more common to do it in the following way since the default signal sent by `kill` is SIGTERM and `kill` can also use the signal number instead of the signal name:

```
[me@linuxbox me]$ kill 2931
```

Then, if the process does not terminate, force it with the SIGKILL signal:

```
[me@linuxbox me]$ kill -9 2931
```
