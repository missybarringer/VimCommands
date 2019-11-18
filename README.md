# VimCommands

Vim provides many ways to move the cursor. Becoming familiar with them leads to more effective text editing.

h   move one character left
j   move one row down
k   move one row up
l   move one character right
w   move to beginning of next word
b   move to previous beginning of word
e   move to end of word
W   move to beginning of next word after a whitespace
B   move to beginning of previous word before a whitespace
E   move to end of word before a whitespace
All the above movements can be preceded by a count; e.g. 4j moves down 4 lines.

0   move to beginning of line
$   move to end of line
_   move to first non-blank character of the line
g_  move to last non-blank character of the line

gg  move to first line
G   move to last line
ngg move to n'th line of file (n is a number; 12gg moves to line 12)
nG  move to n'th line of file (n is a number; 12G moves to line 12)
H   move to top of screen
M   move to middle of screen
L   move to bottom of screen

zz  scroll the line with the cursor to the center of the screen
zt  scroll the line with the cursor to the top
zb  scroll the line with the cursor to the bottom

Ctrl-D  move half-page down
Ctrl-U  move half-page up
Ctrl-B  page up
Ctrl-F  page down
Ctrl-O  jump to last (older) cursor position
Ctrl-I  jump to next cursor position (after Ctrl-O)
Ctrl-Y  move view pane up
Ctrl-E  move view pane down

n   next matching search pattern
N   previous matching search pattern
*   next whole word under cursor
#   previous whole word under cursor
g*  next matching search (not whole word) pattern under cursor
g#  previous matching search (not whole word) pattern under cursor
gd  go to definition/first occurrence of the word under cursor
%   jump to matching bracket { } [ ] ( )

fX  to next 'X' after cursor, in the same line (X is any character)
FX  to previous 'X' before cursor (f and F put the cursor on X)
tX  til next 'X' (similar to above, but cursor is before X)
TX  til previous 'X'
;   repeat above, in same direction
,   repeat above, in reverse direction
See :help {command} (for example, :help g_) for all of the above if you want more details.

Vim has four modes: Normal, Insert, Visual, and Command. Each mode shows it’s name at the bottom left of the status bar in the program.

When you start Vim, it’s in Normal mode. You can use all the command keys to navigate around the file and start editing. When you exit any of the other modes, Vim goes back to the Normal mode.

Vim is in Insert mode with the use of the a, A, i, I, o, and O commands. Once in Insert mode, the editor will stay in that mode until you press an Esc key. Every other key pressed is directly inserted into the file at the current cursor location.

Visual mode happens when you use a v, V, and Ctrl-v commands from Normal mode. In Visual mode, you can select text. As you use a navigation command, the area from the beginning of Visual mode to when you exit Visual mode is the selected text.

Anytime you use the : command in Normal mode, you will enter into Command mode. In Command mode, you can perform complex editing functions, file actions, or shell actions. Command mode is the only mode that does not display anything on the status line, but the command entered gets placed under the status line with anything else typed and the cursor.

##Saving Files, and Closing Vim
In Normal mode, you can type ZZ to save everything and exit. You can also save the file with :w!. The : will put you into Command Mode, the w will write the file, and the ! forces the operation to write without questions. Or, you can type :wq or :wq!. The q quits the editor. You can also use :q! to quit without saving.

##Basic Cursor Movements
In Normal mode, you move around the file and make specific edits to the file. The h key moves the cursor to the left. The l key moves the cursor to the right. The j key moves the cursor down a line, while the k key moves the cursor up a line. To move to the next word, use the w command. The previous word command is b.

If you want to move more than one space, word, or line at a time, type a number first and then the direction key. The cursor will move in that direction that number of times. For example, if you type 10j, the cursor will move down 10 lines.

By using the Command mode, you can switch the line numbering to absolute or relative:

Absolute numbering mode is the normal: each line with a unique number in sequential order. 
Relative numbering mode shows the number of lines away from the current edit line.

To have absolute line numbering, you can use the :set number command. To not show line numbers, you use the :set nonumber command.

To set Relative numbering, type :set relativenumber. To put it back to Absolute numbering, type :set norelativenumber.

By setting both modes using :set number and :set relativenumber, your Vim will then show relative numbers for all but the current line. The current edit line will show it’s absolute numbering.

By using Relative numbering mode, you can quickly see the number of lines to move using the j or k commands. For example, to move to the line with List, you would press 2j.

To move to the beginning of a line, use the 0 (that’s a zero) command. To move to the end of a line, use the $ command. The gg command will move the cursor to the beginning of the file, while the G command will move to the end of the file.

##The .vimrc File
You might prefer to always have the Relative line numbering, but it’s hard to always set it when starting Vim. That’s where the Vim configuration file is useful. In the terminal at your home directory, type

1   vim .vimrc
The .vimrc file is Vim’s configuration file. Any command you type in command mode can be added to this file. It will be ran every time Vim is started. In that file, use the i command to start inserting text. Now add the these lines and save it:

1   set number
2   set relativenumber
3   set hlsearch

Now, every time you open Vim it will have the mixed Absolute and Relative line numbering mode set with all search results highlighted as well. Highlighted search is useful in the next section. There is much more you can do with the .vimrc file, but that will have to wait for another tutorial.

##Search and Replace
You can search by using the / command in Normal mode. By typing /This, you will see all of the This words highlighted as below.

