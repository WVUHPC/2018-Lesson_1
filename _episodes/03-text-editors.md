---
title: "Text Editors"
teaching: 105
exercises: 15
questions:
- "How edit text files on Linux using the terminal?"
objectives:
- "Learn about the 3 most popular terminal-based text editors"
keypoints:
- "The choice of an editor is very personal, it is your compromise between features and learning curve"
---

## Text Editors in Unix/Linux

There are several terminal-based editors available on our clusters. We will focus our attention to three of them: nano, emacs and vim.
Your choice of an editor depends mostly on how much functionality do you want from your editor, how many fingers do you want to use for a given command and the learning curve to master it.
For HPC users the editor is an important choice. Most of your time you are on the terminal executing commands or editing files, being those input files, submission scripts or the output of your calculations.


Lets review those three editors to give you the opportunity to have an informative choice.

## Nano

Nano is a small, free and friendly editor with commands that usually manage using the Control (CTRL) combined with some other key.

You can start editing a file using a command line like this

~~~
nano myfile.f90
~~~
{: .source}


There are several commands available, the list below comes from the help text.
When you see the symbol `"^"` it means to press the Control (CTRL) key, the symbol
`"M-"` is called Meta, but in most keyboards is identified with the (Alt) key.

~~~
^G	(F1)            Display the help text
^X	(F2)            Close the current file buffer / Exit from nano
^O	(F3)            Write the current file to disk
^J	(F4)            Justify the current paragraph

^R	(F5)            Insert another file into the current one
^W	(F6)            Search for a string or a regular expression
^Y	(F7)            Move to the previous screen
^V	(F8)            Move to the next screen

^K	(F9)            Cut the current line and store it in the cutbuffer
^U	(F10)           Uncut from the cutbuffer into the current line
^C	(F11)           Display the position of the cursor
^T	(F12)           Invoke the spell checker, if available
~~~
{: .source}

The most basic usage is to edit a file, and exit from the editor with CTRL-X.
Nano ask you if you want to save the file, you answer "Y" and offers you a name.
Simply press ENTER and your file is saved.

## Emacs

Emacs is an extensible, customizable, open-source text editor. Together with Vi/Vim is one the most widely
used editors in Linux environments. There are a big number of commands, customizations and extra modules
that can be integrated with Emacs. We will just go briefly covering the basics.

The number of commands for Emacs is large, here the basic list of commands for editing, moving and searching text.

### Entering Emacs

~~~
 emacs <filename>
~~~
{: .source}

### Leaving Emacs

~~~
 suspend Emacs (or iconify it under X) C-z
 exit Emacs permanently C-x C-c
~~~
{: .source}

### Files

~~~
 read a file into Emacs C-x C-f
 save a file back to disk C-x C-s
 save all files C-x s
 insert contents of another file into this buffer C-x i
 replace this file with the file you really want C-x C-v
 write buffer to a specified file C-x C-w
 toggle read-only status of buffer C-x C-q
~~~
{: .source}

### Incremental Search

~~~
 search forward C-s
 search backward C-r
 regular expression search C-M-s
 reverse regular expression search C-M-r
 select previous search string M-p
 select next later search string M-n
 exit incremental search RET
 undo effect of last character DEL
 abort current search C-g
 Use C-s or C-r again to repeat the search in either direction. If
 Emacs is still searching, C-g cancels only the part not matched.
~~~
{: .source}

### Motion

~~~
 entity to move over backward forward
 character C-b C-f
 word M-b M-f
 line C-p C-n
 go to line beginning (or end) C-a C-e
 sentence M-a M-e
 paragraph M-{ M-}
 page C-x [ C-x ]
 sexp C-M-b C-M-f
 function C-M-a C-M-e
 go to buffer beginning (or end) M-< M->
 scroll to next screen C-v
 scroll to previous screen M-v
 scroll left C-x <
 scroll right C-x >
 scroll current line to center, top, bottom C-l
 goto line M-g g
 goto char M-g c
 back to indentation M-m
~~~
{: .source}

### Killing and Deleting

