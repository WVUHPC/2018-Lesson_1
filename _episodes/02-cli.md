---
title: "Basic Commands to learn"
teaching: 45
exercises: 15
questions:
- "Which are the most basic commands that I need to learn?"
objectives:
- "Learn the most basic commands in Unix/Linux"
keypoints:
- "Learning the basic commands allow you to create files and directories and move around the filesystem"
- "Use *man* to search for arguments of command line tools"
---

## The top 10 basic commands to learn

When you interact with a HPC cluster your interaction is basically by executing commands on a terminal and editing text files. For newcomers using command lines could be a frustrating experience knowing that there are literally hundreds of commands. Certainly there are manuals for most of those commands, but they are of no use if you do not know which is the command you need to use for each situation. The good news is that you can do a lot of things with just a bunch of them and you can learn others in due time.

This is a selection of the 10 most essential commands you need to learn.

### ls

List all the files in a directory. Linux as many Operating Systems organize
files in files and directories (also called folders).

~~~
$ ls
file0a  file0b  folder1  folder2 link0a  link2a
~~~
{: .source}

Some terminal offer color output so you can differentiate normal files from folders. You can make the difference more clear with this

~~~
$ ls -aCF
./  ../  file0a  file0b  folder1/  folder2/ link0a@  link2a@
~~~
{: .source}

You will see a two extra directories `"."` and `".."`. Those are special folders that refer to the current folder and the folder up in the tree.
Directories have the suffix `"/"`. Symbolic links, kind of shortcuts to other files or directories are indicated with the symbol `"@"`.

Another option to get more information about the files in the system is:

~~~
$ ls -al
total 36
drwxrwxr-x.  4 gufranco users     86 May 30 12:16 .
drwxr-xr-x. 82 gufranco users  12288 May 30 12:05 ..
-rw-rw-r--.  1 gufranco users      0 May 30 12:08 file0a
-rw-rw-r--.  1 gufranco users      0 May 30 12:08 file0b
drwxrwxr-x.  2 gufranco users     32 May 30 12:07 folder1
drwxrwxr-x.  2 gufranco users     32 May 30 12:07 folder2
lrwxrwxrwx.  1 gufranco users      6 May 30 12:16 link0a -> file0a
lrwxrwxrwx.  1 gufranco users     14 May 30 12:16 link2a -> folder2/file2a
~~~
{: .source}

Those characters on the first column indicate the permissions. The first character will be "d" for directories, "l" for symbolic links and "-" for normal files. The next 3 characters are the permissions for "read", "write" and "execute" for the owner. The next 3 are for the group, and the final 3 are for others.
The meaning of "execute" for a file indicates that the file could be a script or binary executable. For a directory it means that you can see its contents.

### cp

This command copies the contents of one file into another file. For example

~~~
$ cp file0b file0c
~~~
{: .source}

### rm

This command deletes the contents of one file. For example

~~~
$ rm file0c
~~~
{: .source}
There is no such thing like a trash folder on a HPC system. Deleting a file should be consider an irreversible operation.

Recursive deletes can be done with

~~~
$ rm -rf folder_to_delete
~~~
{: .source}
Be extremely cautious deleting files recursively. You cannot damage the system as the files that you do not own you cannot delete. However, you can delete all your files forever.

### mv

This command moves a files from one directory to another. It also can be used to rename files or directories.

~~~
$ mv file0b file0c
~~~
{: .source}

### pwd

It is easy to get lost when you move in complex directory structures. pwd will tell you the current directory.

~~~
$ pwd
/home/gufranco/Dropbox/SummerHandsOn
~~~
{: .source}

### cd

This command moves you to the directory indicated as an argument, if no argument is given, it returns to your home directory.

~~~
$ cd folder1
~~~
{: .source}

### cat and tac

When you want to see the contents of a text file, the command cat displays the contents on the screen. It is also useful when you want to concatenate the contents of several files.