By typing n, your cursor goes to the next occurrence of the search pattern. By using N, you can go back to a previous occurrence. The pattern given after the / can be any regular expression. Read the article Advanced Search and Replace With RegEx to understand regular expressions better.

In order to replace text, you have to make use of Command mode. In Command mode, the s command is for substitution in the current line, %s for substitution in the whole file, and <begin>,<end>s for substituting from <begin> line number to the <end> line number.

The format is /<search pattern>/<replace pattern>/gi where the <search pattern> and the <replace pattern> are standard regular expressions. In the example above, I am replacing every existence of This with That. The i after the g makes the search case insensitive. An I would make the search case sensitive. The g makes the substitution global in the line. Without the g, it performs the substitution once per line.

##Editing Commands
To insert text to the left of the current cursor location, use the i command. The a command inserts to the right of the current cursor location. The I command inserts to the front of the line, while A inserts to the end of the line.

The o command inserts a whole new line after the line the cursor is on and puts the editor into Insert mode at the beginning of that line. The O does the same, but adds the line above the current cursor location.

To delete characters, use the d command and then a direction to delete the character in that direction, or the space bar to delete the character under the cursor. If you prefix with a number, then Vim will delete that number characters in the specified direction. The dd command will delete the current line. The D command will delete everything from the current cursor location to the end of the line.

The x command will delete the cursor character. The X command deletes before the cursor. Both the x and X commands will take a number prefix to perform the action that number of times.

##Copy, Cut, and Paste
When you press v in Normal mode, Visual mode begins. All cursor movements cause a selection from the beginning of Visual mode. When you have a selection, using the y command yanks or copies the selected text. Move to a new location and use the p command to paste after the cursor, while the P command pastes before the cursor.

After making a selection, the x command will delete the selection. Using the d command will cut the section so you can paste with the p command.

In order to select a block of text, you start with the <ctrl>-v command. The V command starts Visual mode selecting by lines and not characters.

https://vim-adventures.com/


Simple VIM Reference                  http://simpletutorials.com
------------------------------------------------------------------------------

When you first open the VIM editor, you are in the command mode of the editor. 
The command mode is where you type in VIM commands to manipulate text. 

Insertion mode is where you can type text normally. (Like in Windows Notepad) 
To get into insertion mode, type i (abbreviation for insert). 
To get into command mode, press the Esc key.

If you're ever not sure which mode you're in, just press the Esc key 
and you'll be in command mode for sure.

The following commands are executed in command mode.
------------------------------------------------------------------------------


Copy & Paste
------------
Press v. (To enter visual mode so you can highlight stuff)

Use the arrow keys (or h,j,k,l,w,b,$) to highlight

Press y to yank, p to paste. (shift-p to open up a line above and paste)

Copy a word                         yw
Copy a line                         yy
Copy from cursor to end of line     y$


Copy & Paste (with Registers)
-----------------------------
Press v. (To enter visual mode so you can highlight stuff)

Use the arrow keys (or h,j,k,l,w,b,$) to highlight

Type "ay to yank into register a.
Type "ap to paste from register a.


Deleting
--------
Press v. (To enter visual mode so you can highlight stuff)

Use the arrow keys (or h,j,k,l,w,b,$) keys to higlight and press d

Delete character                x
Delete word                     dw
Delete word and insert text     cw
Delete line                     dd
Delete to end of line           d$


Indenting
---------
Press v and then arrow keys (or h,j,k,l,w,$) to highlight lines of text.

Type > or < to indent right or left.

(to indent more, type 2> or 3>)

(to change your indenting/tabbing to use spaces and not tabs, type :set et)
(to set auto-indenting, type :set ai)
(to set the tab-size, type :set ts=2 (or whatever number you want)
(also, for tabbing-size, set shiftwidth (>) by typing :set sw=2)


Navigation
----------
Go up                         k
Go down                       j
Go left                       h
Go right                      l
Go right a word               w
Go left a word                b
Go to beginning of file       gg
Go to end of file             G
Go 22 lines down              22j
Go to end of line             $
Go to beginning of 
non-whitespace part of line   ^

Go right 5 words              5w


Insert Text
-----------
Insert at cursor                      i
Insert after cursor                   a     (useful when at the end of a line)
Open a line below cursor and insert   o
Open a line above cursor and insert   shift-o


Quitting VIM 
------------
Type :q to quit the editor.


Saving a file
-------------
Type :w to write to the file.


Search & Replace
----------------
Search  /  (after the slash put whatever you want to find 
            and press the enter key)

Find next       n
Find previous   N

Turn off highlighting (after a search)  :noh

Find next instance of a word that your
cursor is over    *

Search and replace from current 
line to end of file   :,$s/search/replace/gc (the gc means global and confirm)


Shell (Exit temporarily to a shell)
-----------------------------------
Type  :sh

To come back to VIM  from the shell type  exit 


Split Window Editing
--------------------
Type :sp followed by the filename.

Go to window above  ctrl-w-k
Go to window below  ctrl-w-j

Maximize window size  ctrl-w  _ 
(the underscore is NOT  pressed at the same time as the ctrl-w)

Make all windows equal size  ctrl-w =
(the equals sign is NOT pressed at the same time as the ctrl-w)


Undo a Command 
--------------
Undo                              u
Redo an undo                      ctrl-r


View Directory & File Explorer
------------------------------
Type :S  (the S is uppercase)

This will split the window and open up a file explorer.  
Use the <enter> key to select directories or to open files.
