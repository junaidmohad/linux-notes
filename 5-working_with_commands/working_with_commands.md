5 – Working with Commands
<ul type=bullets>
  <li/>  type – Indicate how a command name is interpreted
  <li/>  which – Display which executable program will be executed
  <li/>  help – Get help for shell builtins
  <li/>  man – Display a command's manual page
  <li/>  apropos – Display a list of appropriate commands
  <li/>  info – Display a command's info entry
  <li/>  whatis – Display one-line manual page descriptions
  <li/>  alias – Create an alias for a command
</ul>
<h6>What Exactly Are Commands?</h6>
A command can be one of four different things:
<ol type=numbers>
  <li/> An executable program like all those files we saw in /usr/bin. Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in scripting languages such as the shell, Perl, Python, Ruby, and so on.
  <li/> A command built into the shell itself. bash supports a number of commands internally called shell builtins. The cd command, for example, is a shell builtin.
  <li/> A shell function. Shell functions are miniature shell scripts incorporated into the environment. We will cover configuring the environment and writing shell functions in later chapters, but for now, just be aware that they exist.
  <li/> An alias. Aliases are commands that we can define ourselves, built from other commands.
</ol>
<h6> type – Display a Command's Type </h6>
  The type command is a shell builtin that displays the kind of command the shell will execute, given a particular command name. <br>
<img width="282" height="182" alt="image" src="https://github.com/user-attachments/assets/baa68ff0-98b8-4f78-9a3f-c382e1701e29" /> <br>
ls command is actually an alias for the ls command with the “--color=tty” option added. Now we know why the output from ls is displayed in color!

<h6> which – Display an Executable's Location </h6>
  Sometimes there is more than one version of an executable program installed on a system. While this is not common on desktop systems, it's not unusual on large servers. To determine the exact location of a given executable, the which command is used. 
<br>
<img width="255" height="187" alt="image" src="https://github.com/user-attachments/assets/a239f549-577c-4296-8b46-34c09776f4d7" />
<br>
which only works for executable programs, not builtins nor aliases that are substitutes for actual executable programs. When we try to use which on a shell builtin for example, cd, we either get no response or get an error message

<h6>help – Get Help for Shell Builtins</h6>
<br>
<img width="332" height="120" alt="image" src="https://github.com/user-attachments/assets/50a6e677-b8e7-4fb2-a8ca-10572a32cb0a" />
<br>
A note on notation: When square brackets appear in the description of a command's syntax, they indicate optional items. A vertical bar character indicates mutually exclusive items. In the case of the cd command above: <br>
cd [-L|[-P[-e]]] [dir] <br>
This notation says that the command cd may be followed optionally by either a “-L” or a “-P” and further, if the “-P” option is specified the “-e” option may also be included followed by the optional argument “dir”.

Helpful hint: By using the help command with the -m option, help will display its output in an alternate format.

<h6>--help – Display Usage Information</h6>
<br>
<img width="632" height="401" alt="image" src="https://github.com/user-attachments/assets/470125c2-bdf2-4d51-82d0-f8ef3bbcb98f" />
<br>
<h6>man – Display a Program's Manual Page</h6>
  Most executable programs intended for command line use provide a formal piece of documentation called a manual or man page. A special paging program called man is used to view them.
  Man pages vary somewhat in format but generally contain the following:
  <ol type=bullets>
    <li/> A title (the page’s name)
    <li/> A synopsis of the command's syntax
    <li/> A description of the command's purpose
    <li/> A listing and description of each of the command's options
Man pages, however, do not usually include examples, and are intended as a reference, not a tutorial. <br>

<img width="647" height="538" alt="image" src="https://github.com/user-attachments/assets/e7e60f65-cbce-4b45-a49a-9953f7313856" />
<img width="842" height="400" alt="image" src="https://github.com/user-attachments/assets/d0c567e8-a321-4f98-9cd5-668fdd77ea03" /> <br>

Sometimes we need to refer to a specific section of the manual to find what we are looking for. This is particularly true if we are looking for a file format that is also the name of a command. Without specifying a section number, we will always get the first instance of a match, probably in section 1. To specify a section number, we use man like this:<br>
  
  man section search_term <br>
  