~~~
 entity to kill backward forward
 character (delete, not kill) DEL C-d
 word M-DEL M-d
 line (to end of) M-0 C-k C-k
 sentence C-x DEL M-k
 sexp M-- C-M-k C-M-k
 kill region C-w
 copy region to kill ring M-w
 kill through next occurrence of char M-z char
 yank back last thing killed C-y
 replace last yank with previous kill M-y
~~~
{: .source}

### Marking

~~~
 set mark here C-@ or C-SPC
 exchange point and mark C-x C-x
 set mark arg words away M-@
 mark paragraph M-h
 mark page C-x C-p
 mark sexp C-M-@
 mark function C-M-h
 mark entire buffer C-x h
~~~
{: .source}

### Query Replace

~~~
 interactively replace a text string M-%
 using regular expressions M-x query-replace-regexp
 Valid responses in query-replace mode are

 replace this one, go on to next SPC or y
 replace this one, don’t move ,
 skip to next without replacing DEL or n
 replace all remaining matches !
 back up to the previous match ^
 exit query-replace RET
 enter recursive edit (C-M-c to exit) C-r
~~~
{: .source}



### Formatting

~~~
 indent current line (mode-dependent) TAB
 indent region (mode-dependent) C-M-\
 indent sexp (mode-dependent) C-M-q
 indent region rigidly arg columns C-x TAB
 indent for comment M-;
 insert newline after point C-o
 move rest of line vertically down C-M-o
 delete blank lines around point C-x C-o
 join line with previous (with arg, next) M-^
 delete all white space around point M-\
 put exactly one space at point M-SPC
 fill paragraph M-q
 set fill column to arg C-x f
 set prefix each line starts with C-x .
 set face M-o
~~~
{: .source}

### Case Change

~~~
 uppercase word M-u
 lowercase word M-l
 capitalize word M-c
 uppercase region C-x C-u
 lowercase region C-x C-l
~~~
{: .source}

## Vi/Vim

The third editor widely supported on Linux systems is "vi".
Over the years since its creation, vi became the *de-facto* standard Unix editor.
The Single UNIX Specification specifies vi, so every conforming system must have it.

vi is a modal editor: it operates in either insert mode (where typed text becomes part of the document) or normal mode (where keystrokes are interpreted as commands that control the edit session).
For example, typing i while in normal mode switches the editor to insert mode, but typing i again at this point places an "i" character in the document.
From insert mode, pressing ESC switches the editor back to normal mode.

Vim is an improved version of the original vi, it offers

Here is a summary of the main commands used on vi. On Spruce when using "vi" you are actually using "vim".


### To Start vi

To use vi on a file, type in vi filename. If the file named filename exists, then the first page (or screen) of the file will be displayed; if the file does not exist, then an empty file and screen are created into which you may enter text.

~~~
 vi filename	edit filename starting at line 1
 vi -r filename	recover filename that was being edited when system crashed
~~~
{: .source}

### To Exit vi

Usually the new or modified file is saved when you leave vi. However, it is also possible to quit vi without saving the file.
Note: The cursor moves to bottom of screen whenever a colon (:) is typed. This type of command is completed by hitting the <Return> (or <Enter>) key.

~~~
 :x<Return>	quit vi, writing out modified file to file named in original invocation
 :wq<Return>	quit vi, writing out modified file to file named in original invocation
 :q<Return>	quit (or exit) vi
 :q!<Return>	quit vi even though latest changes have not been saved for this vi call
~~~
{: .source}

### Moving the Cursor

Unlike many of the PC and MacIntosh editors, the mouse does not move the cursor within the vi editor screen (or window). You must use the the key commands listed below. On some UNIX platforms, the arrow keys may be used as well; however, since vi was designed with the Qwerty keyboard (containing no arrow keys) in mind, the arrow keys sometimes produce strange effects in vi and should be avoided.
If you go back and forth between a PC environment and a UNIX environment, you may find that this dissimilarity in methods for cursor movement is the most frustrating difference between the two.
In the table below, the symbol `"^"` before a letter means that the `CTRL` key should be held down while the letter key is pressed.

