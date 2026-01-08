
# linux-notes
My notes for learning linux


 
3 – Exploring the System
  ●  ls – List directory contents
  ●  file – Determine file type
  ●  less – View file contents

<img width="548" height="282" alt="image" src="https://github.com/user-attachments/assets/0479226c-2595-43e7-934b-2819019b341d" />

We can even specify multiple directories. In the following example, we list both the user's home directory (symbolized by the “~” character) and the /usr directory.

We can also change the format of the output to reveal more detail.

<img width="420" height="183" alt="image" src="https://github.com/user-attachments/assets/f109b542-99e9-449a-ae65-252adcc6a024" />

Commands are often followed by one or more options that modify their behavior, and further, by one or more arguments, the items upon which the command acts. So most commands look kind of like this: 
command -options arguments
<img width="426" height="180" alt="image" src="https://github.com/user-attachments/assets/63afd3cd-4bb2-41fc-8bf9-b7cec2ef1762" />

Note that command options, like filenames in Linux, are case-sensitive.

<img width="663" height="629" alt="image" src="https://github.com/user-attachments/assets/fa060e47-b4db-4413-ad54-9f5ae491a9cb" />

<img width="833" height="568" alt="image" src="https://github.com/user-attachments/assets/43414849-9fa6-46ec-b29f-fd260ec1cf01" />

As we explore the system it will be useful to know what kind of data files contain. To do this we will use the file command to determine a file's type

[me@linuxbox ~]$ file picture.jpg
picture.jpg: JPEG image data, JFIF standard 1.01

The less command is a program to view text files. Throughout our Linux system, there are many files that contain human-readable text. The less program provides a convenient way to examine them

There are many ways to represent information on a computer. All methods involve defining a relationship between the information and some numbers that will be used to represent it. Computers, after all, only understand numbers and all data is converted to numeric representation.

Some of these representation systems are very complex (such as compressed video files), while others are rather simple. One of the earliest and simplest is called ASCII text. ASCII (pronounced "As-Key") is short for American Standard Code for Information Interchange. This is a simple encoding scheme that was first used on Teletype machines to map keyboard characters to numbers.
Text is a simple one-to-one mapping of characters to numbers. It is very compact. Fifty characters of text translates to fifty bytes of data. It is important to understand that text only contains a simple mapping of characters to numbers. It is not the same as a word processor document such as one created by Microsoft Word or LibreOffice Writer. Those files, in contrast to simple ASCII text, contain many non-text elements that are used to describe its structure and formatting. Plain ASCII text files contain only the characters themselves and a few rudimentary control codes such as tabs, carriage returns and line feeds.
Throughout a Linux system, many files are stored in text format and there are many Linux tools that work with text files. Even Windows recognizes the importance of this format. The well-known NOTEPAD.EXE program is an editor for plain ASCII text files.

Why would we want to examine text files? Because many of the files that contain system settings (called configuration files) are stored in this format, and being able to read them gives us insight about how the system works.

some of the actual programs that the system uses (called scripts) are stored in this format.

<img width="833" height="485" alt="image" src="https://github.com/user-attachments/assets/209cbd92-3f75-4264-b7f5-73a9a99768a8" />

Less Is More
The less program was designed as an improved replacement of an earlier Unix program called more. The name “less” is a play on the phrase “less is more” — a motto of modernist architects and designers.
less falls into the class of programs called “pagers,” programs that allow the easy viewing of long text documents in a page by page manner. Whereas the more program could only page forward, the less program allows paging both forward and backward and has many other features as well.

1.cd into a given directory
2.List the directory contents with ls -l
3.If you see an interesting file, determine its contents with file
4.If it looks like it might be text, try viewing it with less
5.If we accidentally attempt to view a non-text file and it scrambles the terminal window, we can recover by entering the reset command.

Remember the copy and paste trick! If you are using a mouse, you can double click on a filename to copy it and middle click to paste it into commands.

<img width="672" height="198" alt="image" src="https://github.com/user-attachments/assets/e3c763c8-8fdb-429b-82c1-c0abf390a176" />

<img width="444" height="592" alt="image" src="https://github.com/user-attachments/assets/48df7c82-09ff-4f1f-aadb-02c1f36a11ce" />

<img width="442" height="574" alt="image" src="https://github.com/user-attachments/assets/aa230340-00d6-427d-ad91-db25db053ef0" />

<img width="441" height="562" alt="image" src="https://github.com/user-attachments/assets/87be6681-c8f4-4f8c-baee-561e561a8126" />

<img width="445" height="75" alt="image" src="https://github.com/user-attachments/assets/09b44823-c535-4835-bda6-d50ef610042b" />

Symbolic Links
  lrwxrwxrwx 1 root root 11 2007-08-11 07:34 libc.so.6 -> libc-2.6.so

Notice how the first letter of the listing is “l” and the entry seems to have two filenames? This is a special kind of a file called a symbolic link (also known as a soft link or symlink). In most Unix-like systems it is possible to have a file referenced by multiple names. While the value of this might not be obvious, it is really a useful feature.
Picture this scenario: A program requires the use of a shared resource of some kind contained in a file named “foo,” but “foo” has frequent version changes. It would be good to include the version number in the filename so the administrator or other interested party could see what version of “foo” is installed. This presents a problem. If we change the name of the shared resource, we have to track down every program that might use it and change it to look for a new resource name every time a new version of the resource is installed. That doesn't sound like fun at all.

Here is where symbolic links save the day. Suppose we install version 2.6 of “foo,” which has the filename “foo-2.6” and then create a symbolic link simply called “foo” that points to “foo-2.6.” This means that when a program opens the file “foo”, it is actually opening the file “foo-2.6”. Now everybody is happy. The programs that rely on “foo” can find it and we can still see what actual version is installed. When it is time to upgrade to “foo-2.7,” we just add the file to our system, delete the symbolic link “foo” and create a new one that points to the new version. Not only does this solve the problem of the version upgrade, but it also allows us to keep both versions on our machine. Imagine that “foo-2.7” has a bug (damn those developers!) and we need to revert to the old version. Again, we just delete the symbolic link pointing to the new version and create a new symbolic link pointing to the old version.

Hard Links
While we are on the subject of links, we need to mention that there is a second type of link called a hard link. Hard links also allow files to have multiple names, but they do it in a different way.

4 – Manipulating Files and Directories

  ●  cp – Copy files and directories
  ●  mv – Move/rename files and directories
  ●  mkdir – Create directories
  ●  rm – Remove files and directories
  ●  ln – Create hard and symbolic links

Wildcards
  Since the shell uses filenames so much, it provides special characters to help us rapidly specify groups of filenames. These special characters are called wildcards. Using wildcards (which is also known as globbing) allows us to select filenames based on patterns of characters. Table 4-1 lists the wildcards and what they select.
  <img width="935" height="400" alt="image" src="https://github.com/user-attachments/assets/f5ee2975-6655-4419-b9f7-31c7c97d68cf" />
  <img width="930" height="308" alt="image" src="https://github.com/user-attachments/assets/19dd19bf-1f4b-4548-8527-e3d47846f1bf" />

<img width="937" height="214" alt="image" src="https://github.com/user-attachments/assets/dbd38653-0e30-4a80-8d3b-619fe3dbfa12" />
<img width="923" height="437" alt="image" src="https://github.com/user-attachments/assets/3dc6d8fb-b678-4b52-bb93-fa30b535d0a7" />

Character Ranges
If you are coming from another Unix-like environment or have been reading some other books on this subject, you may have encountered the [A-Z] and [a-z] character range notations. These are traditional Unix notations and worked in older versions of Linux as well. They can still work, but you have to be careful with them because they will not produce the expected results unless properly configured. For now, you should avoid using them and use character classes instead.

Dot Files
If we look at our home directory with ls using the -a option we will notice that there are a number of files and directories whose name begin with a dot. As we have discussed, these files are hidden. It’s not a special attribute of the file; it only means that the file will not appear in the output of ls unless the -a or -A options are included. This hidden characteristic also applies to wildcards. Hidden files will not appear unless we use a wildcard pattern such as .*. However, when we do this we will also see both . (the current directory) and .. (the current directory’s parent) in the results. To exclude them we can use patterns such as .[!.]* or .??*.

Wildcards Work in the GUI Too
Wildcards are especially valuable not only because they are used so frequently on the command line, but because they are also supported by some graphical file managers.
●In Nautilus (the file manager for GNOME), you can select files by pressing Ctrl-s and entering a file selection pattern with wildcards and the files in the currently displayed directory will be selected.
●In some versions of Dolphin and Konqueror (the file managers for KDE), you can enter wildcards directly on the location bar. For example, if you want to see all the files starting with a lowercase “u” in the /usr/bin directory, enter “/usr/bin/u*” in the location bar and it will display the result.
Many ideas originally found in the command line interface make their way into the graphical interface, too. It is one of the many things that make the Linux desktop so powerful.

mkdir – Create Directories
  mkdir directory...
A note on notation: When three periods follow an argument in the description of a command (as above), it means that the argument can be repeated, thus the following command:

<img width="640" height="252" alt="image" src="https://github.com/user-attachments/assets/adde77ba-f99a-45e4-bfd6-20543cec7332" />

cp – Copy Files and Directories
  cp item1 item2
copies the single file or directory item1 to the file or directory item2 and the following:
  cp item... directory
copies multiple items (either files or directories) into a directory.

<img width="831" height="369" alt="image" src="https://github.com/user-attachments/assets/17018984-536f-4e99-810f-27ba36d5b767" />
<img width="834" height="342" alt="image" src="https://github.com/user-attachments/assets/4b57fde7-87ca-42ae-9260-2ba474bf5ec0" />

<img width="834" height="544" alt="image" src="https://github.com/user-attachments/assets/d21110e6-4cb9-4157-95fd-15170bedefc4" />

mv – Move and Rename Files
  mv item1 item2
