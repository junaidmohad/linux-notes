3 – Exploring the System
<ul type=bullets>
  <li/>  ls – List directory contents
  <li/>  file – Determine file type
  <li/>  less – View file contents
</ul>
<br>
<img width="548" height="282" alt="image" src="https://github.com/user-attachments/assets/0479226c-2595-43e7-934b-2819019b341d" />
<br>
We can even specify multiple directories. In the following example, we list both the user's home directory (symbolized by the “~” character) and the /usr directory.

We can also change the format of the output to reveal more detail.
<br>
<img width="420" height="183" alt="image" src="https://github.com/user-attachments/assets/f109b542-99e9-449a-ae65-252adcc6a024" />
<br>
Commands are often followed by one or more options that modify their behavior, and further, by one or more arguments, the items upon which the command acts. So most commands look kind of like this: 
command -options arguments
<br>
<img width="426" height="180" alt="image" src="https://github.com/user-attachments/assets/63afd3cd-4bb2-41fc-8bf9-b7cec2ef1762" />
<br>
Note that command options, like filenames in Linux, are case-sensitive.
<br>
<img width="663" height="629" alt="image" src="https://github.com/user-attachments/assets/fa060e47-b4db-4413-ad54-9f5ae491a9cb" />
<br>
<img width="833" height="568" alt="image" src="https://github.com/user-attachments/assets/43414849-9fa6-46ec-b29f-fd260ec1cf01" />
<br>
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
<br>
<img width="833" height="485" alt="image" src="https://github.com/user-attachments/assets/209cbd92-3f75-4264-b7f5-73a9a99768a8" />
<br>

<h5> Less Is More </h5>
The less program was designed as an improved replacement of an earlier Unix program called more. The name “less” is a play on the phrase “less is more” — a motto of modernist architects and designers.
less falls into the class of programs called “pagers,” programs that allow the easy viewing of long text documents in a page by page manner. Whereas the more program could only page forward, the less program allows paging both forward and backward and has many other features as well.
<ol type=numbers>
  <li/> cd into a given directory
  <li/> List the directory contents with ls -l
  <li/> If you see an interesting file, determine its contents with file
  <li/> If it looks like it might be text, try viewing it with less
  <li/> If we accidentally attempt to view a non-text file and it scrambles the terminal window, we can recover by entering the reset command.
</ol>
Remember the copy and paste trick! If you are using a mouse, you can double click on a filename to copy it and middle click to paste it into commands.
<br>
<img width="672" height="198" alt="image" src="https://github.com/user-attachments/assets/e3c763c8-8fdb-429b-82c1-c0abf390a176" />
<br>
<img width="444" height="592" alt="image" src="https://github.com/user-attachments/assets/48df7c82-09ff-4f1f-aadb-02c1f36a11ce" />
<br>
<img width="442" height="574" alt="image" src="https://github.com/user-attachments/assets/aa230340-00d6-427d-ad91-db25db053ef0" />
<br>
<img width="441" height="562" alt="image" src="https://github.com/user-attachments/assets/87be6681-c8f4-4f8c-baee-561e561a8126" />
<br>
<img width="445" height="75" alt="image" src="https://github.com/user-attachments/assets/09b44823-c535-4835-bda6-d50ef610042b" />
<br>
<h6>Symbolic Links</h6>
  lrwxrwxrwx 1 root root 11 2007-08-11 07:34 libc.so.6 -> libc-2.6.so

Notice how the first letter of the listing is “l” and the entry seems to have two filenames? This is a special kind of a file called a symbolic link (also known as a soft link or symlink). In most Unix-like systems it is possible to have a file referenced by multiple names. While the value of this might not be obvious, it is really a useful feature.
Picture this scenario: A program requires the use of a shared resource of some kind contained in a file named “foo,” but “foo” has frequent version changes. It would be good to include the version number in the filename so the administrator or other interested party could see what version of “foo” is installed. This presents a problem. If we change the name of the shared resource, we have to track down every program that might use it and change it to look for a new resource name every time a new version of the resource is installed. That doesn't sound like fun at all.

Here is where symbolic links save the day. Suppose we install version 2.6 of “foo,” which has the filename “foo-2.6” and then create a symbolic link simply called “foo” that points to “foo-2.6.” This means that when a program opens the file “foo”, it is actually opening the file “foo-2.6”. Now everybody is happy. The programs that rely on “foo” can find it and we can still see what actual version is installed. When it is time to upgrade to “foo-2.7,” we just add the file to our system, delete the symbolic link “foo” and create a new one that points to the new version. Not only does this solve the problem of the version upgrade, but it also allows us to keep both versions on our machine. Imagine that “foo-2.7” has a bug (damn those developers!) and we need to revert to the old version. Again, we just delete the symbolic link pointing to the new version and create a new symbolic link pointing to the old version.

<h6>Hard Links</h6>
While we are on the subject of links, we need to mention that there is a second type of link called a hard link. Hard links also allow files to have multiple names, but they do it in a different way.
