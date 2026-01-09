6 – Redirection
  The “I/O” stands for input/output and with this facility we can redirect the input and output of commands to and from files, as well as connect multiple commands together into powerful command pipelines.
  <ul type=bullets>
  <li/>  cat – Concatenate files
  <li/>  sort – Sort lines of text
  <li/>  uniq – Report or omit repeated lines
  <li/>  grep – Print lines matching a pattern
  <li/>  wc – Print newline, word, and byte counts for each file
  <li/>  head – Output the first part of a file
  <li/>  tail – Output the last part of a file
  <li/>  tee – Read from standard input and write to standard output and files
  </ul>
Many of the programs that we have used so far produce output of some kind. This output often consists of two types:
<ul type=bullets>
<li/>The program's results, that is, the data the program is designed to produce
<li/>Status and error messages that tell us how the program is getting along
</ul>
Keeping with the Unix theme of “everything is a file,” programs such as ls actually send their results to a special file called standard output (often expressed as stdout) and their status messages to another file called standard error (stderr). By default, both standard output and standard error are linked to the screen and not saved into a disk file.

In addition, many programs take input from a facility called standard input (stdin), which is, by default, attached to the keyboard.
I/O redirection allows us to change where output goes and where input comes from. Normally, output goes to the screen and input comes from the keyboard, but with I/O redirection, we can change that.

To redirect standard output to another file instead of the screen, we use the > redirection operator followed by the name of the file. Why would we want to do this? It's often useful to store the output of a command in a file.<br>
<img width="456" height="144" alt="image" src="https://github.com/user-attachments/assets/6831ee73-6c99-4dfb-982f-e3661a8bf038" />
<img width="611" height="534" alt="image" src="https://github.com/user-attachments/assets/bf4656fe-3f98-4b8e-8d7c-a3ad4cdeb18e" />
<img width="468" height="66" alt="image" src="https://github.com/user-attachments/assets/27091e16-edd7-407e-a60e-547a5d64e7c1" />
<br>
why was the error message displayed on the screen rather than being redirected to the file ls-output.txt? The answer is that the ls program does not send its error messages to standard output. Instead, like most well-written Unix programs, it sends its error messages to standard error (stderr). Since we only redirected standard output and not standard error, the error message was still sent to the screen. <br>

<img width="418" height="50" alt="image" src="https://github.com/user-attachments/assets/c62c6a66-694d-4e2e-8683-4ef19e64da7a" /> <br>
The file now has zero length! This is because when we redirect output with the “>” redirection operator, the destination file is always rewritten from the beginning. Since our ls command generated no results and only an error message, the redirection operation started to rewrite the file and then stopped because of the error, resulting in its truncation.
if we ever need to actually truncate a file (or create a new, empty file), we can use a trick like this: <br>
<img width="475" height="275" alt="image" src="https://github.com/user-attachments/assets/8e3ab118-b0fa-4fc8-b0a1-9719e882268c" /> <br>
Simply using the redirection operator with no command preceding it will truncate an existing file or create a new, empty file.
how can we append redirected output to a file instead of overwriting the file from the beginning? <br>
<img width="458" height="199" alt="image" src="https://github.com/user-attachments/assets/34de5322-a4f7-48cf-91cf-54fb949dee8b" />
<br>
what if we could treat the sequence as a single entity with a single output stream? We can do this by creating a group command. To do this, we surround our sequence with brace characters <br>
<img width="558" height="106" alt="image" src="https://github.com/user-attachments/assets/20adc3bd-34b3-4439-8e7d-f933a60ec97d" />
<img width="556" height="104" alt="image" src="https://github.com/user-attachments/assets/6776599b-19f6-479a-9357-3de872efbde4" /><br>
With our sequence surrounded by braces, the shell will consider it a single command in terms of redirection. Note that the shell requires whitespace around the braces and the final command in the sequence must be terminated with either a semicolon or a newline

<h6>Redirecting Standard Error</h6>
Redirecting standard error lacks the ease of a dedicated redirection operator. To redirect standard error we must refer to its file descriptor. A program can produce output on any of several numbered file streams. While we have referred to the first three of these file streams as standard input, output and error, the shell references them internally as file de
scriptors 0, 1, and 2, respectively. The shell provides a notation for redirecting files using the file descriptor number. Since standard error is the same as file descriptor number 2, we can redirect standard error with this notation<br>
<img width="287" height="40" alt="image" src="https://github.com/user-attachments/assets/d7bfd7d4-7050-4b53-9eae-9fc99c8e87a7" />

