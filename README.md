# linux-notes
My notes for learning linux

1 – What Is the Shell?

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

<img width="263" height="68" alt="image" src="https://github.com/user-attachments/assets/3982117f-0748-442c-b9b4-f836d38799b8" />

<img width="496" height="51" alt="image" src="https://github.com/user-attachments/assets/441259af-2109-47bd-8340-d7ad89b0bb61" />

To see the current amount of free space on our disk drives, enter df

<img width="510" height="200" alt="image" src="https://github.com/user-attachments/assets/eae4e4f8-646b-4a78-9c3b-00816dcef5b0" />

to display the amount of free memory, enter the free command
<img width="670" height="90" alt="image" src="https://github.com/user-attachments/assets/1f12ecf9-7386-48cb-a6c2-591e226dcbd6" />

Even if we have no terminal emulator running, several terminal sessions continue to run behind the graphical desktop. We can access these sessions, called virtual terminals or virtual consoles, by pressing Ctrl-Alt-F1 through Ctrl-Alt-F6 on most Linux distributions. When a session is accessed, it presents a login prompt into which we can enter our username and password. To switch from one virtual console to another, press Alt-F1 through Alt-F6. On most system we can return to the graphical desktop by pressing Alt-F7

2 – Navigation
  ●  pwd – Print name of current working directory
  ●  cd – Change directory
  ●  ls – List directory contents

Like Windows, a Unix-like operating system such as Linux organizes its files in what is called a hierarchical directory structure.
This means they are organized in a tree-like pattern of directories (sometimes called folders in other systems), which may contain files and other directories. The first directory in the file system is called the root directory.

Note that unlike Windows, which has a separate file system tree for each storage device, Unix-like systems such as Linux always have a single file system tree, regardless of how many drives or storage devices are attached to the computer. Storage devices are attached (or more correctly, mounted) at various points on the tree according to the whims of the system administrator, the person (or people) responsible for the maintenance of the system.

At any given time, we are inside a single directory and we can see the files contained in the directory and the pathway to the directory above us (called the parent directory) and any subdirectories below us. The directory we are standing in is called the current working directory. To display the current working directory, we use the pwd (print working directory) command.

<img width="212" height="52" alt="image" src="https://github.com/user-attachments/assets/3c989ff5-43af-4daa-b343-5ad898e67b74" />

 <img width="603" height="60" alt="image" src="https://github.com/user-attachments/assets/9f0115d9-f4d4-49c6-9350-7d3b14c0617c" />

To change our working directory (where we are standing in our tree-shaped maze) we use the cd command

We can specify pathnames in one of two different ways; as absolute pathnames or as relative pathnames.

<img width="211" height="105" alt="image" src="https://github.com/user-attachments/assets/10418d35-007c-4a1f-989d-a02900f7dd52" />

Where an absolute pathname starts from the root directory and leads to its destination, a relative pathname starts from the working directory. To do this, it uses a couple of special notations to represent relative positions in the file system tree. These special notations are "." (dot) and ".." (dot dot).

"." notation refers to the working directory and the ".." notation refers to the working directory's parent directory. Here is how it works.

<img width="224" height="255" alt="image" src="https://github.com/user-attachments/assets/57f784df-2fed-42c3-a4dc-5121efe976e0" />

<img width="941" height="330" alt="image" src="https://github.com/user-attachments/assets/d2426546-4b46-4b47-b374-5b58abe709ea" />

Important Facts About Filenames
On Linux systems, files are named in a manner similar to other systems such as Windows, but there are some important differences.
  1.Filenames that begin with a period character are hidden. This only means that ls will not list them unless you say ls -a. When your account was created, several hidden files were placed in your home directory to configure things for your account. In Chapter 11 we will take a closer look at some of these files to see how you can customize your environment. In addition, some applications place their configuration and settings files in your home directory as hidden files.
  2.Filenames and commands in Linux, like Unix, are case sensitive. The filenames “File1” and “file1” refer to different files.
  3.Linux has no concept of a “file extension” like some other operating systems. You may name files any way you like. The contents and/or purpose of a file is determined by other means. Although Unix-like operating systems don’t use file extensions to determine the contents/purpose of files, many application programs do.
  4.Though Linux supports long filenames that may contain embedded spaces and punctuation characters, limit the punctuation characters in the names of files you create to period, dash, and underscore. Most importantly, do not embed spaces in filenames. If you want to represent spaces between words in a filename, use underscore characters. You will thank yourself later.
  
  
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

<img width="397" height="209" alt="image" src="https://github.com/user-attachments/assets/26ad3146-84a1-4406-840f-d51cdba61370" />