to move or rename the file or directory item1 to item2 or:
  mv item... directory
to move one or more items from one directory to another.

<img width="842" height="364" alt="image" src="https://github.com/user-attachments/assets/a91a3765-6a94-421e-92f7-7337514d8234" />

<img width="830" height="300" alt="image" src="https://github.com/user-attachments/assets/34a893e1-a292-422b-bbe4-d21c85d5497a" />
<img width="837" height="156" alt="image" src="https://github.com/user-attachments/assets/bb07e7d5-69d9-47fd-85db-4731c46c583c" />

rm – Remove Files and Directories
  rm item...
where item is one or more files or directories.

<img width="827" height="424" alt="image" src="https://github.com/user-attachments/assets/ceed087d-d03c-45b3-a108-239fdd60770c" />
<img width="832" height="80" alt="image" src="https://github.com/user-attachments/assets/42b292f0-4778-45cc-ba23-76e9007411c7" />
<img width="828" height="276" alt="image" src="https://github.com/user-attachments/assets/aeb4c908-e4e1-4108-826f-fb255ea6d81c" />

Be Careful with rm!
Unix-like operating systems such as Linux do not have an undelete command. Once you delete something with rm, it's gone. Linux assumes you're smart and you know what you're doing.
Be particularly careful with wildcards. Consider this classic example. Let's say you want to delete just the HTML files in a directory. To do this, you type the following:
rm *.html
This is correct, but if you accidentally place a space between the * and the .html like so:
rm * .html
the rm command will delete all the files in the directory and then complain that there is no file called .html.
Here is a useful tip: whenever you use wildcards with rm (besides carefully checking your typing!), test the wildcard first with ls. This will let you see the files that will be deleted. Then press the up arrow key to recall the command and replace ls with rm.

ln – Create Links
  ln file link
The following creates a symbolic link:
  ln -s item link
to create a symbolic link where item is either a file or a directory.

Hard Links
Hard links are the original Unix way of creating links, compared to symbolic links, which are more modern. By default, every file has a single hard link that gives the file its name. When we create a hard link, we create an additional directory entry for a file. Hard links have two important limitations:
1.A hard link cannot reference a file outside its own file system. This means a link cannot reference a file that is not on the same disk partition as the link itself.
2.A hard link may not reference a directory.
A hard link is indistinguishable from the file itself. Unlike a symbolic link, when we list a directory containing a hard link we will see no special indication of the link. When a hard link is deleted, the link is removed but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted.
It is important to be aware of hard links because you might encounter them from time to time, but modern practice prefers symbolic links, which we will cover next.

Symbolic Links
Symbolic links were created to overcome the limitations of hard links. Symbolic links work by creating a special type of file that contains a text pointer to the referenced file or directory. In this regard, they operate in much the same way as a Windows shortcut, though of course they predate the Windows feature by many years.
A file pointed to by a symbolic link, and the symbolic link itself are largely indistinguishable from one another. For example, if we write something to the symbolic link, the referenced file is written to. However when we delete a symbolic link, only the link is deleted, not the file itself. If the file is deleted before the symbolic link, the link will continue to exist but will point to nothing. In this case, the link is said to be broken. In many implementations, the ls command will display broken links in a distinguishing color, such as red, to reveal their presence.

<img width="410" height="216" alt="image" src="https://github.com/user-attachments/assets/46a384fd-ea67-4a80-ab66-456904907877" />
<img width="236" height="146" alt="image" src="https://github.com/user-attachments/assets/4dfece3a-58c5-491a-b469-640fe5fbd7a2" />
<img width="379" height="193" alt="image" src="https://github.com/user-attachments/assets/ac5ac98b-11a8-440f-9c92-46c3d7f55172" />
<img width="263" height="60" alt="image" src="https://github.com/user-attachments/assets/573ec08b-0256-4cca-9967-df33f1b8b9d3" />
<img width="268" height="50" alt="image" src="https://github.com/user-attachments/assets/d2abfdb1-eff6-4802-bf87-15148612b32a" />
<img width="367" height="243" alt="image" src="https://github.com/user-attachments/assets/28d538b5-3427-4294-bed9-f35f0022cbc5" />
<img width="372" height="344" alt="image" src="https://github.com/user-attachments/assets/e400f4dc-cf58-43ba-ade7-656c8fb21c31" />
<img width="251" height="198" alt="image" src="https://github.com/user-attachments/assets/bba3b065-e230-4c84-aaee-3ba5b250a14b" />
<img width="241" height="102" alt="image" src="https://github.com/user-attachments/assets/15471dd4-46d3-4387-b3bc-e62da92ed4a9" />

<img width="362" height="205" alt="image" src="https://github.com/user-attachments/assets/2e54afe8-5c67-4ca7-9422-edea06e8f789" />

<img width="242" height="147" alt="image" src="https://github.com/user-attachments/assets/30a0fd44-0302-4d3c-afa6-f3d8a7157a5d" />

<img width="244" height="200" alt="image" src="https://github.com/user-attachments/assets/6b24e96a-ad29-4819-ad9a-424fd33776b2" />

<img width="399" height="120" alt="image" src="https://github.com/user-attachments/assets/d1cc3f7f-f8cc-4c81-9bee-17a5a186ddc5" />

One thing we notice is that both the second fields in the listings for fun and fun-hard contain a 4 which is the number of hard links that now exist for the file. Remember that a file will always have at least one link because the file's name is created by a link. So, how do we know that fun and fun-hard are, in fact, the same file? In this case, ls is not very helpful. While we can see that fun and fun-hard are both the same size (field 5), our listing provides no way to be sure. To solve this problem, we're going to have to dig a little deeper.
When thinking about hard links, it is helpful to imagine that files are made up of two parts.
1.The data part containing the file's contents.
2.The name part that holds the file's name.
When we create hard links, we are actually creating additional name parts that all refer to the same data part. The system assigns a chain of disk blocks to what is called an inode, which is then associated with the name part. Each hard link therefore refers to a specific inode containing the file's contents.

The ls command has a way to reveal this information. It is invoked with the -i option.

<img width="475" height="119" alt="image" src="https://github.com/user-attachments/assets/5087013a-baa5-467b-ab44-7e1db3d0c41f" />

In this version of the listing, the first field is the inode number and, as we can see, both fun and fun-hard share the same inode number, which confirms they are the same file.

Symbolic links were created to overcome the two disadvantages of hard links.
  1.Hard links cannot span physical devices.
  2.Hard links cannot reference directories, only files.
Symbolic links are a special type of file that contains a text pointer to the target file or directory.

<img width="480" height="380" alt="image" src="https://github.com/user-attachments/assets/547477ea-8284-4e45-b530-5c3cb8456544" />

<img width="471" height="197" alt="image" src="https://github.com/user-attachments/assets/96516c9f-d728-4728-929b-fde0f67e8ac5" />

<img width="468" height="185" alt="image" src="https://github.com/user-attachments/assets/3243105c-5b7e-4c5d-81d4-408543d9c784" />

<img width="467" height="181" alt="image" src="https://github.com/user-attachments/assets/ae3d8ef9-6769-48f6-a671-1f1eb2dca0a0" />
<img width="284" height="59" alt="image" src="https://github.com/user-attachments/assets/a9b232e1-2c07-40cf-895c-275835891ce0" />

<img width="365" height="134" alt="image" src="https://github.com/user-attachments/assets/af9bd1a0-3f3d-47d1-bb03-5aa7eec18e16" />

<img width="664" height="159" alt="image" src="https://github.com/user-attachments/assets/9a40f86f-947f-4491-b0cf-c285b3a1568f" />

5 – Working with Commands
  ●  type – Indicate how a command name is interpreted
  ●  which – Display which executable program will be executed
  ●  help – Get help for shell builtins
  ●  man – Display a command's manual page
  ●  apropos – Display a list of appropriate commands
  ●  info – Display a command's info entry
  ●  whatis – Display one-line manual page descriptions
  ●  alias – Create an alias for a command

What Exactly Are Commands?
A command can be one of four different things:
  1.An executable program like all those files we saw in /usr/bin. Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in scripting languages such as the shell, Perl, Python, Ruby, and so on.
  2.A command built into the shell itself. bash supports a number of commands internally called shell builtins. The cd command, for example, is a shell builtin.
  3.A shell function. Shell functions are miniature shell scripts incorporated into the environment. We will cover configuring the environment and writing shell functions in later chapters, but for now, just be aware that they exist.
  4.An alias. Aliases are commands that we can define ourselves, built from other commands.

type – Display a Command's Type
  The type command is a shell builtin that displays the kind of command the shell will execute, given a particular command name.
<img width="282" height="182" alt="image" src="https://github.com/user-attachments/assets/baa68ff0-98b8-4f78-9a3f-c382e1701e29" />
ls command is actually an alias for the ls command with the “--color=tty” option added. Now we know why the output from ls is displayed in color!

which – Display an Executable's Location
  Sometimes there is more than one version of an executable program installed on a system. While this is not common on desktop systems, it's not unusual on large servers. To determine the exact location of a given executable, the which command is used. 

<img width="255" height="187" alt="image" src="https://github.com/user-attachments/assets/a239f549-577c-4296-8b46-34c09776f4d7" />

which only works for executable programs, not builtins nor aliases that are substitutes for actual executable programs. When we try to use which on a shell builtin for example, cd, we either get no response or get an error message

help – Get Help for Shell Builtins

<img width="332" height="120" alt="image" src="https://github.com/user-attachments/assets/50a6e677-b8e7-4fb2-a8ca-10572a32cb0a" />

A note on notation: When square brackets appear in the description of a command's syntax, they indicate optional items. A vertical bar character indicates mutually exclusive items. In the case of the cd command above:
cd [-L|[-P[-e]]] [dir]
This notation says that the command cd may be followed optionally by either a “-L” or a “-P” and further, if the “-P” option is specified the “-e” option may also be included followed by the optional argument “dir”.

