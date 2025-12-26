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
