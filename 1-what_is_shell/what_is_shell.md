<h2>1 – What Is the Shell?</h2>

in linux, command lines means shell 

The shell is a program that takes keyboard commands and passes them to the operating system to carry out

all Linux distributions supply a shell program from the GNU Project called bash. The name “bash” is an acronym for “Bourne Again SHell”, a reference to the fact bash is an enhanced replacement for sh, the original Unix shell program written by Steve Bourne.

When using a graphical user interface (GUI), we need another program called a terminal emulator to interact with the shell.

terminal emulators are available for Linux, but they all basically do the same thing; give us access to the shell.

[me@linuxbox ~]$ 

this is how it looks like when openning up a terminal

Note: If the last character of the prompt is a pound sign (“#”) rather than a dollar sign, the terminal session has superuser privileges. This means either we are logged in as the root user or we selected a terminal emulator that provides superuser (administrative) privileges.

If we press the up-arrow key, we will see that the previous command. This is called command history. Most Linux distributions remember the last 1000 commands by default.

While the shell is all about the keyboard, you can also use a mouse with your terminal emulator. A mechanism built into the X Window System (the underlying engine that makes the GUI go) supports a quick copy and paste technique. If you highlight some text by holding down the left mouse button and dragging the mouse over it (or double clicking on a word), it is copied into a buffer maintained by X. Pressing the middle mouse button will cause the text to be pasted at the cursor location.


Note: Don't be tempted to use Ctrl-c and Ctrl-v to perform copy and paste inside a terminal window. They don't work. These control codes have different meanings to the shell and were assigned many years before the release of Microsoft Windows.

Your graphical desktop environment (most likely KDE or GNOME), in an effort to behave like Windows, probably has its focus policy set to “click to focus.” This means for a window to get focus (become active) you need to click on it. This is contrary to the traditional X behavior of “focus follows mouse” which means that a window gets focus just by passing the mouse over it. The window will not come to the foreground until you click on it but it will be able to receive input. Setting the focus policy to “focus follows mouse” will make the copy and paste technique even more useful.

Some Simple Commands 
<br>
<img width="263" height="68" alt="image" src="https://github.com/user-attachments/assets/3982117f-0748-442c-b9b4-f836d38799b8" />
<br>
<img width="496" height="51" alt="image" src="https://github.com/user-attachments/assets/441259af-2109-47bd-8340-d7ad89b0bb61" />
<br>
To see the current amount of free space on our disk drives, enter df
<br>
<img width="510" height="200" alt="image" src="https://github.com/user-attachments/assets/eae4e4f8-646b-4a78-9c3b-00816dcef5b0" />
<br>
to display the amount of free memory, enter the free command
<img width="670" height="90" alt="image" src="https://github.com/user-attachments/assets/1f12ecf9-7386-48cb-a6c2-591e226dcbd6" />
<br>
Even if we have no terminal emulator running, several terminal sessions continue to run behind the graphical desktop. We can access these sessions, called virtual terminals or virtual consoles, by pressing Ctrl-Alt-F1 through Ctrl-Alt-F6 on most Linux distributions. When a session is accessed, it presents a login prompt into which we can enter our username and password. To switch from one virtual console to another, press Alt-F1 through Alt-F6. On most system we can return to the graphical desktop by pressing Alt-F7