Helpful hint: By using the help command with the -m option, help will display its output in an alternate format.

--help – Display Usage Information

<img width="632" height="401" alt="image" src="https://github.com/user-attachments/assets/470125c2-bdf2-4d51-82d0-f8ef3bbcb98f" />

man – Display a Program's Manual Page
  Most executable programs intended for command line use provide a formal piece of documentation called a manual or man page. A special paging program called man is used to view them.
  Man pages vary somewhat in format but generally contain the following:
•A title (the page’s name)
•A synopsis of the command's syntax
•A description of the command's purpose
•A listing and description of each of the command's options
Man pages, however, do not usually include examples, and are intended as a reference, not a tutorial.

<img width="647" height="538" alt="image" src="https://github.com/user-attachments/assets/e7e60f65-cbce-4b45-a49a-9953f7313856" />
<img width="842" height="400" alt="image" src="https://github.com/user-attachments/assets/d0c567e8-a321-4f98-9cd5-668fdd77ea03" />

Sometimes we need to refer to a specific section of the manual to find what we are looking for. This is particularly true if we are looking for a file format that is also the name of a command. Without specifying a section number, we will always get the first instance of a match, probably in section 1. To specify a section number, we use man like this:
  
  man section search_term
<img width="177" height="52" alt="image" src="https://github.com/user-attachments/assets/37bffed9-5bcf-48b4-aad3-c99bde969fce" />
<img width="638" height="537" alt="image" src="https://github.com/user-attachments/assets/3ccc1584-da38-42db-8c61-a922b41c9206" />

apropos – Display Appropriate Commands
  It is also possible to search the list of man pages for possible matches based on a search term. It's crude but sometimes helpful.
<img width="645" height="404" alt="image" src="https://github.com/user-attachments/assets/dafafffc-694c-41a4-abd5-4991e776af7d" />

Note that the man command with the “-k” option performs the same function as apropos.

whatis – Display One-line Manual Page Descriptions
  The whatis program displays the name and a one-line description of a man page matching a specified keyword
<img width="397" height="61" alt="image" src="https://github.com/user-attachments/assets/5de399bc-a72c-454c-a105-69ab36cbd1da" />

The Most Brutal Man Page Of Them All
As we have seen, the manual pages supplied with Linux and other Unix-like systems are intended as reference documentation and not as tutorials. Many man pages are hard to read, but I think that the grand prize for difficulty has got to go to the man page for bash. As I was doing research for this book, I gave the bash man page careful review to ensure that I was covering most of its topics. When printed, it's more than 80 pages long and extremely dense, and its structure makes absolutely no sense to a new user.
On the other hand, it is very accurate and concise, as well as being extremely complete. So check it out if you dare and look forward to the day when you can read it and it all makes sense.

info – Display a Program's Info Entry
  The GNU Project provides an alternative to man pages for their programs, called “info.” Info manuals are displayed with a reader program named, appropriately enough, info. Info pages are hyperlinked much like web pages.
<img width="653" height="467" alt="image" src="https://github.com/user-attachments/assets/e7b2c9d3-9366-47ad-b48f-02f9937fd39d" />

The info program reads info files, which are tree structured into individual nodes, each containing a single topic. Info files contain hyperlinks that can move the reader from node to node. A hyperlink can be identified by its leading asterisk and is activated by placing the cursor upon it and pressing the Enter key.

<img width="832" height="349" alt="image" src="https://github.com/user-attachments/assets/1afe9503-073a-4230-8db8-93833852493c" />
<img width="835" height="92" alt="image" src="https://github.com/user-attachments/assets/170fe6ff-cb75-4673-82d7-c82efc0ba7b1" />

Most of the command line programs we have discussed so far are part of the GNU Project's coreutils package

README and Other Program Documentation Files
Many software packages installed on our system have documentation files residing in the /usr/share/doc directory. Most of these are stored in plain text format and can be viewed with less. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a “.gz” extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless that will display the contents of gzip-compressed text files.

It's possible to put more than one command on a line by separating each command with a semicolon. It works like this:
command1; command2; command3...
<img width="593" height="89" alt="image" src="https://github.com/user-attachments/assets/958359b2-74c5-4fc8-aff6-f0ca219a75f6" />

<img width="648" height="274" alt="image" src="https://github.com/user-attachments/assets/ddabdbce-04b6-4807-8fb2-63470ab4b1d1" />
<img width="297" height="55" alt="image" src="https://github.com/user-attachments/assets/fc920b25-4fb3-4b6d-b6de-2639637bdd9e" />
<img width="171" height="105" alt="image" src="https://github.com/user-attachments/assets/afe24dfd-c731-438d-8183-b693e79a575a" />

<img width="289" height="284" alt="image" src="https://github.com/user-attachments/assets/a2de8833-dfc7-4eeb-9956-324c3e82167a" />

While we purposefully avoided naming our alias with an existing command name, it is not uncommon to do so. This is often done to apply a commonly desired option to each invocation of a common command.
To see all the aliases defined in the environment, use the alias command without arguments. Here are some of the aliases defined by default on a Fedora system

There is one tiny problem with defining aliases on the command line. They vanish when our shell session ends.

6 – Redirection
  The “I/O” stands for input/output and with this facility we can redirect the input and output of commands to and from files, as well as connect multiple commands together into powerful command pipelines.
  ●  cat – Concatenate files
  ●  sort – Sort lines of text
  ●  uniq – Report or omit repeated lines
  ●  grep – Print lines matching a pattern
  ●  wc – Print newline, word, and byte counts for each file
  ●  head – Output the first part of a file
  ●  tail – Output the last part of a file
  ●  tee – Read from standard input and write to standard output and files
Many of the programs that we have used so far produce output of some kind. This output often consists of two types:
•The program's results, that is, the data the program is designed to produce
•Status and error messages that tell us how the program is getting along
Keeping with the Unix theme of “everything is a file,” programs such as ls actually send their results to a special file called standard output (often expressed as stdout) and their status messages to another file called standard error (stderr). By default, both standard output and standard error are linked to the screen and not saved into a disk file.

In addition, many programs take input from a facility called standard input (stdin), which is, by default, attached to the keyboard.
I/O redirection allows us to change where output goes and where input comes from. Normally, output goes to the screen and input comes from the keyboard, but with I/O redirection, we can change that.

To redirect standard output to another file instead of the screen, we use the > redirection operator followed by the name of the file. Why would we want to do this? It's often useful to store the output of a command in a file.
<img width="456" height="144" alt="image" src="https://github.com/user-attachments/assets/6831ee73-6c99-4dfb-982f-e3661a8bf038" />
<img width="611" height="534" alt="image" src="https://github.com/user-attachments/assets/bf4656fe-3f98-4b8e-8d7c-a3ad4cdeb18e" />
<img width="468" height="66" alt="image" src="https://github.com/user-attachments/assets/27091e16-edd7-407e-a60e-547a5d64e7c1" />

why was the error message displayed on the screen rather than being redirected to the file ls-output.txt? The answer is that the ls program does not send its error messages to standard output. Instead, like most well-written Unix programs, it sends its error messages to standard error (stderr). Since we only redirected standard output and not standard error, the error message was still sent to the screen.

<img width="418" height="50" alt="image" src="https://github.com/user-attachments/assets/c62c6a66-694d-4e2e-8683-4ef19e64da7a" />
The file now has zero length! This is because when we redirect output with the “>” redirection operator, the destination file is always rewritten from the beginning. Since our ls command generated no results and only an error message, the redirection operation started to rewrite the file and then stopped because of the error, resulting in its truncation.
if we ever need to actually truncate a file (or create a new, empty file), we can use a trick like this:
<img width="475" height="275" alt="image" src="https://github.com/user-attachments/assets/8e3ab118-b0fa-4fc8-b0a1-9719e882268c" />
Simply using the redirection operator with no command preceding it will truncate an existing file or create a new, empty file.
how can we append redirected output to a file instead of overwriting the file from the beginning?
<img width="458" height="199" alt="image" src="https://github.com/user-attachments/assets/34de5322-a4f7-48cf-91cf-54fb949dee8b" />

what if we could treat the sequence as a single entity with a single output stream? We can do this by creating a group command. To do this, we surround our sequence with brace characters
<img width="558" height="106" alt="image" src="https://github.com/user-attachments/assets/20adc3bd-34b3-4439-8e7d-f933a60ec97d" />
<img width="556" height="104" alt="image" src="https://github.com/user-attachments/assets/6776599b-19f6-479a-9357-3de872efbde4" />
With our sequence surrounded by braces, the shell will consider it a single command in terms of redirection. Note that the shell requires whitespace around the braces and the final command in the sequence must be terminated with either a semicolon or a newline

Redirecting Standard Error
Redirecting standard error lacks the ease of a dedicated redirection operator. To redirect standard error we must refer to its file descriptor. A program can produce output on any of several numbered file streams. While we have referred to the first three of these file streams as standard input, output and error, the shell references them internally as file de
scriptors 0, 1, and 2, respectively. The shell provides a notation for redirecting files using the file descriptor number. Since standard error is the same as file descriptor number 2, we can redirect standard error with this notation
<img width="287" height="40" alt="image" src="https://github.com/user-attachments/assets/d7bfd7d4-7050-4b53-9eae-9fc99c8e87a7" />

The file descriptor “2” is placed immediately before the redirection operator to perform the redirection of standard error to the file ls-error.txt.

Redirecting Standard Output and Standard Error to One File
There are cases in which we may want to capture all of the output of a command to a single file. To do this, we must redirect both standard output and standard error at the same time. There are two ways to do this. Shown here is the traditional way, which works with old versions of the shell
<img width="322" height="43" alt="image" src="https://github.com/user-attachments/assets/e1290099-573e-46d6-af5b-b2f309cfcb67" />

