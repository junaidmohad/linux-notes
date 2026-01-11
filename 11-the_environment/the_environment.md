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
<img width="185" height="39" alt="image" src="https://github.com/user-attachments/assets/befa3b22-a91b-40f6-9baa-afdace81414d" />
<img width="546" height="475" alt="image" src="https://github.com/user-attachments/assets/63301a49-a1bc-478e-afbb-ea1ba616e7c5" /> <br>

What we see is a list of environment variables and their values. For example, we see a variable called USER, which contains the value me. The printenv command can also list the value of a specific variable <br>
<img width="182" height="73" alt="image" src="https://github.com/user-attachments/assets/28936398-b218-4a52-8e82-481ea1212e31" /> <br>

set command, when used without options or arguments, will display both the shell and environment variables, as well as any defined shell functions. Unlike printenv, its output is courteously sorted in alphabetical order <br>
<img width="183" height="47" alt="image" src="https://github.com/user-attachments/assets/817acd85-c5c9-4bfd-843f-efc2ea5e6c31" />
<img width="486" height="485" alt="image" src="https://github.com/user-attachments/assets/1af2f858-180d-4bb2-be7b-f6452cf36e44" />
<br>
It is also possible to view the contents of a variable using the echo command <br>
<img width="239" height="60" alt="image" src="https://github.com/user-attachments/assets/1dafb25b-d149-44e4-b0c7-bc16daec8cdf" />
<br>

One element of the environment that neither set nor printenv displays is aliases. To see them, enter the alias command without arguments <br>
<img width="238" height="231" alt="image" src="https://github.com/user-attachments/assets/540046b7-102c-44fb-9275-0d9b3fe5f6da" /> <br>

<h6>Some Interesting Variables</h6>
The environment contains quite a few variables, and though the environment will differ from the one presented here, we will likely see the variables listed <br>
<img width="808" height="173" alt="image" src="https://github.com/user-attachments/assets/e1274f8b-405b-4cf0-aa08-3983a6de1d34" />
<img width="657" height="591" alt="image" src="https://github.com/user-attachments/assets/892d8758-8775-46e0-9ac1-ba14b72112fe" />

<h6>How Is The Environment Established?</h6>
When we log on to the system, the bash program starts, and reads a series of configuration scripts called startup files, which define the default environment shared by all users. This is followed by more startup files in our home directory that define our personal environment. The exact sequence depends on the type of shell session being started. There are two kinds.
<ul type=bullets>
  <li/> A login shell session: A login shell session is one in which we are prompted for our username and password. This happens when we when we log into a graphical environment, for example. It is also done when we start a virtual console session.
  <li/> A non-login shell session: A non-login shell session typically occurs when we launch a terminal session in the GUI with our terminal emulator
</ul>

<img width="904" height="444" alt="image" src="https://github.com/user-attachments/assets/4e34c193-32d9-4d5d-afc3-8b6f420a55ae" />
<img width="904" height="263" alt="image" src="https://github.com/user-attachments/assets/6ee71222-cc08-41e0-beb9-f6e537a7673f" /> <br>

In addition to reading the startup files in Table 11-3, non-login shells inherit the environment variables from their parent process, usually a login shell <br>
The ~/.bashrc file is probably the most important startup file from the ordinary user’s point of view, since it is almost always read. Non-login shells read it by default and most startup files for login shells are written in such a way as to read the ~/.bashrc file as well

<h6>What's in a Startup File?</h6>
If we take a look inside a typical .bash_profile (taken from a CentOS 6 system) <br>
<img width="619" height="314" alt="image" src="https://github.com/user-attachments/assets/39ef9620-f7b9-40bf-ae13-bfcd08893a63" /> <br>
<img width="580" height="459" alt="image" src="https://github.com/user-attachments/assets/806fb001-d3b6-4f65-880d-85556a2f8dd0" />
(less ~/.profile) for kali
Lines that begin with a “#” are comments and are not read by the shell. These are there for human readability. The first interesting thing occurs on the fourth line

This is called an if compound command, here is a translation: 
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
Another handy trick the shell provides is the ability to execute a command and give it a temporary environment variable. Sometimes we want to run a program and give it a special environment value. A good example is the man command which looks for an environment variable named MANWIDTH that tells man how wide to format its output. For example, to have man format its output a maximum of 75 characters wide (a handy setting for easy reading)
<img width="268" height="91" alt="image" src="https://github.com/user-attachments/assets/9bb56051-5262-457d-b090-4eb040dad2a1" /> <br>

<h6>Which Files Should We Modify?</h6>
As a general rule, to add directories to your PATH or define additional environment variables, place those changes in .bash_profile (or the equivalent, according to your distribution; for example, Ubuntu uses .profile). For everything else, place the changes in .bashrc. <br>
Note: Unless you are the system administrator and need to change the defaults for all users of the system, restrict your modifications to the files in your home directory. It is certainly possible to change the files in /etc such as profile, and in many cases it would be sensible to do so <br>





