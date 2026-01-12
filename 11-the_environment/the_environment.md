<h2>11 – The Environment</h2>
the shell maintains a body of information during our shell session called the environment. Programs use data stored in the environment to determine facts about the system's configuration. While most programs use configuration files to store program settings, some programs also look for values stored in the environment to adjust their behavior
<ul type=bullets>
  <li/>  printenv – Print part or all of the environment
  <li/>  set – Set shell options
  <li/>  export – Export environment to subsequently executed programs
  <li/>  alias – Create an alias for a command
  <li/>  source – Execute commands from a file in the current shell
</ul>

<h6>What is Stored in the Environment?</h6>
The shell stores two basic types of data in the environment; though, with bash, the types are, at first glance, largely indistinguishable. They are environment variables and shell variables. Shell variables are bits of data placed there by current instance of bash, and environment variables are everything else. In addition to variables, the shell stores some programmatic data, namely aliases and shell functions.

<h6>Examining The Environment</h6>
To see what is stored in the environment, we can use either the set builtin in bash or the printenv program. The set command will show both the shell and environment variables, while printenv will only display the latter. Since the list of environment contents will be fairly long, it is best to pipe the output of either command into less <br>
<img width="185" height="39" alt="image" src="https://github.com/user-attachments/assets/befa3b22-a91b-40f6-9baa-afdace81414d" /> <br>
<img width="546" height="475" alt="image" src="https://github.com/user-attachments/assets/63301a49-a1bc-478e-afbb-ea1ba616e7c5" /> <br>

What we see is a list of environment variables and their values. For example, we see a variable called USER, which contains the value me. The printenv command can also list the value of a specific variable <br>
<img width="182" height="73" alt="image" src="https://github.com/user-attachments/assets/28936398-b218-4a52-8e82-481ea1212e31" /> <br>

set command, when used without options or arguments, will display both the shell and environment variables, as well as any defined shell functions. Unlike printenv, its output is courteously sorted in alphabetical order <br>
<img width="183" height="47" alt="image" src="https://github.com/user-attachments/assets/817acd85-c5c9-4bfd-843f-efc2ea5e6c31" /> <br>
<img width="486" height="485" alt="image" src="https://github.com/user-attachments/assets/1af2f858-180d-4bb2-be7b-f6452cf36e44" /> <br>
It is also possible to view the contents of a variable using the echo command <br>
<img width="239" height="60" alt="image" src="https://github.com/user-attachments/assets/1dafb25b-d149-44e4-b0c7-bc16daec8cdf" /> <br>

One element of the environment that neither set nor printenv displays is aliases. To see them, enter the alias command without arguments <br>
<img width="238" height="231" alt="image" src="https://github.com/user-attachments/assets/540046b7-102c-44fb-9275-0d9b3fe5f6da" /> <br>

<h6>Some Interesting Variables</h6>
The environment contains quite a few variables, and though the environment will differ from the one presented here, we will likely see the variables listed <br>
<img width="808" height="173" alt="image" src="https://github.com/user-attachments/assets/e1274f8b-405b-4cf0-aa08-3983a6de1d34" /> <br>
<img width="657" height="591" alt="image" src="https://github.com/user-attachments/assets/892d8758-8775-46e0-9ac1-ba14b72112fe" /> <br>

<h6>How Is The Environment Established?</h6>
When we log on to the system, the bash program starts, and reads a series of configuration scripts called startup files, which define the default environment shared by all users. This is followed by more startup files in our home directory that define our personal environment. The exact sequence depends on the type of shell session being started. There are two kinds.
<ul type=bullets>
  <li/> A login shell session: A login shell session is one in which we are prompted for our username and password. This happens when we when we log into a graphical environment, for example. It is also done when we start a virtual console session.
  <li/> A non-login shell session: A non-login shell session typically occurs when we launch a terminal session in the GUI with our terminal emulator
</ul>

<img width="904" height="444" alt="image" src="https://github.com/user-attachments/assets/4e34c193-32d9-4d5d-afc3-8b6f420a55ae" /> <br>
<img width="904" height="263" alt="image" src="https://github.com/user-attachments/assets/6ee71222-cc08-41e0-beb9-f6e537a7673f" /> <br>

In addition to reading the startup files in Table 11-3, non-login shells inherit the environment variables from their parent process, usually a login shell <br>
The ~/.bashrc file is probably the most important startup file from the ordinary user’s point of view, since it is almost always read. Non-login shells read it by default and most startup files for login shells are written in such a way as to read the ~/.bashrc file as well