Using this method, we perform two redirections. First we redirect standard output to the file ls-output.txt and then we redirect file descriptor 2 (standard error) to file descriptor 1 (standard output) using the notation 2>&1.
<img width="318" height="93" alt="image" src="https://github.com/user-attachments/assets/004affdc-d026-4090-b251-e20c93575b95" />

Notice that the order of the redirections is significant. The redirection of standard error must always occur after redirecting standard output or it doesn't work. The following example redirects standard error to the file ls-output.txt:
  >ls-output.txt 2>&1
However, if the order is changed to the following, standard error is directed to the screen.
  2>&1 >ls-output.txt

Recent versions of bash provide a second, more streamlined method for performing this combined redirection shown here
<img width="321" height="88" alt="image" src="https://github.com/user-attachments/assets/84581529-ce65-43d8-861a-3331a65efa17" />

We can also append the standard output and standard error streams to a single file like so:
<img width="301" height="134" alt="image" src="https://github.com/user-attachments/assets/1f525e74-e903-418c-9864-16c4e2417a72" />

Disposing of Unwanted Output
Sometimes “silence is golden,” and we don't want output from a command, we just want to throw it away. This applies particularly to error and status messages. The system provides a way to do this by redirecting output to a special file called “/dev/null”. This file is a system device often referred to as a bit bucket, which accepts input and does nothing with it. To suppress error messages from a command, we do this:
<img width="406" height="216" alt="image" src="https://github.com/user-attachments/assets/9223ddd9-ecbb-4b77-91b0-8c52f3d3a7ba" />

/dev/null In Unix Culture
The bit bucket is an ancient Unix concept and because of its universality, it has appeared in many parts of Unix culture. When someone says he/she is sending your comments to /dev/null, now you know what it means. For more examples, see the Wikipedia article on /dev/null .

Redirecting Standard Input
Up to now, we haven't encountered any commands that make use of standard input (actually we have, but we’ll reveal that surprise a little bit later), so we need to introduce one

cat – Concatenate Files
The cat command reads one or more files and copies them to standard output. In most cases, we can think of cat as being analogous to the TYPE command in DOS. We can use it to display files without paging.
<img width="454" height="76" alt="image" src="https://github.com/user-attachments/assets/f6439801-58aa-47c6-8a38-30b4f2a51c38" />

cat is often used to display short text files. Since cat can accept more than one file as an argument, it can also be used to join files together. Say we have downloaded a large file that has been split into multiple parts (multimedia files are often split this way on Usenet), and we want to join them back together.

If cat is not given any arguments, it reads from standard input and since standard input is, by default, attached to the keyboard, it's waiting for us to type something! Try adding the following text and pressing Enter:
Next, type a Ctrl-d (i.e., hold down the Ctrl key and press “d”) to tell cat that it has reached end of file (EOF) on standard input:
<img width="670" height="160" alt="image" src="https://github.com/user-attachments/assets/e41d9db4-bfa8-4e60-ab1d-ce4da220ba54" />

<img width="376" height="130" alt="image" src="https://github.com/user-attachments/assets/3dc1d1c8-cde1-4014-adc6-c32250ab3737" />

<img width="371" height="57" alt="image" src="https://github.com/user-attachments/assets/db26c121-ded5-4a78-81ee-159c268d448c" />

Using the command line, we have implemented the world's dumbest word processor!

Pipelines
The capability of commands to read data from standard input and send to standard output is utilized by a shell feature called pipelines. Using the pipe operator | (vertical bar), the standard output of one command can be piped into the standard input of another.
  command1 | command2

To fully demonstrate this, we are going to need some commands. Remember how we said there was one we already knew that accepts standard input? It's less. We can use less to display, page by page, the output of any command that sends its results to standard output:
<img width="223" height="43" alt="image" src="https://github.com/user-attachments/assets/ce6d1342-2f43-451b-91f0-2afcf0ac1aea" />

This is extremely handy! Using this technique, we can conveniently examine the output of any command that produces standard output

The Difference Between > and |
At first glance, it may be hard to understand the redirection performed by the pipeline operator | versus the redirection operator >. Simply put, the redirection operator connects a command with a file, while the pipeline operator connects the output of one command with the input of a second command.
command1 > file1
command1 | command2
A lot of people will try the following when they are learning about pipelines, “just to see what happens”:
command1 > command2
Answer: sometimes something really bad.
Here is an actual example submitted by a reader who was administering a Linux-based server appliance. As the superuser, he did this:
# cd /usr/bin
# ls > less
The first command put him in the directory where most programs are stored and the second command told the shell to overwrite the file less with the output of the ls command. Since the /usr/bin directory already contained a file named less (the less program), the second command overwrote the less program file with the text from ls, thus destroying the less program on his system.
The lesson here is that the > redirection operator silently creates or overwrites files, so you need to treat it with a lot of respect.

Filters
Pipelines are often used to perform complex operations on data. It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as filters. Filters take input, change it somehow, and then output it.

The first one we will try is sort. Imagine we wanted to make a combined list of all the executable programs in /bin and /usr/bin, put them in sorted order and view the resulting list
<img width="298" height="38" alt="image" src="https://github.com/user-attachments/assets/53065553-7fa4-45f8-9557-e0e36c552df3" />
Since we specified two directories (/bin and /usr/bin), the output of ls would have consisted of two sorted lists, one for each directory. By including sort in our pipeline, we changed the data to produce a single, sorted list.
sort is a powerful command with many features and options.

uniq - Report or Omit Repeated Lines
The uniq command is often used in conjunction with sort. uniq accepts a sorted list of data from either standard input or a single filename argument (see the uniq man page for details) and, by default, removes any duplicates from the list. So, to make sure our list has no duplicates (that is, any programs of the same name that appear in both the /bin and /usr/bin directories), we will add uniq to our pipeline
<img width="342" height="46" alt="image" src="https://github.com/user-attachments/assets/a092a52c-d881-4cc5-87fb-70874d9fb0a4" />

we use uniq to remove any duplicates from the output of the sort command. If we want to see the list of duplicates instead, we add the “-d” option to uniq like so
<img width="375" height="42" alt="image" src="https://github.com/user-attachments/assets/25f6170a-4d7f-4956-bd59-29e4a03ef918" />

<img width="275" height="563" alt="image" src="https://github.com/user-attachments/assets/672d07a3-67a1-405e-ab78-2b90dc76f6ed" />
<img width="252" height="561" alt="image" src="https://github.com/user-attachments/assets/748afa71-b0d7-40ca-827e-f94331bece96" />

wc – Print Line, Word, and Byte Counts
The wc (word count) command is used to display the number of lines, words, and bytes contained in files.
<img width="241" height="63" alt="image" src="https://github.com/user-attachments/assets/8410867b-29b1-4805-aedb-326a7b07bdb6" />
In this case, it prints out three numbers: lines, words, and bytes contained in ls-output.txt.
<img width="343" height="52" alt="image" src="https://github.com/user-attachments/assets/5c5b5a5c-aca3-484c-b2ad-87d164fbcba3" />

grep – Print Lines Matching a Pattern
grep is a powerful program used to find text patterns within files. It's used like this:
grep pattern [file...]
When grep encounters a “pattern” in the file, it prints out the lines containing it. The patterns that grep can match can be very complex, but for now we will concentrate on simple text matches.
Let's say we wanted to find all the files in our list of programs that had the word zip embedded in the name. Such a search might give us an idea of some of the programs on our system that had something to do with file compression.
<img width="366" height="404" alt="image" src="https://github.com/user-attachments/assets/1cdb16db-bcf2-4906-84de-09c0fbd348ad" />
Here are a few handy options for grep:
  •  -i, causes grep to ignore case when performing the search (normally searches are case sensitive)
  •  -l, causes grep to only output the names of the files containing text that matches the pattern.
  •  -v, causes grep to print only those lines that do not match the pattern.
  •  -w, causes grep to only match whole words.

head / tail – Print First / Last Part of Files
  Sometimes we don't want all the output from a command. We may only want the first few lines or the last few lines. The head command prints the first ten lines of a file, and the tail command prints the last ten lines. While both commands print ten lines of text by default, this can be adjusted with the -n option
<img width="416" height="296" alt="image" src="https://github.com/user-attachments/assets/04d26765-c623-47b2-8ebd-371e28e28db6" />
These commands can be used in pipelines as well:
<img width="260" height="123" alt="image" src="https://github.com/user-attachments/assets/2ead7567-9044-4e6c-93ac-1e628d5ce64d" />

Using the -n option with head and tail together allows us to cut an excerpt from the middle of a file. Let’s imagine we have a text file with a 5 line header and a 5 line footer that we want to remove leaving only the “good” part in the middle containing the data.
<img width="426" height="83" alt="image" src="https://github.com/user-attachments/assets/328f5146-ff62-4746-9eeb-3ae49300eb8e" />
The -n option when used with head allows a negative value which causes all but the last n lines to be output. Similarly, the -n option with tail allows a plus sign causing all but the first n lines to be output.

tail also has an option which allows us to follow the contents of a file in real time. This is useful for watching the progress of log files as they are being written. In the following example, we will look at the messages file in /var/log (or the /var/log/syslog file if messages is missing). Superuser privileges may be required to do this on some Linux distributions because log files may contain security information
<img width="634" height="72" alt="image" src="https://github.com/user-attachments/assets/8cec148f-1d5d-4d66-83f6-c705114c6aeb" />
<img width="603" height="215" alt="image" src="https://github.com/user-attachments/assets/43d6ddf0-4abb-4094-974e-f912d51b5c97" />

tee – Read from Stdin and Output to Stdout and Files
In keeping with our plumbing metaphor, Linux provides a command called tee which creates a “tee” fitting on our pipe. The tee program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files. This is useful for capturing a pipeline's contents at an intermediate stage of processing.