~~~
$ cat INCAR
system   =  LiAu
PREC      =  High
NELMIN    =  8
NELM      =  100
EDIFF     =  1E-07
...
~~~
{: .source}

To concatenate files you need to use the symbol `">"` indicating that you want to redirect the output of a command into a file

~~~
$ cat file1 file2 file3 > file_all
~~~
{: .source}
The command tac shows the files in reverse starting from the last line back to the first one.

### more and less

Sometimes text files, as those created as product of simulations are too large to be seen in one screen, the command "more" shows the files one screen at a time. The command `"less"` offers more functionality and should be the tool of choice to see large text files.

~~~
$ less OUTCAR
~~~
{: .source}

### ln

This command allow to create links between files. Used wisely could help you save time when traveling frequently to deep directories. By default it creates hard links. Hard links are like copies, but they make references to the same place in disk. Symbolic links are better in many cases because you can cross file systems and partitions. To create a symbolic link

~~~
$ ln -s file1 link_to_file1
~~~
{: .source}

### grep

The grep command extract from its input the lines containing a specified string or regular expression. It is a powerful command for extracting specific information from large files. Consider for example

~~~
$ grep TOTEN OUTCAR
  free energy    TOTEN  =        68.29101273 eV
  free energy    TOTEN  =       -13.46870926 eV
  free energy    TOTEN  =       -18.78141268 eV
  ...
~~~
{: .source}

Regular expressions offers ways to specified text strings that could vary in several ways and allow commands such as grep to extract those strings efficiently. We will see more about regular expressions in third chapter.

### More commands

The 10 commands above, will give you enough tools to move files around and
travel the directory tree.
The GNU Core Utilities are the basic file, shell and text manipulation
utilities of the GNU operating system.
These are the core utilities which are expected to exist on every
operating system.

If you want to know about the whole set of coreutils execute:

~~~
info coreutils
~~~
{: .source}

Each command has its own manual. You can access those manuals with

~~~
man <COMMAND>
~~~
{: .source}

> ### Output of entire files
>
> ~~~
> cat                    Concatenate and write files
> tac                    Concatenate and write files in reverse
> nl                     Number lines and write files
> od                     Write files in octal or other formats
> base64                 Transform data into printable data
> ~~~
> {: .source}
{: .callout}

> ### Formatting file contents
>
> ~~~
> fmt                    Reformat paragraph text
> numfmt                 Reformat numbers
> pr                     Paginate or columnate files for printing
> fold                   Wrap input lines to fit in specified width
> ~~~
> {: .source}
{: .callout}

> ### Output of parts of files
>
> ~~~
> head                   Output the first part of files
> tail                   Output the last part of files
> split                  Split a file into fixed-size pieces
> csplit                 Split a file into context-determined pieces
> ~~~
> {: .source}
{: .callout}

> ### Summarizing files
>
> ~~~
> wc                     Print newline, word, and byte counts
> sum                    Print checksum and block counts
> cksum                  Print CRC checksum and byte counts
> md5sum                 Print or check MD5 digests
> sha1sum                Print or check SHA-1 digests
> sha2 utilities                   Print or check SHA-2 digests
> ~~~
> {: .source}
{: .callout}

> ### Operating on sorted files
>
> ~~~
> sort                   Sort text files
> shuf                   Shuffle text files
> uniq                   Uniquify files
> comm                   Compare two sorted files line by line
> ptx                    Produce a permuted index of file contents
> tsort                  Topological sort
> ~~~
> {: .source}
{: .callout}

> ### Operating on fields
>
> ~~~
> cut                    Print selected parts of lines
> paste                  Merge lines of files
> join                   Join lines on a common field
> ~~~
> {: .source}
{: .callout}

> ### Operating on characters
>
> ~~~
> tr                     Translate, squeeze, and/or delete characters
> expand                 Convert tabs to spaces
> unexpand               Convert spaces to tabs
> ~~~
> {: .source}
{: .callout}