<h6>What's in a Startup File?</h6>
If we take a look inside a typical .bash_profile (taken from a CentOS 6 system) <br>
<img width="619" height="314" alt="image" src="https://github.com/user-attachments/assets/39ef9620-f7b9-40bf-ae13-bfcd08893a63" /> <br>
<img width="580" height="459" alt="image" src="https://github.com/user-attachments/assets/806fb001-d3b6-4f65-880d-85556a2f8dd0" /> <br>
(less ~/.profile) for kali
Lines that begin with a “#” are comments and are not read by the shell. These are there for human readability. The first interesting thing occurs on the fourth line <br>

This is called an if compound command, here is a translation: <br>
<img width="474" height="80" alt="image" src="https://github.com/user-attachments/assets/db87ff5c-37b7-4bb0-aabe-699c469e9427" /> <br>
this bit of code is how a login shell gets the contents of .bashrc. The next thing in our startup file has to do with the PATH variable <br>

Ever wonder how the shell knows where to find commands when we enter them on the command line? For example, when we enter ls, the shell does not search the entire computer to find /bin/ls (the full pathname of the ls command); rather, it searches a list of directories that are contained in the PATH variable. The PATH variable is often (but not always, depending on the distribution) set by the /etc/profile startup file with this code <br>
PATH=$PATH:$HOME/bin <br>
PATH is modified to add the directory $HOME/bin to the end of the list. This is an example of parameter expansion <br>
<img width="302" height="360" alt="image" src="https://github.com/user-attachments/assets/38db7ab1-95c7-4b83-ac2c-22c20d7ecd89" /> <br>
Using this technique, we can append text to the end of a variable's contents <br>

By adding the string $HOME/bin to the end of the PATH variable's contents, the directory $HOME/bin is added to the list of directories searched when a command is entered. This means that when we want to create a directory within our home directory for storing our own private programs, the shell is ready to accommodate us. All we have to do is call it bin, and we’re ready to go <br> 

Note: Many distributions provide this PATH setting by default. Debian based distributions, such as Ubuntu, test for the existence of the ~/bin directory at login and dynamically add it to the PATH variable if the directory is found <br>

Lastly, the export command tells the shell to make the contents of PATH available to child processes of this shell. In a sense, it converts a shell variable into an environment variable.

<h6>Exploring How Child Processes Inherit Their Environments</h6>
Shell variables are local to the current instance of the shell and are not copied to any children the shell launches. <br>
First, we’ll set a shell variable in our current shell <br>
Next, we’ll launch another copy of the shell <br>
Now it looks like nothing happened, but we are in fact running another instance of the shell <br>
we see that we are running two copies of bash. Since we didn’t put the new instance into the background when we launched it, it is now the foreground task and the original instance is waiting for this new shell to finish. <br>
No result indicates the foo variable is empty. The reason for this is we didn’t give it a value in this instance of the shell. Shell variables are not copied and given to a child process when the child process is created. Environment variables, on the other hand, are copied to become the environment of the child process

**an important rule regarding child processes: a child process cannot alter the environment of its parent**
When a child process terminates, it takes its environment with it. This fact will become important when we start writing shell scripts <br>
<img width="281" height="522" alt="image" src="https://github.com/user-attachments/assets/027342bc-cfb6-4577-b0a0-9c2355d551d3" />

<h6>Launching a Program with a Temporary Environment</h6>
Another handy trick the shell provides is the ability to execute a command and give it a temporary environment variable. Sometimes we want to run a program and give it a special environment value. A good example is the man command which looks for an environment variable named MANWIDTH that tells man how wide to format its output. For example, to have man format its output a maximum of 75 characters wide (a handy setting for easy reading) <br>
<img width="268" height="91" alt="image" src="https://github.com/user-attachments/assets/9bb56051-5262-457d-b090-4eb040dad2a1" /> <br>

<h6>Which Files Should We Modify?</h6>
As a general rule, to add directories to your PATH or define additional environment variables, place those changes in .bash_profile (or the equivalent, according to your distribution; for example, Ubuntu uses .profile). For everything else, place the changes in .bashrc. <br>
Note: Unless you are the system administrator and need to change the defaults for all users of the system, restrict your modifications to the files in your home directory. It is certainly possible to change the files in /etc such as profile, and in many cases it would be sensible to do so <br>

<h6>Text Editors</h6>
To edit (i.e., modify) the shell's startup files, as well as most of the other configuration files on the system, we use a program called a text editor. A text editor is a program that is, in some ways, like a word processor in that it allows us to edit the words on the screen with a moving cursor. It differs from a word processor by only supporting pure text and often contains features designed for writing programs. Text editors are the central tool used by software developers to write code and by system administrators to manage the configuration files that control the system. <br>
A lot of different text editors are available for Linux; most systems have several installed <br>