The file descriptor “2” is placed immediately before the redirection operator to perform the redirection of standard error to the file ls-error.txt.

<h6>Redirecting Standard Output and Standard Error to One File</h6>
There are cases in which we may want to capture all of the output of a command to a single file. To do this, we must redirect both standard output and standard error at the same time. There are two ways to do this. Shown here is the traditional way, which works with old versions of the shell<br>
<img width="322" height="43" alt="image" src="https://github.com/user-attachments/assets/e1290099-573e-46d6-af5b-b2f309cfcb67" /><br>

Using this method, we perform two redirections. First we redirect standard output to the file ls-output.txt and then we redirect file descriptor 2 (standard error) to file descriptor 1 (standard output) using the notation 2>&1.<br>
<img width="318" height="93" alt="image" src="https://github.com/user-attachments/assets/004affdc-d026-4090-b251-e20c93575b95" /><li/>

Notice that the order of the redirections is significant. The redirection of standard error must always occur after redirecting standard output or it doesn't work. The following example redirects standard error to the file ls-output.txt: <br>
  >ls-output.txt 2>&1 <br>
However, if the order is changed to the following, standard error is directed to the screen. <br>
  2>&1 >ls-output.txt <br>

Recent versions of bash provide a second, more streamlined method for performing this combined redirection shown here <br>
<img width="321" height="88" alt="image" src="https://github.com/user-attachments/assets/84581529-ce65-43d8-861a-3331a65efa17" /> <br>

We can also append the standard output and standard error streams to a single file like so: <br>
<img width="301" height="134" alt="image" src="https://github.com/user-attachments/assets/1f525e74-e903-418c-9864-16c4e2417a72" /> <br>
 
<h6>Disposing of Unwanted Output</h6>
Sometimes “silence is golden,” and we don't want output from a command, we just want to throw it away. This applies particularly to error and status messages. The system provides a way to do this by redirecting output to a special file called “/dev/null”. This file is a system device often referred to as a bit bucket, which accepts input and does nothing with it. To suppress error messages from a command, we do this: <br>
<img width="406" height="216" alt="image" src="https://github.com/user-attachments/assets/9223ddd9-ecbb-4b77-91b0-8c52f3d3a7ba" /> <br>

<h6>/dev/null In Unix Culture</h6>
The bit bucket is an ancient Unix concept and because of its universality, it has appeared in many parts of Unix culture. When someone says he/she is sending your comments to /dev/null, now you know what it means. For more examples, see the Wikipedia article on /dev/null .

<h6>Redirecting Standard Input</h6>
Up to now, we haven't encountered any commands that make use of standard input (actually we have, but we’ll reveal that surprise a little bit later), so we need to introduce one

<h6>cat – Concatenate Files</h6>
The cat command reads one or more files and copies them to standard output. In most cases, we can think of cat as being analogous to the TYPE command in DOS. We can use it to display files without paging. <br>
<img width="454" height="76" alt="image" src="https://github.com/user-attachments/assets/f6439801-58aa-47c6-8a38-30b4f2a51c38" /> <br>

cat is often used to display short text files. Since cat can accept more than one file as an argument, it can also be used to join files together. Say we have downloaded a large file that has been split into multiple parts (multimedia files are often split this way on Usenet), and we want to join them back together. <br>

If cat is not given any arguments, it reads from standard input and since standard input is, by default, attached to the keyboard, it's waiting for us to type something! Try adding the following text and pressing Enter: <br>
Next, type a Ctrl-d (i.e., hold down the Ctrl key and press “d”) to tell cat that it has reached end of file (EOF) on standard input:<br>
<img width="670" height="160" alt="image" src="https://github.com/user-attachments/assets/e41d9db4-bfa8-4e60-ab1d-ce4da220ba54" />
<img width="376" height="130" alt="image" src="https://github.com/user-attachments/assets/3dc1d1c8-cde1-4014-adc6-c32250ab3737" />
<img width="371" height="57" alt="image" src="https://github.com/user-attachments/assets/db26c121-ded5-4a78-81ee-159c268d448c" />
<br>
Using the command line, we have implemented the world's dumbest word processor!