> ### Directory listing
>
> ~~~
> ls                     List directory contents
> dir                    Briefly list directory contents
> vdir                   Verbosely list directory contents
> dircolors              Color setup for 'ls'
> ~~~
> {: .source}
{: .callout}

> ### Basic operations
>
> ~~~
> cp                     Copy files and directories
> dd                     Convert and copy a file
> install                Copy files and set attributes
> mv                     Move (rename) files
> rm                     Remove files or directories
> shred                  Remove files more securely
> ~~~
> {: .source}
{: .callout}

> ### Special file types
>
> ~~~
> link                   Make a hard link via the link syscall
> ln                     Make links between files
> mkdir                  Make directories
> mkfifo                 Make FIFOs (named pipes)
> mknod                  Make block or character special files
> readlink               Print value of a symlink or canonical file name
> rmdir                  Remove empty directories
> unlink                 Remove files via unlink syscall
> ~~~
> {: .source}
{: .callout}

> ### Changing file attributes
>
> ~~~
> chown                  Change file owner and group
> chgrp                  Change group ownership
> chmod                  Change access permissions
> touch                  Change file timestamps
> ~~~
> {: .source}
{: .callout}

> ### Disk usage
>
> ~~~
> df                     Report file system disk space usage
> du                     Estimate file space usage
> stat                   Report file or file system status
> sync                   Synchronize data on disk with memory
> truncate               Shrink or extend the size of a file
> ~~~
> {: .source}
{: .callout}

> ### Printing text
>
> ~~~
> echo                   Print a line of text
> printf                 Format and print data
> yes                    Print a string until interrupted
> ~~~
> {: .source}
{: .callout}

> ### Conditions
>
> ~~~
> false                  Do nothing, unsuccessfully
> true                   Do nothing, successfully
> test                   Check file types and compare values
> expr                   Evaluate expressions
> tee                    Redirect output to multiple files or processes
> ~~~
> {: .source}
{: .callout}

> ### File name manipulation
>
> ~~~
> basename               Strip directory and suffix from a file name
> dirname                Strip last file name component
> pathchk                Check file name validity and portability
> mktemp                 Create temporary file or directory
> realpath               Print resolved file names
> ~~~
> {: .source}
{: .callout}

> ### Working context
>
> ~~~
> pwd                    Print working directory
> stty                   Print or change terminal characteristics
> printenv               Print all or some environment variables
> tty                    Print file name of terminal on standard input
> ~~~
> {: .source}
{: .callout}

> ### User information
>
> ~~~
> id                     Print user identity
> logname                Print current login name
> whoami                 Print effective user ID
> groups                 Print group names a user is in
> users                  Print login names of users currently logged in
> who                    Print who is currently logged in
> ~~~
> {: .source}
{: .callout}

> ### System context
>
> ~~~
> arch                   Print machine hardware name
> date                   Print or set system date and time
> nproc                  Print the number of processors
> uname                  Print system information
> hostname               Print or set system name
> hostid                 Print numeric host identifier
> uptime                 Print system uptime and load
> ~~~
> {: .source}
{: .callout}

> ### Modified command
>
> ~~~
> chroot                 Run a command with a different root directory
> env                    Run a command in a modified environment
> nice                   Run a command with modified niceness
> nohup                  Run a command immune to hangups
> stdbuf                 Run a command with modified I/O buffering
> timeout                Run a command with a time limit
> ~~~
> {: .source}
{: .callout}

> ### Process control
>
> ~~~
> kill                   Sending a signal to processes
> ~~~
> {: .source}
{: .callout}

> ### Delaying
>
> ~~~
> sleep                  Delay for a specified time
> ~~~
> {: .source}
{: .callout}

> ### Numeric operations
>
> ~~~
> factor                 Print prime factors
> seq                    Print numeric sequences
> ~~~
> {: .source}
{: .callout}

{% include links.md %}
