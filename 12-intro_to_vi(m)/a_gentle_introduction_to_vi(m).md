<h1>12 – A Gentle Introduction to vi(m)</h1>

Learning the Linux command line, like becoming an accomplished pianist, is not something that we pick up in an afternoon. It takes years of practice. In this chapter, we will introduce the vi (pronounced “vee eye”) text editor, one of the core programs in the Unix tradition. vi is somewhat notorious for its unique user interface, but when we see a master sit down at the keyboard and begin to “play,” we will indeed be witness to some great art

<h6>A Little Background</h6>
The first version of vi was written in 1976 by Bill Joy, a University of California at Berkeley student who later went on to co-found Sun Microsystems. vi derives its name from the word “visual,” because it was intended to allow editing on a video terminal with a moving cursor. Previous to visual editors, there were line editors that operated on a single line of text at a time. To specify a change, we tell a line editor to go to a particular line and describe what change to make, such as adding or deleting text. With the advent of video terminals (rather than printer-based terminals like teletypes), visual editing became possible. vi actually incorporates a powerful line editor called ex, and we can use line editing commands while using vi. <br>
Most Linux distributions don't include real vi; rather, they ship with an enhanced replacement called vim (which is short for “vi improved”) written by Bram Moolenaar. vim is a substantial improvement over traditional Unix vi and is often symbolically linked (or aliased) to the name vi on Linux systems. In the discussions that follow, we will assume that we have a program called vi that is really vim. <br>

To start vi, we simply enter the following: <br>
[me@linuxbox ~]$ vi <br>

<img width="656" height="545" alt="image" src="https://github.com/user-attachments/assets/a2f88e01-5863-4bf2-8d6d-a2f600f078a9" /> <br>

To exit, we enter the following command (note that the colon character is part of the command): <br>
:q <br>

to force exit <br>
:q! <br>

Different Linux distributions package vim in different ways. Some distributions install a minimal version of vim (i.e., vim-tiny) by default that supports only a limited set of vim features. While performing the lessons that follow, you may encounter missing features. If this is the case, install the full version of vim. <br>

This is how we can create a new file with vi: <br>
[me@linuxbox ~]$ rm -f foo.txt <br>
[me@linuxbox ~]$ vi foo.txt <br>

The second most important thing to learn about vi (after learning how to exit) is that vi is a modal editor. When vi starts, it begins in normal mode. In this mode, almost every key is a command <br>

<h6>Entering Insert Mode</h6>
To add some text to our file, we must first enter insert mode. To do this, we press the i key. Afterward, we should see the following at the bottom of the screen if vim is running in its usual enhanced mode (this will not appear in vi compatible mode) <br>
-- INSERT -- <br>
To exit insert mode and return to normal mode, press the Esc key.

<h6>Saving Our Work</h6>
To save the change we just made to our file, we must enter an command mode. This is done by pressing the : key while in normal mode. After doing this, a colon character should appear at the bottom of the screen. <br>
: <br>
To write our modified file, we follow the colon with a w and then press Enter.
:w <br>


Note: While vim calls the three primary editing modes, normal, insert, and command. Real vi (and its documentation) calls these modes command, insert, and ex, respectively. Many online vi resources will refer to them that way, and yes, it can be confusing. <br>

<h6>Moving the Cursor Around</h6>
While in normal mode, vi offers a large number of movement commands, some of which it shares with less <br>


<img width="490" height="476" alt="image" src="https://github.com/user-attachments/assets/6f08b08d-b0c6-48fb-af23-2ebc848063c4" /><br>
<img width="507" height="56" alt="image" src="https://github.com/user-attachments/assets/66e06511-177b-4737-b05e-927dcc0212da" /> <br>

Why are the h, j, k, and l keys used for cursor movement? When vi was originally written, not all video terminals had arrow keys, and skilled typists could use regular keyboard keys to move the cursor without ever having to lift their fingers from the keyboard. <br>
Many commands in vi can be prefixed with a number, as with the “G” command listed above. By prefixing a command with a number, we may specify the number of times a command is to be carried out. For example, the command “5j” causes vi to move the cursor down five lines. <br>

<h6>Basic Editing</h6>
Most editing consists of a few basic operations such as inserting text, deleting text, and moving text around by cutting and pasting. vi, of course, supports all of these operations in its own unique way. vi also provides a limited form of undo. If we press the “u” key while in normal mode, vi will undo the last change that you made. <br>

**<h6>Appending Text</h6>**
vi has several different ways of entering insert mode. We have already used the i command to insert text.<br>

If we wanted to add some text to the end of this sentence, we would discover that the i command will not do it, since we can't move the cursor beyond the end of the line. vi provides a command to append text, the sensibly named a command. If we move the cursor to the end of the line and type a, the cursor will move past the end of the line and vi will enter insert mode <br>

Since we will almost always want to append text to the end of a line, vi offers a shortcut to move to the end of the current line and start appending. It's the A command. <br>

**<h6>Opening a Line</h6>**
Another way we can insert text is by “opening” a line. This inserts a blank line between two existing lines and enters insert mode. <br>
<img width="342" height="96" alt="image" src="https://github.com/user-attachments/assets/1038a808-2053-4b16-b0a5-598ae863c827" /> <br>

<img width="484" height="106" alt="image" src="https://github.com/user-attachments/assets/906cb1e1-eca7-4b2a-be1b-2867f46f1c06" /> <br>

<img width="503" height="113" alt="image" src="https://github.com/user-attachments/assets/1f4881b4-1df6-4a4b-9a5c-278e499c1d4b" /> <br>

**<h6>Deleting Text</h6>**
As we might expect, vi offers a variety of ways to delete text, all of which contain one of two keystrokes. First, the x command will delete a character at the cursor location. x may be preceded by a number specifying how many characters are to be deleted. The d command is more general purpose. Like x, it may be preceded by a number specifying the number of times the deletion is to be performed. In addition, d is always followed by a movement command that controls the size of the deletion <br>

<img width="479" height="304" alt="image" src="https://github.com/user-attachments/assets/3265fe35-7249-4e22-b1ea-5f640d7dc4f1" />

<img width="475" height="79" alt="image" src="https://github.com/user-attachments/assets/d08f4a21-fa4c-4d7e-a7c3-cbc230acca8b" /> <br>

Note: Real vi supports only a single level of undo. vim supports multiple levels. <br>

<h6>Cutting, Copying, and Pasting Text</h6>
The d command not only deletes text, it also “cuts” text. Each time we use the d command, the deletion is copied into a paste buffer (think clipboard) that we can later recall with the p command to paste the contents of the buffer after the cursor or with the P command to paste the contents before the cursor.
The y command is used to “yank” (copy) text in much the same way the d command is used to cut text. <br>.


<img width="484" height="301" alt="image" src="https://github.com/user-attachments/assets/d36f996c-37ab-403c-94a0-31c6e946564c" />






