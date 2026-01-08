<h2>2 – Navigation</h2>
<div>
  <ul type=bullets>
  <li/>  pwd – Print name of current working directory
  <li/>  cd – Change directory
  <li/>  ls – List directory contents
  </ul>

Like Windows, a Unix-like operating system such as Linux organizes its files in what is called a hierarchical directory structure.
This means they are organized in a tree-like pattern of directories (sometimes called folders in other systems), which may contain files and other directories. The first directory in the file system is called the root directory.

Note that unlike Windows, which has a separate file system tree for each storage device, Unix-like systems such as Linux always have a single file system tree, regardless of how many drives or storage devices are attached to the computer. Storage devices are attached (or more correctly, mounted) at various points on the tree according to the whims of the system administrator, the person (or people) responsible for the maintenance of the system.

At any given time, we are inside a single directory and we can see the files contained in the directory and the pathway to the directory above us (called the parent directory) and any subdirectories below us. The directory we are standing in is called the current working directory. To display the current working directory, we use the pwd (print working directory) command.
<br>
<img width="212" height="52" alt="image" src="https://github.com/user-attachments/assets/3c989ff5-43af-4daa-b343-5ad898e67b74" />
<br>
<img width="603" height="60" alt="image" src="https://github.com/user-attachments/assets/9f0115d9-f4d4-49c6-9350-7d3b14c0617c" />
<br>
To change our working directory (where we are standing in our tree-shaped maze) we use the cd command

We can specify pathnames in one of two different ways; as absolute pathnames or as relative pathnames.
<br>
<img width="211" height="105" alt="image" src="https://github.com/user-attachments/assets/10418d35-007c-4a1f-989d-a02900f7dd52" />
<br>
Where an absolute pathname starts from the root directory and leads to its destination, a relative pathname starts from the working directory. To do this, it uses a couple of special notations to represent relative positions in the file system tree. These special notations are "." (dot) and ".." (dot dot).

"." notation refers to the working directory and the ".." notation refers to the working directory's parent directory. Here is how it works.
<br>
<img width="224" height="255" alt="image" src="https://github.com/user-attachments/assets/57f784df-2fed-42c3-a4dc-5121efe976e0" />
<br>
<img width="941" height="330" alt="image" src="https://github.com/user-attachments/assets/d2426546-4b46-4b47-b374-5b58abe709ea" />
<br>
<h6>Important Facts About Filenames</h6>
On Linux systems, files are named in a manner similar to other systems such as Windows, but there are some important differences.
  <ol type=numbers>
  <li/> Filenames that begin with a period character are hidden. This only means that ls will not list them unless you say ls -a. When your account was created, several hidden files were placed in your home directory to configure things for your account. In Chapter 11 we will take a closer look at some of these files to see how you can customize your environment. In addition, some applications place their configuration and settings files in your home directory as hidden files.
  <li/> Filenames and commands in Linux, like Unix, are case sensitive. The filenames “File1” and “file1” refer to different files.
  <li/> Linux has no concept of a “file extension” like some other operating systems. You may name files any way you like. The contents and/or purpose of a file is determined by other means. Although Unix-like operating systems don’t use file extensions to determine the contents/purpose of files, many application programs do.
  <li/> Though Linux supports long filenames that may contain embedded spaces and punctuation characters, limit the punctuation characters in the names of files you create to period, dash, and underscore. Most importantly, do not embed spaces in filenames. If you want to represent spaces between words in a filename, use underscore characters. You will thank yourself later.
  
 