Text editors fall into two basic categories: graphical and text-based. GNOME and KDE both include some popular graphical editors. GNOME ships with an editor called gedit, which is usually called “Text Editor” in the GNOME menu. KDE usually ships with three, which are (in order of increasing complexity) kedit, kwrite, and kate. <br>
There are many text-based editors. The popular ones we'll often encounter are nano, vi, and emacs. The nano editor is a simple, easy-to-use editor designed as a replacement for the pico editor supplied with the PINE email suite. The vi editor (which on most Linux systems is replaced by a program called vim, which is short for “vi improved”) is the traditional editor for Unix-like systems <br>
emacs editor was originally written by Richard Stallman. It is a gigantic, all-purpose, does-everything programming environment. While readily available, it is seldom installed on most Linux systems by default.

<h6>Using a Text Editor </h6>
Text editors are invoked from the command line by typing the name of the editor followed by the name of the file we want to edit. If the file does not already exist, the editor will assume that we want to create a new file. <br>
[me@linuxbox ~]$ gedit some_file <br>
command will start the gedit text editor and load the file named “some_file”, if it exists. <br> <br>

fire up nano and edit the .bashrc file. But before we do that, let's practice some “safe computing.” Whenever we edit an important configuration file, it is always a good idea to create a backup copy of the file first. This protects us in case we mess up the file while editing. To create a backup of the .bashrc file, do this <br>
<img width="217" height="94" alt="image" src="https://github.com/user-attachments/assets/38a88adb-e7f2-435d-9bf2-0e50802220b9" /> <br>
It doesn't matter what we call the backup file; just pick an understandable name. The extensions “.bak”, “.sav”, “.old”, and “.orig” are all popular ways of indicating a backup file. Oh, and remember that cp will overwrite existing files silently <br>
The screen consists of a header at the top, the text of the file being edited in the middle, and a menu of commands at the bottom. Since nano was designed to replace the text editor supplied with an email client, it is rather short on editing features. <br>
<img width="1000" height="541" alt="image" src="https://github.com/user-attachments/assets/1a1a4635-04f1-46b4-80c9-de5b134d247d" /><br>
we press Ctrl-x to exit. <br>
The notation ^X means Ctrl-x. This is a common notation for control characters used by many programs <br>
to save our work. With nano it's Ctrl-o. <br>
Using the down arrow key and/or the PageDown key, move the cursor to the end of the file <br>
add the following lines to the .bashrc file <br>
<img width="230" height="79" alt="image" src="https://github.com/user-attachments/assets/87b77d94-04c3-4bc1-b22b-c597c24d9361" /> <br>
<img width="490" height="357" alt="image" src="https://github.com/user-attachments/assets/18eb2508-8bf0-4af4-aed7-987d99d51dd1" /> <br>
many of our additions are not intuitively obvious, so it would be a good idea to add some comments to our .bashrc file to help explain things to the humans.<br>
<img width="359" height="165" alt="image" src="https://github.com/user-attachments/assets/93f10e7f-8609-416e-83d8-b3bbd5aac704" /> <br>
<img width="467" height="362" alt="image" src="https://github.com/user-attachments/assets/21fcedf3-68ea-4ffb-b02f-ad62ff5e398c" /> <br>
<img width="462" height="36" alt="image" src="https://github.com/user-attachments/assets/0dc6d680-4371-4ac9-87eb-9c04ea8b686d" /> <br>

<h6>Activating Our Changes</h6>
The changes we have made to our .bashrc will not take effect until we close our terminal session and start a new one because the .bashrc file is only read at the beginning of a session. However, we can force bash to reread the modified .bashrc file <br>
<img width="478" height="383" alt="image" src="https://github.com/user-attachments/assets/37227188-04d3-4f9c-a50e-ea612158db54" /> <br>
<img width="223" height="352" alt="image" src="https://github.com/user-attachments/assets/9bd5ac66-2038-4a91-8494-9f4860c1393c" /> <br>
<img width="198" height="110" alt="image" src="https://github.com/user-attachments/assets/7cc993ca-600a-4fcb-a677-c80703b36c4e" /> <br>
<img width="478" height="383" alt="image" src="https://github.com/user-attachments/assets/5a2647e1-cedc-4745-a91c-dd27faa62f13" /> <br>

<h6>A Little More about Source</h6>
The source command (which can be abbreviated as .) is a shell builtin that reads a file directly into the current shell just as if its contents had been entered at the keyboard. Yes, all those strange looking things we have seen in the shell startup files are simply things that shell understands and can act upon. Many older text-based operating systems (DOS, CP/M, etc.) functioned mainly as simple program launchers. Unix style shells can do that of course, as we have seen, but they can also do so much more <br>

we learned an essential skill — editing configuration files with a text editor. Moving forward, as we read man pages for commands, take note of the environment variables that commands support. There may be a gem or two. In later chapters, we will learn about shell functions, a powerful feature that you can also include in the bash startup files to add to your arsenal of custom commands.







