4 – Manipulating Files and Directories
<ul type=bullets>
  <li/>  cp – Copy files and directories
  <li/>  mv – Move/rename files and directories
  <li/>  mkdir – Create directories
  <li/>  rm – Remove files and directories
  <li/>  ln – Create hard and symbolic links
</ul>
<h6>Wildcards</h6>
  Since the shell uses filenames so much, it provides special characters to help us rapidly specify groups of filenames. These special characters are called wildcards. Using wildcards (which is also known as globbing) allows us to select filenames based on patterns of characters. Table 4-1 lists the wildcards and what they select.
<br>  
<img width="935" height="400" alt="image" src="https://github.com/user-attachments/assets/f5ee2975-6655-4419-b9f7-31c7c97d68cf" />
<br>
<img width="930" height="308" alt="image" src="https://github.com/user-attachments/assets/19dd19bf-1f4b-4548-8527-e3d47846f1bf" />
<br>
<img width="937" height="214" alt="image" src="https://github.com/user-attachments/assets/dbd38653-0e30-4a80-8d3b-619fe3dbfa12" />
<br>
<img width="923" height="437" alt="image" src="https://github.com/user-attachments/assets/3dc6d8fb-b678-4b52-bb93-fa30b535d0a7" />
<br>
<h6>Character Ranges</h6>
If you are coming from another Unix-like environment or have been reading some other books on this subject, you may have encountered the [A-Z] and [a-z] character range notations. These are traditional Unix notations and worked in older versions of Linux as well. They can still work, but you have to be careful with them because they will not produce the expected results unless properly configured. For now, you should avoid using them and use character classes instead.

<h6>Dot Files</h6>
If we look at our home directory with ls using the -a option we will notice that there are a number of files and directories whose name begin with a dot. As we have discussed, these files are hidden. It’s not a special attribute of the file; it only means that the file will not appear in the output of ls unless the -a or -A options are included. This hidden characteristic also applies to wildcards. Hidden files will not appear unless we use a wildcard pattern such as .*. However, when we do this we will also see both . (the current directory) and .. (the current directory’s parent) in the results. To exclude them we can use patterns such as .[!.]* or .??*.

Wildcards Work in the GUI Too
Wildcards are especially valuable not only because they are used so frequently on the command line, but because they are also supported by some graphical file managers.
<ul type=bullets>
  <li/> In Nautilus (the file manager for GNOME), you can select files by pressing Ctrl-s and entering a file selection pattern with wildcards and the files in the currently displayed directory will be selected.
  <li/> In some versions of Dolphin and Konqueror (the file managers for KDE), you can enter wildcards directly on the location bar. For example, if you want to see all the files starting with a lowercase “u” in the /usr/bin directory, enter “/usr/bin/u*” in the location bar and it will display the result.
</ul>
Many ideas originally found in the command line interface make their way into the graphical interface, too. It is one of the many things that make the Linux desktop so powerful.


<h5>mkdir – Create Directories</h5>
  mkdir directory... <br>
A note on notation: When three periods follow an argument in the description of a command (as above), it means that the argument can be repeated, thus the following command:
<br>
<img width="640" height="252" alt="image" src="https://github.com/user-attachments/assets/adde77ba-f99a-45e4-bfd6-20543cec7332" />
<br>
<h5>cp – Copy Files and Directories</h5>
  cp item1 item2 <br>
copies the single file or directory item1 to the file or directory item2 and the following: <br>
  cp item... directory <br>
copies multiple items (either files or directories) into a directory.
<br>
<img width="831" height="369" alt="image" src="https://github.com/user-attachments/assets/17018984-536f-4e99-810f-27ba36d5b767" /><br>
<img width="834" height="342" alt="image" src="https://github.com/user-attachments/assets/4b57fde7-87ca-42ae-9260-2ba474bf5ec0" /><br>
<img width="834" height="544" alt="image" src="https://github.com/user-attachments/assets/d21110e6-4cb9-4157-95fd-15170bedefc4" /><br>

<h5>mv – Move and Rename Files</h5>
  mv item1 item2 <br>
to move or rename the file or directory item1 to item2 or: <br>
  mv item... directory <br>
to move one or more items from one directory to another.<br>

<img width="842" height="364" alt="image" src="https://github.com/user-attachments/assets/a91a3765-6a94-421e-92f7-7337514d8234" /><br>
<img width="830" height="300" alt="image" src="https://github.com/user-attachments/assets/34a893e1-a292-422b-bbe4-d21c85d5497a" /><br>
<img width="837" height="156" alt="image" src="https://github.com/user-attachments/assets/bb07e7d5-69d9-47fd-85db-4731c46c583c" /><br>

<h5>rm – Remove Files and Directories</h5>
  rm item... <br>
where item is one or more files or directories.<br>

<img width="827" height="424" alt="image" src="https://github.com/user-attachments/assets/ceed087d-d03c-45b3-a108-239fdd60770c" /><br>
<img width="832" height="80" alt="image" src="https://github.com/user-attachments/assets/42b292f0-4778-45cc-ba23-76e9007411c7" /><br>
<img width="828" height="276" alt="image" src="https://github.com/user-attachments/assets/aeb4c908-e4e1-4108-826f-fb255ea6d81c" /><br>