<img width="331" height="488" alt="image" src="https://github.com/user-attachments/assets/6e6d5742-9b55-4ee5-89f2-383887ba1ee2" />
<img width="295" height="537" alt="image" src="https://github.com/user-attachments/assets/72dc4283-475d-4907-8fbc-39ca1a1bb4a3" />
did this through root

Linux Is About Imagination
When I am asked to explain the difference between Windows and Linux, I often use a toy analogy.
Windows is like a Game Boy. You go to the store and buy one all shiny new in the box. You take it home, turn it on, and play with it. Pretty graphics, cute sounds. After a while, though, you get tired of the game that came with it, so you go back to the store and buy another one. This cycle repeats over and over. Finally, you go back to the store and say to the person behind the counter, “I want a game that does this!” only to be told that no such game exists because there is no “market demand” for it. Then you say, “But I only need to change this one thing!” The person behind the counter says you can't change it. The games are all sealed up in their cartridges. You discover that your toy is limited to the games others have decided that you need.
Linux, on the other hand, is like the world's largest Erector Set. You open it, and it's just a huge collection of parts. There's a lot of steel struts, screws, nuts, gears, pulleys, motors, and a few suggestions on what to build. So, you start to play with it. You build one of the suggestions and then another. After a while you discover that you have your own ideas of what to make. You don't ever have to go back to the store, as you already have everything you need. The Erector Set takes on the shape of your imagination. It does what you want.
Your choice of toys is, of course, a personal thing, so which toy would you find more satisfying?

7 – Seeing the World as the Shell Sees It
  ●  echo – Display a line of text
**Expansion**
Each time we type a command and press the Enter key, bash performs several substitutions upon the text before it carries out our command.
for example *, can have a lot of meaning to the shell. The process that makes this happen is called expansion. With expansion, we enter something and it is expanded into something else before the shell acts upon it.
<img width="655" height="147" alt="image" src="https://github.com/user-attachments/assets/f5d6992e-c20c-4e10-bc88-4d4a6222d308" />
Why didn't echo print *? As we recall from our work with wildcards, the * character means match any characters in a filename, but what we didn't see in our original discussion was how the shell does that. The simple answer is that the shell expands the * into something else (in this instance, the names of the files in the current working directory) before the echo command is executed.

Pathname Expansion
The mechanism by which wildcards work is called pathname expansion.
<img width="545" height="347" alt="image" src="https://github.com/user-attachments/assets/59e1af58-78eb-480c-9508-adf7be9bed53" />