<h6>Pipelines</h6>
The capability of commands to read data from standard input and send to standard output is utilized by a shell feature called pipelines. Using the pipe operator | (vertical bar), the standard output of one command can be piped into the standard input of another. <br>
  command1 | command2 <br>

To fully demonstrate this, we are going to need some commands. Remember how we said there was one we already knew that accepts standard input?It's less. We can use less to display, page by page, the output of any command that sends its results to standard output: <br>
<img width="223" height="43" alt="image" src="https://github.com/user-attachments/assets/ce6d1342-2f43-451b-91f0-2afcf0ac1aea" /> <br>

This is extremely handy! Using this technique, we can conveniently examine the output of any command that produces standard output

<h6>The Difference Between > and |</h6>
At first glance, it may be hard to understand the redirection performed by the pipeline operator | versus the redirection operator >. Simply put, the redirection operator connects a command with a file, while the pipeline operator connects the output of one command with the input of a second command. <br>
command1 > file1 <br>
command1 | command2 <br>
A lot of people will try the following when they are learning about pipelines, “just to see what happens”: <br>
command1 > command2 <br>
Answer: sometimes something really bad. <br>
Here is an actual example submitted by a reader who was administering a Linux-based server appliance. As the superuser, he did this: <br>
# cd /usr/bin <br>
# ls > less <br>
The first command put him in the directory where most programs are stored and the second command told the shell to overwrite the file less with the output of the ls command. Since the /usr/bin directory already contained a file named less (the less program), the second command overwrote the less program file with the text from ls, thus destroying the less program on his system. <br>
The lesson here is that the > redirection operator silently creates or overwrites files, so you need to treat it with a lot of respect. <br>

<h6>Filters</h6>
Pipelines are often used to perform complex operations on data. It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as filters. Filters take input, change it somehow, and then output it. <br>

The first one we will try is sort. Imagine we wanted to make a combined list of all the executable programs in /bin and /usr/bin, put them in sorted order and view the resulting list <br>
<img width="298" height="38" alt="image" src="https://github.com/user-attachments/assets/53065553-7fa4-45f8-9557-e0e36c552df3" /> <br>
Since we specified two directories (/bin and /usr/bin), the output of ls would have consisted of two sorted lists, one for each directory. By including sort in our pipeline, we changed the data to produce a single, sorted list. <br>
sort is a powerful command with many features and options. <br>

<h6>uniq - Report or Omit Repeated Lines</h6>
The uniq command is often used in conjunction with sort. uniq accepts a sorted list of data from either standard input or a single filename argument (see the uniq man page for details) and, by default, removes any duplicates from the list. So, to make sure our list has no duplicates (that is, any programs of the same name that appear in both the /bin and /usr/bin directories), we will add uniq to our pipeline <br>
<img width="342" height="46" alt="image" src="https://github.com/user-attachments/assets/a092a52c-d881-4cc5-87fb-70874d9fb0a4" /> <br>

we use uniq to remove any duplicates from the output of the sort command. If we want to see the list of duplicates instead, we add the “-d” option to uniq like so <br>
<img width="375" height="42" alt="image" src="https://github.com/user-attachments/assets/25f6170a-4d7f-4956-bd59-29e4a03ef918" />
<img width="275" height="563" alt="image" src="https://github.com/user-attachments/assets/672d07a3-67a1-405e-ab78-2b90dc76f6ed" />
<img width="252" height="561" alt="image" src="https://github.com/user-attachments/assets/748afa71-b0d7-40ca-827e-f94331bece96" />

<h6>wc – Print Line, Word, and Byte Counts</h6>
The wc (word count) command is used to display the number of lines, words, and bytes contained in files. <br>
<img width="241" height="63" alt="image" src="https://github.com/user-attachments/assets/8410867b-29b1-4805-aedb-326a7b07bdb6" /> <br>
In this case, it prints out three numbers: lines, words, and bytes contained in ls-output.txt. <br>
<img width="343" height="52" alt="image" src="https://github.com/user-attachments/assets/5c5b5a5c-aca3-484c-b2ad-87d164fbcba3" /> <br>

