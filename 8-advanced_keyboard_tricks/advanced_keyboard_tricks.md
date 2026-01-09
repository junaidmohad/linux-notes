8 – Advanced Keyboard Tricks
<ul type=bullets>
  <li/>  clear – Clear the screen
  <li/>  history – Display the contents of the history list
</ul>
<h6>Command Line Editing</h6>
bash uses a library (a shared collection of routines that different programs can use) called Readline to implement command line editing.
Think of these as additional tools that we can employ in our work. It’s not important to learn all of them, but many of them are very useful. Pick and choose as desired. <br>

Note: Some of the key sequences below (particularly those that use the Alt key) may be intercepted by the GUI for other functions. All of the key sequences should work properly when using a virtual console. <br>

<h6>Cursor Movement</h6>
The following table lists the keys used to move the cursor: <br>
<img width="777" height="313" alt="image" src="https://github.com/user-attachments/assets/54ffa3bf-5b61-42bd-ae04-14b68de7db02" /> <br>

<h6>Modifying Text</h6>
Since we might make a mistake when composing a command, we need a way to correct them efficiently. <br>
<img width="836" height="363" alt="image" src="https://github.com/user-attachments/assets/34a1737e-981e-4215-ae6b-3ae179526d3a" /> <br>

<h6>Cutting and Pasting (Killing and Yanking) Text</h6>
The Readline documentation uses the terms killing and yanking to refer to what we would commonly call cutting and pasting. Items that are cut are stored in a buffer (a temporary storage area in memory) called the kill-ring <br>
<img width="786" height="329" alt="image" src="https://github.com/user-attachments/assets/681f2762-a0a3-4bea-a968-8e91ad448c2d" /> <br>

<h6>The Meta Key</h6>
If you venture into the Readline documentation, which can be found in the “READLINE” section of the bash man page, you will encounter the term meta key. On modern keyboards this maps to the Alt key but it wasn't always so. <br>
Back in the dim times (before PCs but after Unix), not everybody had their own computer. What they might have had was a device called a terminal. A terminal was a communication device that featured a text display screen and a keyboard and just enough electronics inside to display text characters and move the cursor around. It was attached (usually by serial cable) to a larger computer or the communication network of a larger computer. There were many different brands of terminals, and they all had different keyboards and display feature sets. Since they all tended to at least understand ASCII, software developers wanting portable applications wrote to the lowest common denominator. Unix systems have an elaborate way of dealing with terminals and their different display features. Since the developers of Readline could not be sure of the presence of a dedicated extra control key, they invented one and called it meta. While the Alt key serves as the meta key on modern keyboards, you can also press and release the Esc key to get the same effect as holding down the Alt key if you're using a terminal (which you can still do in Linux!). <br>

<h6>Completion</h6>
Another way that the shell can help us is through a mechanism called completion. Completion occurs when we press the tab key while typing a command. <br>
While this example shows completion of pathnames, which is its most common use, completion will also work on variables (if the beginning of the word is a $), user names (if the word begins with ~), commands (if the word is the first word on the line) and hostnames (if the beginning of the word is @). Hostname completion works only for hostnames listed in /etc/hosts. <br>
<img width="425" height="126" alt="image" src="https://github.com/user-attachments/assets/cd0176d4-5d80-4869-b410-2c6c459f433b" /> <br>

There are a number of control and meta key sequences that are associated with completion <br>
<img width="807" height="234" alt="image" src="https://github.com/user-attachments/assets/0d8e88a2-aea1-48ab-85bc-66a71cfcc8c0" /> <br>
There are quite a few more that are rather obscure. A list appears in the bash man page under “READLINE”. <br>

<h6>Programmable Completion</h6>
Recent versions of bash have a facility called programmable completion. Programmable completion allows you (or more likely, your distribution provider) to add additional completion rules. Usually this is done to add support for specific applications. For example, it is possible to add completions for the option list of a command or match particular file types that an application supports. Ubuntu has a fairly large set defined by default. Programmable completion is implemented by shell functions, a kind of mini shell script that we will cover in later chapters. If you are curious, try the following: <br>
set | less <br>
and see if you can find them. Not all distributions include them by default. <br>

<h6>Using History</h6>
bash maintains a history of commands that have been entered. This list of commands is kept in our home directory in a file called .bash_history. The history facility is a useful resource for reducing the amount of typing we have to do, especially when combined with command line editing. <br>

<h6>Searching History</h6>
At any time, we can view the contents of the history list by doing the following: <br>
<img width="166" height="46" alt="image" src="https://github.com/user-attachments/assets/d7d80213-b92b-4244-a7f4-b7eaf9c9f06b" /> <br>
<img width="281" height="536" alt="image" src="https://github.com/user-attachments/assets/b39ce5f3-2869-42c3-989e-5be15aa10786" /> <br>

By default, most modern Linux distributions configure bash to store the last 1000 commands we have entered. We will see how to adjust this value

let's say that among our results we got a line containing an interesting command like this: <br>
88 ls -l /usr/bin > ls-output.txt <br>
The 88 is the line number of the command in the history list. We could use this immediately using another type of expansion called history expansion. <br>
<img width="301" height="95" alt="image" src="https://github.com/user-attachments/assets/d1ff9c0b-d48d-4fd2-94f8-a6b73b3d9085" /> <br>

bash also provides the ability to search the history list incrementally. This means we can tell bash to search the history list as we enter characters, with each additional character further refining our search. To start incremental search press Ctrl-r followed by the text we are looking for. When we find it, we can either press Enter to execute the command or press Ctrl-j to copy the line from the history list to the current command line. To find the next occurrence of the text (moving “up” the history list), press Ctrl-r again. To quit searching, press either Ctrl-g or Ctrl-c. <br>
<img width="291" height="155" alt="image" src="https://github.com/user-attachments/assets/f39a8816-af00-4c31-af7a-a01ebc5ef9fe" />
<img width="839" height="525" alt="image" src="https://github.com/user-attachments/assets/0425d8d6-0061-4c07-80f4-69772caf2f2a" /> <br>

<h6>History Expansion</h6>
The shell offers a specialized type of expansion for items in the history list by using the ! character. We have already seen how the exclamation point can be followed by a number to insert an entry from the history list. There are a number of other expansion features, as described in Table <br>
<img width="817" height="264" alt="image" src="https://github.com/user-attachments/assets/52098944-0c5d-445c-9d97-d05f8015aed4" /> <br>

Use caution with the !string and !?string forms unless youyou are absolutely sure of the contents of the history list items. We can mitigate this problem somewhat by appending “:p” to our expansion. This tells the shell to print the result of the expansion and place it into the command history. <br>
<img width="288" height="288" alt="image" src="https://github.com/user-attachments/assets/0d8cc9e2-cea9-4f2f-aa3b-5bc3f9ad7f9e" /> <br>

<h6>script</h6>
In addition to the command history feature in bash, most Linux distributions include a program called script that can be used to record an entire shell session and store it in a file. The basic syntax of the command is as follows: <br>
script [file] <br>
where file is the name of the file used for storing the recording. If no file is specified, the file typescript is used. See the script man page for a complete list of the program’s options and features.