~~~
 j or <Return> [or down-arrow]	   move cursor down one line
 k [or up-arrow]	           move cursor up one line
 h or <Backspace> [or left-arrow]  move cursor left one character
 l or <Space> [or right-arrow]	   move cursor right one character
 0 (zero)	                   move cursor to start of current line (the one with the cursor)
 $	                           move cursor to end of current line
 w	                           move cursor to beginning of next word
 b	                           move cursor back to beginning of preceding word
 :0<Return> or 1G	           move cursor to first line in file
 :n<Return> or nG	           move cursor to line n
 :$<Return> or G	           move cursor to last line in file
~~~
{: .source}

### Screen Manipulation

The following commands allow the vi editor screen (or window) to move up or down several lines and to be refreshed.

~~~
 ^f	move forward one screen
 ^b	move backward one screen
 ^d	move down (forward) one half screen
 ^u	move up (back) one half screen
 ^l	redraws the screen
 ^r	redraws the screen, removing deleted lines
~~~
{: .source}

### Adding, Changing, and Deleting Text

This command acts like a toggle, undoing and redoing your most recent action.
You cannot go back more than one step.

~~~
	u	UNDO WHATEVER YOU JUST DID; a simple toggle
~~~
{: .source}

### Inserting or Adding Text

The following commands allow you to insert and add text.
Each of these commands puts the vi editor into insert mode; thus, the <Esc> key must be pressed to terminate the entry of text and to put the vi editor
back into command mode.

~~~
 i	insert text before cursor, until <Esc> hit
 I	insert text at beginning of current line, until <Esc> hit
 a	append text after cursor, until <Esc> hit
 A	append text to end of current line, until <Esc> hit
 o	open and put text in a new line below current line, until <Esc> hit
 O	open and put text in a new line above current line, until <Esc> hit
~~~
{: .source}

### Changing Text

The following commands allow you to modify text.

~~~
 r	replace single character under cursor (no <Esc> needed)
 R	replace characters, starting with current cursor position, until <Esc> hit
 cw	change the current word with new text, starting with the character under cursor, until <Esc> hit
 cNw	change N words beginning with character under cursor, until <Esc> hit; e.g., c5w changes 5 words
 C	change (replace) the characters in the current line, until <Esc> hit
 cc	change (replace) the entire current line, stopping when <Esc> is hit
 Ncc or cNc	change (replace) the next N lines, starting with the current line, stopping when <Esc> is hit
~~~
{: .source}

### Deleting Text

The following commands allow you to delete text.

~~~
 x	delete single character under cursor
 Nx	delete N characters, starting with character under cursor
 dw	delete the single word beginning with character under cursor
 dNw	delete N words beginning with character under cursor; e.g., d5w deletes 5 words
 D	delete the remainder of the line, starting with current cursor position
 dd	delete entire current line
 Ndd 	delete N lines, beginning with the current line; e.g., 5dd deletes 5 lines
 dNd    same as Ndd
~~~
{: .source}

### Cutting and Pasting Text

The following commands allow you to copy and paste text.

~~~
 yy     copy (yank, cut) the current line into the buffer
 Nyy    copy (yank, cut) the next N lines, including the current line, into the buffer
 yNy    same as Nyy
 p      put (paste) the line(s) in the buffer into the text after the current line
~~~
{: .source}

### Searching Text

A common occurrence in text editing is to replace one word or phase by another. To locate instances of particular sets of characters (or strings), use the following commands.

~~~
 /string	search forward for occurrence of string in text
 ?string	search backward for occurrence of string in text
 n	move to next occurrence of search string
 N	move to next occurrence of search string in opposite direction
~~~
{: .source}

### Determining Line Numbers

Being able to determine the line number of the current line or the total number of lines in the file being edited is sometimes useful.

~~~
 :.=	returns line number of current line at bottom of screen
 :=	returns the total number of lines at bottom of screen
 ^g	provides the current line number, along with the total number of lines, in the file at the bottom of the screen
~~~
{: .source}

### Saving and Reading Files

These commands permit you to input and output files other than the named file with which you are currently working.

~~~
 :r filename<Return>	        read file named filename and insert after current line (the line with cursor)
 :w<Return>	                write current contents to file named in original vi call
 :w newfile<Return>	        write current contents to a new file named newfile
 :12,35w smallfile<Return>	write the contents of the lines numbered 12 through 35 to a new file named smallfile
 :w! prevfile<Return>	        write current contents over a pre-existing file named prevfile
~~~
{: .source}

{% include links.md %}