<img width="177" height="52" alt="image" src="https://github.com/user-attachments/assets/37bffed9-5bcf-48b4-aad3-c99bde969fce" /><br>
<img width="638" height="537" alt="image" src="https://github.com/user-attachments/assets/3ccc1584-da38-42db-8c61-a922b41c9206" />

<h6>apropos – Display Appropriate Commands</h6>
  It is also possible to search the list of man pages for possible matches based on a search term. It's crude but sometimes helpful.<br>
<img width="645" height="404" alt="image" src="https://github.com/user-attachments/assets/dafafffc-694c-41a4-abd5-4991e776af7d" />

  <br>

Note that the man command with the “-k” option performs the same function as apropos.

<h6>whatis – Display One-line Manual Page Descriptions</h6>
  The whatis program displays the name and a one-line description of a man page matching a specified keyword <br>
<img width="397" height="61" alt="image" src="https://github.com/user-attachments/assets/5de399bc-a72c-454c-a105-69ab36cbd1da" />

<h6>The Most Brutal Man Page Of Them All</h6>
As we have seen, the manual pages supplied with Linux and other Unix-like systems are intended as reference documentation and not as tutorials. Many man pages are hard to read, but I think that the grand prize for difficulty has got to go to the man page for bash. As I was doing research for this book, I gave the bash man page careful review to ensure that I was covering most of its topics. When printed, it's more than 80 pages long and extremely dense, and its structure makes absolutely no sense to a new user.
On the other hand, it is very accurate and concise, as well as being extremely complete. So check it out if you dare and look forward to the day when you can read it and it all makes sense.

<h6>info – Display a Program's Info Entry</h6>
  The GNU Project provides an alternative to man pages for their programs, called “info.” Info manuals are displayed with a reader program named, appropriately enough, info. Info pages are hyperlinked much like web pages.<br>
<img width="653" height="467" alt="image" src="https://github.com/user-attachments/assets/e7b2c9d3-9366-47ad-b48f-02f9937fd39d" /><br>

The info program reads info files, which are tree structured into individual nodes, each containing a single topic. Info files contain hyperlinks that can move the reader from node to node. A hyperlink can be identified by its leading asterisk and is activated by placing the cursor upon it and pressing the Enter key.<br>

<img width="832" height="349" alt="image" src="https://github.com/user-attachments/assets/1afe9503-073a-4230-8db8-93833852493c" />
<img width="835" height="92" alt="image" src="https://github.com/user-attachments/assets/170fe6ff-cb75-4673-82d7-c82efc0ba7b1" />

Most of the command line programs we have discussed so far are part of the GNU Project's coreutils package

<h6>README and Other Program Documentation Files</h6>
Many software packages installed on our system have documentation files residing in the /usr/share/doc directory. Most of these are stored in plain text format and can be viewed with less. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a “.gz” extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless that will display the contents of gzip-compressed text files.

It's possible to put more than one command on a line by separating each command with a semicolon. It works like this:<br>
command1; command2; command3... <br>
<img width="593" height="89" alt="image" src="https://github.com/user-attachments/assets/958359b2-74c5-4fc8-aff6-f0ca219a75f6" />
<img width="648" height="274" alt="image" src="https://github.com/user-attachments/assets/ddabdbce-04b6-4807-8fb2-63470ab4b1d1" />
<img width="297" height="55" alt="image" src="https://github.com/user-attachments/assets/fc920b25-4fb3-4b6d-b6de-2639637bdd9e" />
<img width="171" height="105" alt="image" src="https://github.com/user-attachments/assets/afe24dfd-c731-438d-8183-b693e79a575a" />
<img width="289" height="284" alt="image" src="https://github.com/user-attachments/assets/a2de8833-dfc7-4eeb-9956-324c3e82167a" />
<br>
While we purposefully avoided naming our alias with an existing command name, it is not uncommon to do so. This is often done to apply a commonly desired option to each invocation of a common command.
To see all the aliases defined in the environment, use the alias command without arguments. Here are some of the aliases defined by default on a Fedora system

There is one tiny problem with defining aliases on the command line. They vanish when our shell session ends.