<h6>grep – Print Lines Matching a Pattern</h6>
grep is a powerful program used to find text patterns within files. It's used like this: <br>
grep pattern [file...] <br>
When grep encounters a “pattern” in the file, it prints out the lines containing it. The patterns that grep can match can be very complex, but for now we will concentrate on simple text matches.
Let's say we wanted to find all the files in our list of programs that had the word zip embedded in the name. Such a search might give us an idea of some of the programs on our system that had something to do with file compression. <br>
<img width="366" height="404" alt="image" src="https://github.com/user-attachments/assets/1cdb16db-bcf2-4906-84de-09c0fbd348ad" /> <br>
Here are a few handy options for grep: <br>
<ul type=bullets> 
  <li/>  -i, causes grep to ignore case when performing the search (normally searches are case sensitive)
  <li/>  -l, causes grep to only output the names of the files containing text that matches the pattern.
  <li/>  -v, causes grep to print only those lines that do not match the pattern.
  <li/>  -w, causes grep to only match whole words.
</ul>
<h6>head / tail – Print First / Last Part of Files</h6>
  Sometimes we don't want all the output from a command. We may only want the first few lines or the last few lines. The head command prints the first ten lines of a file, and the tail command prints the last ten lines. While both commands print ten lines of text by default, this can be adjusted with the -n option <br>
<img width="416" height="296" alt="image" src="https://github.com/user-attachments/assets/04d26765-c623-47b2-8ebd-371e28e28db6" /> <br>
These commands can be used in pipelines as well: <br>
<img width="260" height="123" alt="image" src="https://github.com/user-attachments/assets/2ead7567-9044-4e6c-93ac-1e628d5ce64d" /> <br>
 
Using the -n option with head and tail together allows us to cut an excerpt from the middle of a file. Let’s imagine we have a text file with a 5 line header and a 5 line footer that we want to remove leaving only the “good” part in the middle containing the data. <br>
<img width="426" height="83" alt="image" src="https://github.com/user-attachments/assets/328f5146-ff62-4746-9eeb-3ae49300eb8e" /> <br>
The -n option when used with head allows a negative value which causes all but the last n lines to be output. Similarly, the -n option with tail allows a plus sign causing all but the first n lines to be output. <br>

tail also has an option which allows us to follow the contents of a file in real time. This is useful for watching the progress of log files as they are being written. In the following example, we will look at the messages file in /var/log (or the /var/log/syslog file if messages is missing). Superuser privileges may be required to do this on some Linux distributions because log files may contain security information <br>
<img width="634" height="72" alt="image" src="https://github.com/user-attachments/assets/8cec148f-1d5d-4d66-83f6-c705114c6aeb" />
<img width="603" height="215" alt="image" src="https://github.com/user-attachments/assets/43d6ddf0-4abb-4094-974e-f912d51b5c97" />

<h6>tee – Read from Stdin and Output to Stdout and Files</h6>
In keeping with our plumbing metaphor, Linux provides a command called tee which creates a “tee” fitting on our pipe. The tee program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files. This is useful for capturing a pipeline's contents at an intermediate stage of processing. <br>
<img width="331" height="488" alt="image" src="https://github.com/user-attachments/assets/6e6d5742-9b55-4ee5-89f2-383887ba1ee2" />
<img width="295" height="537" alt="image" src="https://github.com/user-attachments/assets/72dc4283-475d-4907-8fbc-39ca1a1bb4a3" /> <br>
did this through root

<h6>Linux Is About Imagination</h6>
When I am asked to explain the difference between Windows and Linux, I often use a toy analogy.
Windows is like a Game Boy. You go to the store and buy one all shiny new in the box. You take it home, turn it on, and play with it. Pretty graphics, cute sounds. After a while, though, you get tired of the game that came with it, so you go back to the store and buy another one. This cycle repeats over and over. Finally, you go back to the store and say to the person behind the counter, “I want a game that does this!” only to be told that no such game exists because there is no “market demand” for it. Then you say, “But I only need to change this one thing!” The person behind the counter says you can't change it. The games are all sealed up in their cartridges. You discover that your toy is limited to the games others have decided that you need. <br>
Linux, on the other hand, is like the world's largest Erector Set. You open it, and it's just a huge collection of parts. There's a lot of steel struts, screws, nuts, gears, pulleys, motors, and a few suggestions on what to build. So, you start to play with it. You build one of the suggestions and then another. After a while you discover that you have your own ideas of what to make. You don't ever have to go back to the store, as you already have everything you need. The Erector Set takes on the shape of your imagination. It does what you want.
Your choice of toys is, of course, a personal thing, so which toy would you find more satisfying?