<div> <h6>Be Careful with rm!</h6>
Unix-like operating systems such as Linux do not have an undelete command. Once you delete something with rm, it's gone. Linux assumes you're smart and you know what you're doing. <br>
Be particularly careful with wildcards. Consider this classic example. Let's say you want to delete just the HTML files in a directory. To do this, you type the following: <br>
rm *.html <br>
This is correct, but if you accidentally place a space between the * and the .html like so: <br>
rm * .html <br>
the rm command will delete all the files in the directory and then complain that there is no file called .html. <br>
Here is a useful tip: whenever you use wildcards with rm (besides carefully checking your typing!), test the wildcard first with ls. This will let you see the files that will be deleted. Then press the up arrow key to recall the command and replace ls with rm. <br>
</div>
ln – Create Links <br>
  ln file link <br>
The following creates a symbolic link: <br>
  ln -s item link <br>
to create a symbolic link where item is either a file or a directory. 

<h6>Hard Links</h6>
Hard links are the original Unix way of creating links, compared to symbolic links, which are more modern. By default, every file has a single hard link that gives the file its name. When we create a hard link, we create an additional directory entry for a file. Hard links have two important limitations:
<ol type=numbers>
  <li/> A hard link cannot reference a file outside its own file system. This means a link cannot reference a file that is not on the same disk partition as the link itself.
  <li/> A hard link may not reference a directory.
A hard link is indistinguishable from the file itself. Unlike a symbolic link, when we list a directory containing a hard link we will see no special indication of the link. When a hard link is deleted, the link is removed but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted.
It is important to be aware of hard links because you might encounter them from time to time, but modern practice prefers symbolic links, which we will cover next.
</ol>
<h6> Symbolic Links </h6>
Symbolic links were created to overcome the limitations of hard links. Symbolic links work by creating a special type of file that contains a text pointer to the referenced file or directory. In this regard, they operate in much the same way as a Windows shortcut, though of course they predate the Windows feature by many years.
A file pointed to by a symbolic link, and the symbolic link itself are largely indistinguishable from one another. For example, if we write something to the symbolic link, the referenced file is written to. However when we delete a symbolic link, only the link is deleted, not the file itself. If the file is deleted before the symbolic link, the link will continue to exist but will point to nothing. In this case, the link is said to be broken. In many implementations, the ls command will display broken links in a distinguishing color, such as red, to reveal their presence. <br>

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
<img width="399" height="120" alt="image" src="https://github.com/user-attachments/assets/d1cc3f7f-f8cc-4c81-9bee-17a5a186ddc5" /> <br><br>

One thing we notice is that both the second fields in the listings for fun and fun-hard contain a 4 which is the number of hard links that now exist for the file. Remember that a file will always have at least one link because the file's name is created by a link. So, how do we know that fun and fun-hard are, in fact, the same file? In this case, ls is not very helpful. While we can see that fun and fun-hard are both the same size (field 5), our listing provides no way to be sure. To solve this problem, we're going to have to dig a little deeper.
When thinking about hard links, it is helpful to imagine that files are made up of two parts.
<ol type=numbers>
<li/> The data part containing the file's contents.
<li/> The name part that holds the file's name.
When we create hard links, we are actually creating additional name parts that all refer to the same data part. The system assigns a chain of disk blocks to what is called an inode, which is then associated with the name part. Each hard link therefore refers to a specific inode containing the file's contents.
</ol>
The ls command has a way to reveal this information. It is invoked with the -i option. <br>

<img width="475" height="119" alt="image" src="https://github.com/user-attachments/assets/5087013a-baa5-467b-ab44-7e1db3d0c41f" /> <br>

In this version of the listing, the first field is the inode number and, as we can see, both fun and fun-hard share the same inode number, which confirms they are the same file. <br>

Symbolic links were created to overcome the two disadvantages of hard links.
<ol type=numbers>
  <li/> Hard links cannot span physical devices.
  <li/> Hard links cannot reference directories, only files.
</ol>
Symbolic links are a special type of file that contains a text pointer to the target file or directory. <br>

<img width="480" height="380" alt="image" src="https://github.com/user-attachments/assets/547477ea-8284-4e45-b530-5c3cb8456544" />
<img width="471" height="197" alt="image" src="https://github.com/user-attachments/assets/96516c9f-d728-4728-929b-fde0f67e8ac5" />
<img width="468" height="185" alt="image" src="https://github.com/user-attachments/assets/3243105c-5b7e-4c5d-81d4-408543d9c784" />
<img width="467" height="181" alt="image" src="https://github.com/user-attachments/assets/ae3d8ef9-6769-48f6-a671-1f1eb2dca0a0" />
<img width="284" height="59" alt="image" src="https://github.com/user-attachments/assets/a9b232e1-2c07-40cf-895c-275835891ce0" />
<img width="365" height="134" alt="image" src="https://github.com/user-attachments/assets/af9bd1a0-3f3d-47d1-bb03-5aa7eec18e16" />
<img width="664" height="159" alt="image" src="https://github.com/user-attachments/assets/9a40f86f-947f-4491-b0cf-c285b3a1568f" />