Pathname Expansion of Hidden Files
As we know, filenames that begin with a period character are hidden. Pathname expansion also respects this behavior. An expansion such as the following does not reveal hidden files.
echo *
It might appear at first glance that we could include hidden files in an expansion by starting the pattern with a leading period, like this:
echo .*
It almost works. However, if we examine the results closely, we will see that the names . and .. will also appear in the results. Because these names refer to the current working directory and its parent directory, using this pattern will likely produce an incorrect result. We can see this if we try the following command:
ls -d .* | less
To better perform pathname expansion in this situation, we have to employ a more specific pattern.
echo .[!.]*
This pattern expands into every filename that begins with only one period followed by any other characters. This will work correctly with most hidden files (though it still won't include filenames with multiple leading periods). The ls command with the -A option (“almost all”) will provide a correct listing of hidden files.
ls -A
<img width="654" height="494" alt="image" src="https://github.com/user-attachments/assets/5a12f61f-045c-423e-a1da-a462f6dd8de4" />
<img width="530" height="391" alt="image" src="https://github.com/user-attachments/assets/a139d928-b80d-4f07-b311-cc0cf9a0b80f" />

Tilde Expansion
As we may recall from our introduction to the cd command, the tilde character (~) has a special meaning. When used at the beginning of a word, it expands into the name of the home directory of the named user or, if no user is named, the home directory of the current user
<img width="211" height="65" alt="image" src="https://github.com/user-attachments/assets/c813bdc6-5060-4046-84db-b9b19e1fd47f" />

Arithmetic Expansion
The shell allows arithmetic to be performed by expansion.

<img width="201" height="120" alt="image" src="https://github.com/user-attachments/assets/3759218c-3e6a-4342-b7cf-52de66f99073" />
Arithmetic expansion supports only integers (whole numbers, no decimals) but can perform quite a number of different operations.

<img width="837" height="345" alt="image" src="https://github.com/user-attachments/assets/5b6e32d1-604b-4c3a-9ec5-d7aefd86a563" />
Arithmetic expansion uses the following form:
$((expression))

<img width="241" height="115" alt="image" src="https://github.com/user-attachments/assets/7c29b91b-c5d8-4e33-ba93-aa46bfae2e19" />

<img width="350" height="118" alt="image" src="https://github.com/user-attachments/assets/9a62d64e-e1c3-44e5-a0fc-b2be9529142a" />

Brace Expansion
Perhaps the strangest expansion is called brace expansion. With it, we can create multiple text strings from a pattern containing braces

<img width="485" height="373" alt="image" src="https://github.com/user-attachments/assets/dd2ea9e9-8892-4a2e-b825-5742ae4ef946" />
So, what is this good for? The most common application is making lists of files or directories to be created
<img width="646" height="364" alt="image" src="https://github.com/user-attachments/assets/b0897481-bbcc-4074-8837-d4b589d06682" />

Parameter Expansion
It's a feature that is more useful in shell scripts than directly on the command line. Many of its capabilities have to do with the system's ability to store small chunks of data and to give each chunk a name. Many such chunks, more properly called variables, are available for our examination. For example, the variable named USER contains our username.

<img width="222" height="108" alt="image" src="https://github.com/user-attachments/assets/5578e144-3037-48e5-afe0-68aeb21a3255" />
<img width="367" height="92" alt="image" src="https://github.com/user-attachments/assets/117c5fa1-fb91-4c8c-b88e-165a77636f14" />
<img width="239" height="112" alt="image" src="https://github.com/user-attachments/assets/876b7b52-aa8e-42b5-a2ee-6d9bacb20c18" />

Command Substitution
Command substitution allows us to use the output of a command as an expansion.

<img width="614" height="142" alt="image" src="https://github.com/user-attachments/assets/aa887999-196c-4bb1-a2b6-ab5042b12fa5" /> 
Here we passed the results of which cp as an argument to the ls command, thereby getting the listing of the cp program without having to know its full pathname. We are not limited to just simple commands. Entire pipelines can be used

<img width="658" height="500" alt="image" src="https://github.com/user-attachments/assets/76cfd6ec-0110-47c4-a63f-65a8405183d4" />
In this example, the results of the pipeline became the argument list of the file command.
There is an alternate syntax for command substitution used by older shell programs that is also supported in bash. It uses backquotes instead of the dollar sign and parentheses.

<img width="458" height="59" alt="image" src="https://github.com/user-attachments/assets/759baa7e-0ce1-4e03-a608-c1113f99f7e1" />

Quoting
Now that we've seen how many ways the shell can perform expansions, it's time to learn how we can control it.

<img width="360" height="123" alt="image" src="https://github.com/user-attachments/assets/4449b45d-8ff3-41c2-9d13-4725afb4ea8f" />
In the first example, word-splitting by the shell removed extra whitespace from the echo command's list of arguments. In the second example, parameter expansion substituted an empty string for the value of $1 because it was an undefined variable. The shell provides a mechanism called quoting to selectively suppress unwanted expansions.

Double Quotes
The first type of quoting we will look at is double quotes. If we place text inside double quotes, all the special characters used by the shell lose their special meaning and are treated as ordinary characters. The exceptions are $, \ (backslash), and ` (back-quote). This means that word-splitting, pathname expansion, tilde expansion, and brace expansion are suppressed, but parameter expansion, arithmetic expansion, and command substitution are still carried out. Using double quotes, we can cope with filenames containing embedded spaces.

<img width="461" height="253" alt="image" src="https://github.com/user-attachments/assets/f95bc0a3-736e-4df0-b0ad-a0910b3d93eb" />
<img width="649" height="278" alt="image" src="https://github.com/user-attachments/assets/9a5b138d-0c5e-4690-941e-699dfacb64d7" />
<img width="288" height="121" alt="image" src="https://github.com/user-attachments/assets/5ef743d5-8e34-4898-a851-1472b21ea816" />

The fact that newlines are considered delimiters by the word-splitting mechanism causes an interesting, albeit subtle, effect on command substitution.

<img width="659" height="484" alt="image" src="https://github.com/user-attachments/assets/dcc49d94-abf0-4c8e-b855-211aeae9b100" />
In the first instance, the unquoted command substitution resulted in a command line containing 49 arguments. In the second, it resulted in a command line with one argument that includes the embedded spaces and newlines.

Single Quotes
If we need to suppress all expansions, we use single quotes. Here is a comparison of unquoted, double quotes, and single quotes:

<img width="655" height="196" alt="image" src="https://github.com/user-attachments/assets/4ff94886-0f3e-44be-b389-7f0eddc32138" />
As we can see, with each succeeding level of quoting, more and more of the expansions are suppressed.

Escaping Characters
Sometimes we want to quote only a single character. To do this, we can precede a character with a backslash, which in this context is called the escape character. Often this is done inside double quotes to selectively prevent an expansion.

<img width="417" height="58" alt="image" src="https://github.com/user-attachments/assets/e3ff7b15-b8ab-4f4c-998a-fc7a5732b230" />

It is also common to use escaping to eliminate the special meaning of a character in a filename. For example, it is possible to use characters in filenames that normally have special meaning to the shell. These would include $, !, &, spaces, and others. To include a special character in a filename we can do this:
mv bad\&filename good_filename

To allow a backslash character to appear, escape it by typing \\. Note that within single quotes, the backslash loses its special meaning and is treated as an ordinary character.
Another use of the backslash escape is suppressing aliases. For example, assuming the ls command is aliased to ls=’ls --color=auto’, the default on many Linux distributions, we can precede the command with a backslash and the alias will be ignored and the ls command will be executed without the color option.

Backslash Escape Sequences
In addition to its role as the escape character, the backslash is also used as part of a notation to represent certain special characters called control codes. The first 32 characters in the ASCII coding scheme are used to transmit commands to teletype-like devices. Some of these codes are familiar (tab, backspace, linefeed, and carriage return), while others are not (null, end-of-transmission, and acknowledge).

<img width="707" height="289" alt="image" src="https://github.com/user-attachments/assets/42e525f4-baf1-4f7f-8c43-0e9a8bbb1a4b" />
The table above lists some of the common backslash escape sequences. The idea behind this representation using the backslash originated in the C programming language and has been adopted by many others, including the shell.
Adding the -e option to echo will enable interpretation of escape sequences. You may also place them inside $' '. Here, using the sleep command, a simple program that just waits for the specified number of seconds and then exits, we can create a primitive countdown timer:
sleep 10; echo -e "Time's up\a"
We could also do this:
sleep 10; echo "Time's up" $'\a'

Without a proper understanding of expansion, the shell will always be a source of mystery and confusion, with much of its potential power wasted.

8 – Advanced Keyboard Tricks
  ●  clear – Clear the screen
  ●  history – Display the contents of the history list

Command Line Editing
bash uses a library (a shared collection of routines that different programs can use) called Readline to implement command line editing.
Think of these as additional tools that we can employ in our work. It’s not important to learn all of them, but many of them are very useful. Pick and choose as desired.

Note: Some of the key sequences below (particularly those that use the Alt key) may be intercepted by the GUI for other functions. All of the key sequences should work properly when using a virtual console.

Cursor Movement
The following table lists the keys used to move the cursor:
<img width="777" height="313" alt="image" src="https://github.com/user-attachments/assets/54ffa3bf-5b61-42bd-ae04-14b68de7db02" />

Modifying Text
Since we might make a mistake when composing a command, we need a way to correct them efficiently.
<img width="836" height="363" alt="image" src="https://github.com/user-attachments/assets/34a1737e-981e-4215-ae6b-3ae179526d3a" />

Cutting and Pasting (Killing and Yanking) Text
The Readline documentation uses the terms killing and yanking to refer to what we would commonly call cutting and pasting. Items that are cut are stored in a buffer (a temporary storage area in memory) called the kill-ring
<img width="786" height="329" alt="image" src="https://github.com/user-attachments/assets/681f2762-a0a3-4bea-a968-8e91ad448c2d" />

The Meta Key
If you venture into the Readline documentation, which can be found in the “READLINE” section of the bash man page, you will encounter the term meta key. On modern keyboards this maps to the Alt key but it wasn't always so.
Back in the dim times (before PCs but after Unix), not everybody had their own computer. What they might have had was a device called a terminal. A terminal was a communication device that featured a text display screen and a keyboard and just enough electronics inside to display text characters and move the cursor around. It was attached (usually by serial cable) to a larger computer or the communication network of a larger computer. There were many different brands of terminals, and they all had different keyboards and display feature sets. Since they all tended to at least understand ASCII, software developers wanting portable applications wrote to the lowest common denominator. Unix systems have an elaborate way of dealing with terminals and their different display features. Since the developers of Readline could not be sure of the presence of a dedicated extra control key, they invented one and called it meta. While the Alt key serves as the meta key on modern keyboards, you can also press and release the Esc key to get the same effect as holding down the Alt key if you're using a terminal (which you can still do in Linux!).

Completion
Another way that the shell can help us is through a mechanism called completion. Completion occurs when we press the tab key while typing a command.
While this example shows completion of pathnames, which is its most common use, completion will also work on variables (if the beginning of the word is a $), user names (if the word begins with ~), commands (if the word is the first word on the line) and hostnames (if the beginning of the word is @). Hostname completion works only for hostnames listed in /etc/hosts.
<img width="425" height="126" alt="image" src="https://github.com/user-attachments/assets/cd0176d4-5d80-4869-b410-2c6c459f433b" />

There are a number of control and meta key sequences that are associated with completion
<img width="807" height="234" alt="image" src="https://github.com/user-attachments/assets/0d8e88a2-aea1-48ab-85bc-66a71cfcc8c0" />
There are quite a few more that are rather obscure. A list appears in the bash man page under “READLINE”.

Programmable Completion
Recent versions of bash have a facility called programmable completion. Programmable completion allows you (or more likely, your distribution provider) to add additional completion rules. Usually this is done to add support for specific applications. For example, it is possible to add completions for the option list of a command or match particular file types that an application supports. Ubuntu has a fairly large set defined by default. Programmable completion is implemented by shell functions, a kind of mini shell script that we will cover in later chapters. If you are curious, try the following:
set | less
and see if you can find them. Not all distributions include them by default.

Using History
bash maintains a history of commands that have been entered. This list of commands is kept in our home directory in a file called .bash_history. The history facility is a useful resource for reducing the amount of typing we have to do, especially when combined with command line editing.

Searching History
At any time, we can view the contents of the history list by doing the following:
<img width="166" height="46" alt="image" src="https://github.com/user-attachments/assets/d7d80213-b92b-4244-a7f4-b7eaf9c9f06b" />
<img width="281" height="536" alt="image" src="https://github.com/user-attachments/assets/b39ce5f3-2869-42c3-989e-5be15aa10786" />

By default, most modern Linux distributions configure bash to store the last 1000 commands we have entered. We will see how to adjust this value

let's say that among our results we got a line containing an interesting command like this:
88 ls -l /usr/bin > ls-output.txt
The 88 is the line number of the command in the history list. We could use this immediately using another type of expansion called history expansion.
<img width="301" height="95" alt="image" src="https://github.com/user-attachments/assets/d1ff9c0b-d48d-4fd2-94f8-a6b73b3d9085" />

bash also provides the ability to search the history list incrementally. This means we can tell bash to search the history list as we enter characters, with each additional character further refining our search. To start incremental search press Ctrl-r followed by the text we are looking for. When we find it, we can either press Enter to execute the command or press Ctrl-j to copy the line from the history list to the current command line. To find the next occurrence of the text (moving “up” the history list), press Ctrl-r again. To quit searching, press either Ctrl-g or Ctrl-c.
<img width="291" height="155" alt="image" src="https://github.com/user-attachments/assets/f39a8816-af00-4c31-af7a-a01ebc5ef9fe" />
<img width="839" height="525" alt="image" src="https://github.com/user-attachments/assets/0425d8d6-0061-4c07-80f4-69772caf2f2a" />

History Expansion
The shell offers a specialized type of expansion for items in the history list by using the ! character. We have already seen how the exclamation point can be followed by a number to insert an entry from the history list. There are a number of other expansion features, as described in Table
<img width="817" height="264" alt="image" src="https://github.com/user-attachments/assets/52098944-0c5d-445c-9d97-d05f8015aed4" />

Use caution with the !string and !?string forms unless youyou are absolutely sure of the contents of the history list items. We can mitigate this problem somewhat by appending “:p” to our expansion. This tells the shell to print the result of the expansion and place it into the command history.
<img width="288" height="288" alt="image" src="https://github.com/user-attachments/assets/0d8cc9e2-cea9-4f2f-aa3b-5bc3f9ad7f9e" />

script
In addition to the command history feature in bash, most Linux distributions include a program called script that can be used to record an entire shell session and store it in a file. The basic syntax of the command is as follows:
script [file]
where file is the name of the file used for storing the recording. If no file is specified, the file typescript is used. See the script man page for a complete list of the program’s options and features.

9 – Permissions
Operating systems in the Unix tradition differ from those in the MS-DOS tradition in that they are not only multitasking systems, but also multi-user systems. It means that more than one person can be using the computer at the same time.
if a computer is attached to a network or the Internet, remote users can log in via ssh (secure shell) and operate the computer
multi-user capability of Linux is not a recent "innovation," but rather a feature that is deeply embedded into the design of the operating system.
A typical university computer system, for example, consisted of a large central computer located in one building and terminals that were located throughout the campus, each connected to the large central computer.
To make this practical, a method had to be devised to protect the users from each other. After all, the actions of one user could not be allowed to crash the computer, nor could one user interfere with the files belonging to another use. we will look at this essential part of system security
  ●  id – Display user identity
  ●  chmod – Change a file's mode
  ●  umask – Set the default file permissions
  ●  su – Run a shell as another user
  ●  sudo – Execute a command as another user
  ●  chown – Change a file's owner
  ●  chgrp – Change a file's group ownership
  ●  addgroup – Add a user or a group to the system
  ●  usermod – Modify a user account
  ●  passwd – Change a user's password
we may have encountered a problem when trying to examine a file such as /etc/shadow
<img width="368" height="113" alt="image" src="https://github.com/user-attachments/assets/5e69ab1f-86b4-4f68-8127-259ef9cb4634" />

In the Unix security model, a user may own files and directories. When a user owns a file or directory, the user has control over its access. Users can, in turn, belong to a group consisting of one or more users who are given access to files and directories by their owners. In addition to granting access to a group, an owner may also grant some set of access rights to everybody, which are called others (sometimes referred to as the world). To find information about our identity, we use the id command.
<img width="654" height="82" alt="image" src="https://github.com/user-attachments/assets/0384cef5-1da9-496b-b054-1d014c6a668a" />

User accounts are defined in the /etc/passwd file and groups are defined in the /etc/group file. When user accounts and groups are created, these files are modified along with /etc/shadow which holds information about the user's password. For each user account, the /etc/passwd file defines the user (login) name, uid, gid, user’s real name, home directory, and login shell. If we examine the contents of /etc/passwd and /etc/group, we notice that besides the regular user accounts, there are accounts for the superuser (always uid 0) and various other system users. when we cover processes, we will see that some of these other “users” are, in fact, quite busy.
While many Unix-like systems assign regular users to a common group such as “users”, modern Linux practice is to create a unique, single-member group with the same name as the user. This makes certain types of permission assignment easier.

Reading, Writing, and Executing
Access rights to files and directories are defined in terms of read access, write access, and execution access.
<img width="374" height="117" alt="image" src="https://github.com/user-attachments/assets/b0b472cf-e84a-43fb-8f4f-47419a549dda" />
The first 10 characters of the listing are the file attributes. The first of these characters is the file type.
<img width="833" height="224" alt="image" src="https://github.com/user-attachments/assets/08797f5c-b1a6-47fe-add0-3bf4caf8a0c5" />
<img width="775" height="190" alt="image" src="https://github.com/user-attachments/assets/2ce1bfa6-cf9e-406a-9eb7-c93e5bfef92d" />
The remaining nine characters of the file attributes, called the file mode, represent the read, write, and execute permissions for the file's owner, the file's group owner, and everybody else.
<img width="451" height="118" alt="image" src="https://github.com/user-attachments/assets/b5efc33d-fbe8-40bf-956f-6704d569f0b5" />
<img width="852" height="582" alt="image" src="https://github.com/user-attachments/assets/1d290d6e-1861-457b-a21e-7e27540088e9" /> .. to the directory

<img width="658" height="601" alt="image" src="https://github.com/user-attachments/assets/fe67bd7f-dcbf-48e1-a711-578bfc5551de" />

chmod – Change File Mode
To change the mode (permissions) of a file or directory, the chmod command is used. Be aware that only the file’s owner or the superuser can change the mode of a file or directory. chmod supports two distinct ways of specifying mode changes: octal number representation, or symbolic representation.

What the Heck is Octal?
Octal (base 8), and its cousin, hexadecimal (base 16) are number systems often used to express numbers on computers. We humans, owing to the fact that we (or at least most of us) were born with 10 fingers, count using a base 10 number system. Computers, on the other hand, were born with only one finger and thus do all their counting in binary (base 2). Their number system has only two numerals, 0 and 1. So, in binary, counting looks like this:
0, 1, 10, 11, 100, 101, 110, 111, 1000, 1001, 1010, 1011...
In octal, counting is done with the numerals zero through seven, like so:
0, 1, 2, 3, 4, 5, 6, 7, 10, 11, 12, 13, 14, 15, 16, 17, 20, 21...
Hexadecimal counting uses the numerals zero through nine plus the letters “A” through “F”:
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, 10, 11, 12, 13...
While we can see the sense in binary (since computers have only one finger), what are octal and hexadecimal good for? The answer has to do with human convenience. Many times, small portions of data are represented on computers as bit patterns. Take for example an RGB color. On most computer displays, each pixel is composed of three color components: eight bits of red, eight bits of green, and eight bits of blue. A lovely medium blue would be a 24 digit number:
010000110110111111001101
How would you like to read and write those kinds of numbers all day? I didn't think so. Here's where another number system would help. Each digit in a hexadecimal number represents four digits in binary. In octal, each digit represents three binary digits. So our 24 digit medium blue could be condensed to a six-digit hexadecimal number:
436FCD
Since the digits in the hexadecimal number “line up” with the bits in the binary number, we can see that the red component of our color is 43, the green 6F, and the blue CD.
These days, hexadecimal notation (often referred to as “hex”) is more common than octal, but as we will soon see, octal's ability to express three bits of binary will be very useful...

With octal notation, we use octal numbers to set the pattern of desired permissions. Since each digit in an octal number represents three binary digits, this maps nicely to the scheme used to store the file mode.

<img width="773" height="431" alt="image" src="https://github.com/user-attachments/assets/fbcf0fb3-a414-4df6-9802-6852a165f180" />

<img width="363" height="238" alt="image" src="https://github.com/user-attachments/assets/03c8f78a-9236-4ae9-a645-178fff6eb7a2" />

By passing the argument “600”, we were able to set the permissions of the owner to read and write while removing all permissions from the group owner and others. Though remembering the octal to binary mapping may seem inconvenient, we will usually have only to use a few common ones: 7 (rwx), 6 (rw-), 5 (r-x), 4 (r--), and 0 (---)

chmod also supports a symbolic notation for specifying file modes. Symbolic notation is divided into three parts.
  •  Who the change will affect
  •  Which operation will be performed
  •  What permission will be set.
To specify who is affected, a combination of the characters “u”, “g”, “o”, and “a” is used
<img width="933" height="271" alt="image" src="https://github.com/user-attachments/assets/fce85611-53c2-4c20-ae2c-15cc3d4b90f4" />

If no character is specified, “all” will be assumed. The operation may be a “+” indicating that a permission is to be added, a “-” indicating that a permission is to be taken away, or a “=” indicating that only the specified permissions are to be applied and that all others are to be removed.
Permissions are specified with the “r”, “w”, and “x” characters.
<img width="929" height="538" alt="image" src="https://github.com/user-attachments/assets/22821c9e-ba7d-4bb4-a29f-7c6fc2287817" />

Some people prefer to use octal notation, and some folks really like the symbolic. Symbolic notation does offer the advantage of allowing us to set a single attribute without disturbing any of the others.

A word of caution regarding the “--recursive” option: it acts on both files and directories, so it's not as useful as we would hope since we rarely want files and directories to have the same permissions.

umask – Set Default Permissions
The umask command controls the default permissions given to a file when it is created. It uses octal notation to express a mask of bits to be removed from a file's mode attributes.
<img width="377" height="238" alt="image" src="https://github.com/user-attachments/assets/e05a617e-e75e-45e8-9e5d-8a8c14aa18eb" />
We first removed any old copy of foo.txt to make sure we were starting fresh. Next, we ran the umask command without an argument to see the current value. It responded with the value 0002 (the value 0022 is another common default value), which is the octal representation of our mask. We next create a new instance of the file foo.txt and observe its permissions.
We can see that both the user and group get read and write permission, while everyone else only gets read permission. The reason that world does not have write permission is because of the value of the mask.
<img width="374" height="217" alt="image" src="https://github.com/user-attachments/assets/1fe7f50f-946e-41a0-bcc4-1346bed234ec" />
When we set the mask to 0000 (effectively turning it off), we see that the file is now world writable. To understand how this works, we have to look at octal numbers again. If we change the mask to 0002, expand it into binary, and then compare it to the attributes
<img width="623" height="141" alt="image" src="https://github.com/user-attachments/assets/b955471d-8597-4ff0-8295-86af54d7fbd5" />

Ignore for the moment the leading zeros (we'll get to those in a minute) and observe that where the 1 appears in our mask, an attribute was removed — in this case, the world write permission. That's what the mask does. Everywhere a 1 appears in the binary value of the mask, an attribute is unset. If we look at a mask value of 0022
<img width="619" height="129" alt="image" src="https://github.com/user-attachments/assets/3df94ca1-b29a-44c4-8745-72123ccb6e88" />
Most of the time we won't have to change the mask; the default provided by the distribution will be fine. In some high-security situations, however, we will want to control it.

Some Special Permissions
Though we usually see an octal permission mask expressed as a three-digit number, it is more technically correct to express it in four digits. Why? Because, in addition to read, write, and execute permission, there are some other, less used, permission settings.
The first of these is the setuid bit (octal 4000). When applied to an executable file, it sets the effective user ID from that of the real user (the user actually running the program) to that of the program's owner. Most often this is given to a few programs owned by the superuser. When an ordinary user runs a program that is “setuid root” , the program runs with the effective privileges of the superuser. This allows the program to access files and directories that an ordinary user would normally be prohibited from accessing. Clearly, because this raises security concerns, the number of setuid programs must be held to an absolute minimum.
The second less-used setting is the setgid bit (octal 2000), which, like the setuid bit, changes the effective group ID from the real group ID of the real user to that of the file owner. If the setgid bit is set on a directory, newly created files in the directory will be given the group ownership of the directory rather the group ownership of the file's creator. This is useful in a shared directory when members of a common group need access to all the files in the directory, regardless of the file owner's primary group.
The third is called the sticky bit (octal 1000). This is a holdover from ancient Unix, where it was possible to mark an executable file as “not swappable.” On files, Linux ignores the sticky bit, but if applied to a directory, it prevents users from deleting or renaming files unless the user is either the owner of the directory, the owner of the file, or the superuser. This is often used to control access to a shared directory, such as /tmp.
Here are some examples of using chmod with symbolic notation to set these special permissions. Here’s an example of assigning setuid to a program:
chmod u+s program
Next, here’s and example of assigning setgid to a directory:
chmod g+s dir
Finally, here’s an example of assigning the sticky bit to a directory:
chmod +t dir
When viewing the output from ls, you can determine the special permissions. Here are some examples. First, an example of a program that is setuid:
-rwsr-xr-x
Here’s an example of a directory that has the setgid attribute:
drwxrwsr-x
Here’s an example of a directory with the sticky bit set:
drwxrwxrwt

Often we want to gain superuser privileges to carry out some administrative task, but it is also possible to “become” another regular user for such things as testing an account. There are three ways to take on an alternate identity.
  1.  Log out and log back in as the alternate user.
  2.  Use the su command.
  3.  Use the sudo command.

From within our own shell session, the su command allows us to assume the identity of another user and either start a new shell session with that user's ID, or to issue a single command as that user. The sudo command allows an administrator to set up a configuration file called /etc/sudoers and define specific commands that particular users are permitted to execute under an assumed identity. The choice of which command to use is largely determined by which Linux distribution you use. Be aware that the use of su is falling out of favor in modern Linux distributions.

su – Run a Shell with Substitute User and Group IDs
The su command is used to start a shell as another user. The command syntax looks like this:
su [-[l]] [user]
If the “-l” option is included, the resulting shell session is a login shell for the specified user. This means the user's environment is loaded and the working directory is changed to the user's home directory. This is usually what we want. If the user is not specified, the superuser is assumed. Notice that (strangely) the -l may be abbreviated as -, which is how it is most often used. Assuming that the root account has a password set (which is not the custom in modern distributions) we can start a shell for the superuser this way

<img width="224" height="73" alt="image" src="https://github.com/user-attachments/assets/4fd5a2e0-ef01-451f-b4c6-84bd17948b6c" />

It is also possible to execute a single command rather than starting a new interactive command by using su this way.
su -c 'command'
Using this form, a single command line is passed to the new shell for execution. It is important to enclose the command in quotes, as we do not want expansion to occur in our shell, but rather in the new shell

<img width="506" height="143" alt="image" src="https://github.com/user-attachments/assets/969c3603-345b-43f2-bf17-a629bf1b424c" />


sudo – Execute a Command as Another User
The sudo command is like su in many ways but has some important additional capabilities. The administrator can configure sudo to allow an ordinary user to execute commands as a different user (usually the superuser) in a controlled way. In particular, a user may be restricted to one or more specific commands and no others. Another important difference is that the use of sudo does not require access to the superuser's password. Authenticating using sudo, requires the user’s own password
<img width="319" height="74" alt="image" src="https://github.com/user-attachments/assets/2bf90e24-2704-493d-8607-527231a9e617" />
After entering the command, we are prompted for our password (not the superuser's) and once the authentication is complete, the specified command is carried out. One important difference between su and sudo is that sudo does not start a new shell, nor does it load another user's environment. This means that commands do not need to be quoted any differently than they would be without using sudo. Note that this behavior can be overridden by specifying various options. Note, too, that sudo can be used to start an interactive superuser session (much like su -) by using the -i option.
To see what privileges are granted by sudo, use the -l option to list them
<img width="659" height="169" alt="image" src="https://github.com/user-attachments/assets/0ac7ffd9-2023-4be0-a0d7-f4a03576037b" />
<img width="182" height="77" alt="image" src="https://github.com/user-attachments/assets/33461aaf-8613-44ef-9be5-a4d257deb18c" />


Modern Linux Distributions and sudo
One of the recurrent problems for regular users is how to perform certain tasks that require superuser privileges. These tasks include installing and updating software, editing system configuration files, and accessing devices. In the Windows world, this is often done by giving users administrative privileges. This allows users to perform these tasks. However, it also enables programs executed by the user to have the same abilities. This is desirable in most cases, but it also permits malware (malicious software) such as viruses to have free rein of the computer.
In the Unix world, there has always been a larger division between regular users and administrators, owing to the multiuser heritage of Unix. The approach taken in Unix is to grant superuser privileges only when needed. To do this, the su and sudo commands are commonly used.
Years ago, most Linux distributions relied on su for this purpose. su didn't require the configuration that sudo required, and having a root account is traditional in Unix. This, however introduced a problem. Users were tempted to operate as root unnecessarily. In fact, some users operated their systems as the root user exclusively, since it does away with all those annoying “permission denied” messages. This is how you reduce the security of a Linux system to that of a Windows system. Not a good idea.
When Ubuntu was introduced, its creators took a different tack. By default, Ubuntu disables logins to the root account (by failing to set a password for the account) and instead uses sudo to grant superuser privileges. The initial user account is granted full access to superuser privileges via sudo and may grant similar powers to subsequent user accounts. This method of granting privileges is now the accepted standard is most modern distributions.

chown – Change File Owner and Group
The chown command is used to change the owner and group owner of a file or directory. Superuser privileges are required to use this command.

chown [owner][:[group]] file...

chown can change the file owner and/or the file group owner depending on the first argument of the command.
<img width="998" height="430" alt="image" src="https://github.com/user-attachments/assets/3e990c1f-c97c-41f7-a746-b516a90d0389" />
Let's say we have two users; janet, who has access to superuser privileges and tony, who does not. User janet wants to copy a file from her home directory to the home directory of user tony. Since user janet wants tony to be able to edit the file, janet changes the ownership of the copied file from janet to tony.
<img width="502" height="471" alt="image" src="https://github.com/user-attachments/assets/e15f3ead-b9f0-4ea8-84e8-4f2fcdcbfaef" />

Notice that after the first use of sudo, janet was not prompted for her password. This is because sudo, in most configurations, “trusts” us for several minutes until its timer

chgrp – Change Group Ownership
In older versions of Unix, the chown command only changed file ownership, not group ownership. For that purpose, a separate command, chgrp was used. It works much the same way as chown, except for being more limited.

Exercising Our Privileges
We are going to demonstrate the solution to a common problem — setting up a shared directory. revisit our friends janet and tony. They both have music collections and want to set up a shared directory, where they will each store their music files as Ogg Vorbis or MP3. As before, user janet has access to superuser privileges via sudo.
A group needs to be created that will have both janet and tony as members. This is done in two steps. First, using the groupadd command, we create the group followed with the usermod command to add users to the group.
The options used with the usermod command are short for --append and --group and they add the specified user to the corresponding group in the /etc/group file.
Next, janet creates the directory for the music files.
Since janet is manipulating files outside of her home directory, superuser privileges are required. After the directory is created, it has the following ownerships and permissions
As we can see, the directory is owned by root and has permission mode 755. To make this directory shareable, janet needs to change the group ownership and the group permissions to allow writing.
Using the chown command, janet sets the group owner of the directory to music then uses chmod to set the directory permissions to 2755. This sets the setguid to cause all files in the directory to inherit the same group ownership as the directory. We did this by executing chmod 2755 but we could have done thing by using the symbolic method with chmod g+s.
What does this all mean? It means that we now have a directory, /usr/local/share/Music that is owned by root and allows read and write access to group music. Group music has members janet and tony; thus, janet and tony can create files in directory /usr/local/share/Music. Other users can list the contents of the directory but cannot create files there.
But we still have a problem. The default umask on this system is 0022, which prevents group members from writing files belonging to other members of the group. This would not be a problem if the shared directory contained only files, but since this directory will store music, and music is usually organized in a hierarchy of artists and albums, members of the group will need the ability to create files and directories inside directories created by other members. We need to change the umask used by janet and tony to 0002 instead.
janet sets her umask to 0002, and creates a new test file and directory
Both files and directories are now created with the correct permissions to allow all members of the group music to create files and directories inside the Music directory.
The one remaining issue is umask. The necessary setting only lasts until the end of session and must be reset.
<img width="273" height="119" alt="image" src="https://github.com/user-attachments/assets/7f7e6129-205f-43c9-91c4-f9240c5eecd4" />
<img width="409" height="514" alt="image" src="https://github.com/user-attachments/assets/9b8b13f9-cbc0-41e1-b160-3437ef102826" />
<img width="513" height="514" alt="image" src="https://github.com/user-attachments/assets/2f850616-8ad5-49fa-8876-e4fe35c72bfa" />
<img width="472" height="299" alt="image" src="https://github.com/user-attachments/assets/be8dcd7c-1120-4ac4-996d-fe050b332c50" />

Changing Your Password
setting passwords for ourselves (and for other users if we have access to superuser privileges). To set or change a password, the passwd command is used. The command syntax looks like this:
passwd [user]
<img width="328" height="167" alt="image" src="https://github.com/user-attachments/assets/720d465a-ea4c-40a0-8373-554159562b19" />
The passwd command will try to enforce use of “strong” passwords.
If we have superuser privileges, you can specify a username as an argument to the passwd command to set the password for another user. Other options are available to the superuser to allow account locking, password expiration, and so on. See the passwd man page for details

The passwd, addgroup, and usermod commands are part of a suite of commands in the shadow-utils package
<img width="878" height="427" alt="image" src="https://github.com/user-attachments/assets/8d454135-cc47-4ffa-9e4d-e2347ece5115" />

10 – Processes
Modern operating systems are usually multitasking, meaning they create the illusion of doing more than one thing at once by rapidly switching from one executing program to another. The Linux kernel manages this through the use of processes. Processes are how Linux organizes the different programs waiting for their turn at the CPU
In this chapter, we will look at some of the tools available at the command line that let us examine what programs are doing and how to terminate processes that are misbehaving.
  ●  ps – Report a snapshot of current processes
  ●  top – Display tasks
  ●  jobs – List active jobs
  ●  bg – Place a job in the background
  ●  fg – Place a job in the foreground
  ●  kill – Send a signal to a process
  ●  killall – Kill processes by name
  ●  nice - Run a program with modified scheduling priority
  ●  renice - Alter priority of running processes
  ●  nohup - Run a command immune to hangups
  ●  halt/poweroff/reboot - Halt, power-off, or reboot the system
  ●  shutdown – Shutdown or reboot the system

How a Process Works
When a system starts up, the kernel initiates a few of its own activities as processes and launches a program called init. init, in turn, starts systemd which starts all the system services. In older Linux distributions init runs a series of shell scripts (located in /etc) called init scripts to perform a similar function. Many system services are implemented as daemon programs, programs that just sit in the background and do their thing without having any user interface. So, even if we are not logged in, the system is at least a little busy performing routine stuff
The fact that a program can launch other programs is expressed in the process scheme as a parent process producing a child process.
The kernel maintains information about each process to help keep things organized. For example, each process is assigned a number called a process ID (PID). PIDs are assigned in ascending order, with init always getting PID 1. The kernel also keeps track of the memory assigned to each process, as well as the processes' readiness to resume execution. Like files, processes also have owners and user IDs, effective user IDs, etc.
Viewing Processes
The most commonly used tool to view processes (there are several) is the ps command. The ps program has a lot of options
<img width="259" height="97" alt="image" src="https://github.com/user-attachments/assets/25520815-ae36-4a8b-8a56-3a2f2413b2f5" />
The result in this example lists two processes, process 5198 and process 10129, which are bash and ps respectively. As we can see, by default, ps doesn't show us very much, just the processes associated with the current terminal session.

