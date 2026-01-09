7 – Seeing the World as the Shell Sees It <br>
  ●  echo – Display a line of text <br>
<h6>Expansion</h6>
Each time we type a command and press the Enter key, bash performs several substitutions upon the text before it carries out our command.
for example *, can have a lot of meaning to the shell. The process that makes this happen is called expansion. With expansion, we enter something and it is expanded into something else before the shell acts upon it. <br>
<img width="655" height="147" alt="image" src="https://github.com/user-attachments/assets/f5d6992e-c20c-4e10-bc88-4d4a6222d308" /> <br>
Why didn't echo print *? As we recall from our work with wildcards, the * character means match any characters in a filename, but what we didn't see in our original discussion was how the shell does that. The simple answer is that the shell expands the * into something else (in this instance, the names of the files in the current working directory) before the echo command is executed.

<h6>Pathname Expansion</h6>
The mechanism by which wildcards work is called pathname expansion. <br>
<img width="545" height="347" alt="image" src="https://github.com/user-attachments/assets/59e1af58-78eb-480c-9508-adf7be9bed53" />

<h6>Pathname Expansion of Hidden Files</h6>
As we know, filenames that begin with a period character are hidden. Pathname expansion also respects this behavior. An expansion such as the following does not reveal hidden files. <br>
echo * <br>
It might appear at first glance that we could include hidden files in an expansion by starting the pattern with a leading period, like this: <br>
echo .* <br>
It almost works. However, if we examine the results closely, we will see that the names . and .. will also appear in the results. Because these names refer to the current working directory and its parent directory, using this pattern will likely produce an incorrect result. We can see this if we try the following command: <br>
ls -d .* | less <br>
To better perform pathname expansion in this situation, we have to employ a more specific pattern. <br>
echo .[!.]* <br>
This pattern expands into every filename that begins with only one period followed by any other characters. This will work correctly with most hidden files (though it still won't include filenames with multiple leading periods). The ls command with the -A option (“almost all”) will provide a correct listing of hidden files. <br>
ls -A <br>
<img width="654" height="494" alt="image" src="https://github.com/user-attachments/assets/5a12f61f-045c-423e-a1da-a462f6dd8de4" />
<img width="530" height="391" alt="image" src="https://github.com/user-attachments/assets/a139d928-b80d-4f07-b311-cc0cf9a0b80f" />

<h6>Tilde Expansion</h6>
As we may recall from our introduction to the cd command, the tilde character (~) has a special meaning. When used at the beginning of a word, it expands into the name of the home directory of the named user or, if no user is named, the home directory of the current user <br>
<img width="211" height="65" alt="image" src="https://github.com/user-attachments/assets/c813bdc6-5060-4046-84db-b9b19e1fd47f" />

<h6>Arithmetic Expansion</h6>
The shell allows arithmetic to be performed by expansion. <br>
<img width="201" height="120" alt="image" src="https://github.com/user-attachments/assets/3759218c-3e6a-4342-b7cf-52de66f99073" /> <br>
Arithmetic expansion supports only integers (whole numbers, no decimals) but can perform quite a number of different operations. <br>
<img width="837" height="345" alt="image" src="https://github.com/user-attachments/assets/5b6e32d1-604b-4c3a-9ec5-d7aefd86a563" /> <br>
Arithmetic expansion uses the following form: <br>
$((expression)) <br>
<img width="241" height="115" alt="image" src="https://github.com/user-attachments/assets/7c29b91b-c5d8-4e33-ba93-aa46bfae2e19" />
<img width="350" height="118" alt="image" src="https://github.com/user-attachments/assets/9a62d64e-e1c3-44e5-a0fc-b2be9529142a" />

<h6>Brace Expansion</h6>
Perhaps the strangest expansion is called brace expansion. With it, we can create multiple text strings from a pattern containing braces <br>
<img width="485" height="373" alt="image" src="https://github.com/user-attachments/assets/dd2ea9e9-8892-4a2e-b825-5742ae4ef946" /> <br>
So, what is this good for? The most common application is making lists of files or directories to be created <br>
<img width="646" height="364" alt="image" src="https://github.com/user-attachments/assets/b0897481-bbcc-4074-8837-d4b589d06682" /> <br>

<h6>Parameter Expansion</h6>
It's a feature that is more useful in shell scripts than directly on the command line. Many of its capabilities have to do with the system's ability to store small chunks of data and to give each chunk a name. Many such chunks, more properly called variables, are available for our examination. For example, the variable named USER contains our username. <br>

<img width="222" height="108" alt="image" src="https://github.com/user-attachments/assets/5578e144-3037-48e5-afe0-68aeb21a3255" />
<img width="367" height="92" alt="image" src="https://github.com/user-attachments/assets/117c5fa1-fb91-4c8c-b88e-165a77636f14" />
<img width="239" height="112" alt="image" src="https://github.com/user-attachments/assets/876b7b52-aa8e-42b5-a2ee-6d9bacb20c18" />

<h6>Command Substitution</h6>
Command substitution allows us to use the output of a command as an expansion. <br>
<img width="614" height="142" alt="image" src="https://github.com/user-attachments/assets/aa887999-196c-4bb1-a2b6-ab5042b12fa5" /> <br>
Here we passed the results of which cp as an argument to the ls command, thereby getting the listing of the cp program without having to know its full pathname. We are not limited to just simple commands. Entire pipelines can be used <br>
<img width="658" height="500" alt="image" src="https://github.com/user-attachments/assets/76cfd6ec-0110-47c4-a63f-65a8405183d4" /> <br>
In this example, the results of the pipeline became the argument list of the file command. <br>
There is an alternate syntax for command substitution used by older shell programs that is also supported in bash. It uses backquotes instead of the dollar sign and parentheses. <br>
<img width="458" height="59" alt="image" src="https://github.com/user-attachments/assets/759baa7e-0ce1-4e03-a608-c1113f99f7e1" />

<h6>Quoting</h6>
Now that we've seen how many ways the shell can perform expansions, it's time to learn how we can control it.<br>
<img width="360" height="123" alt="image" src="https://github.com/user-attachments/assets/4449b45d-8ff3-41c2-9d13-4725afb4ea8f" /> <br>
In the first example, word-splitting by the shell removed extra whitespace from the echo command's list of arguments. In the second example, parameter expansion substituted an empty string for the value of $1 because it was an undefined variable. The shell provides a mechanism called quoting to selectively suppress unwanted expansions. <br>

<h6>Double Quotes</h6>
The first type of quoting we will look at is double quotes. If we place text inside double quotes, all the special characters used by the shell lose their special meaning and are treated as ordinary characters. The exceptions are $, \ (backslash), and ` (back-quote). This means that word-splitting, pathname expansion, tilde expansion, and brace expansion are suppressed, but parameter expansion, arithmetic expansion, and command substitution are still carried out. Using double quotes, we can cope with filenames containing embedded spaces. <br>

<img width="461" height="253" alt="image" src="https://github.com/user-attachments/assets/f95bc0a3-736e-4df0-b0ad-a0910b3d93eb" />
<img width="649" height="278" alt="image" src="https://github.com/user-attachments/assets/9a5b138d-0c5e-4690-941e-699dfacb64d7" />
<img width="288" height="121" alt="image" src="https://github.com/user-attachments/assets/5ef743d5-8e34-4898-a851-1472b21ea816" /> <br>

The fact that newlines are considered delimiters by the word-splitting mechanism causes an interesting, albeit subtle, effect on command substitution. <br>
<img width="659" height="484" alt="image" src="https://github.com/user-attachments/assets/dcc49d94-abf0-4c8e-b855-211aeae9b100" /> <br>
In the first instance, the unquoted command substitution resulted in a command line containing 49 arguments. In the second, it resulted in a command line with one argument that includes the embedded spaces and newlines. <br>

<h6>Single Quotes</h6>
If we need to suppress all expansions, we use single quotes. Here is a comparison of unquoted, double quotes, and single quotes: <br>
<img width="655" height="196" alt="image" src="https://github.com/user-attachments/assets/4ff94886-0f3e-44be-b389-7f0eddc32138" /> <br>
As we can see, with each succeeding level of quoting, more and more of the expansions are suppressed. <br>

<h6>Escaping Characters</h6>
Sometimes we want to quote only a single character. To do this, we can precede a character with a backslash, which in this context is called the escape character. Often this is done inside double quotes to selectively prevent an expansion. <br>

<img width="417" height="58" alt="image" src="https://github.com/user-attachments/assets/e3ff7b15-b8ab-4f4c-998a-fc7a5732b230" /> <br>

It is also common to use escaping to eliminate the special meaning of a character in a filename. For example, it is possible to use characters in filenames that normally have special meaning to the shell. These would include $, !, &, spaces, and others. To include a special character in a filename we can do this: <br>
mv bad\&filename good_filename <br>

To allow a backslash character to appear, escape it by typing \\. Note that within single quotes, the backslash loses its special meaning and is treated as an ordinary character. <br>
Another use of the backslash escape is suppressing aliases. For example, assuming the ls command is aliased to ls=’ls --color=auto’, the default on many Linux distributions, we can precede the command with a backslash and the alias will be ignored and the ls command will be executed without the color option. <br>

<h6>Backslash Escape Sequences</h6>
In addition to its role as the escape character, the backslash is also used as part of a notation to represent certain special characters called control codes. The first 32 characters in the ASCII coding scheme are used to transmit commands to teletype-like devices. Some of these codes are familiar (tab, backspace, linefeed, and carriage return), while others are not (null, end-of-transmission, and acknowledge). <br>

<img width="707" height="289" alt="image" src="https://github.com/user-attachments/assets/42e525f4-baf1-4f7f-8c43-0e9a8bbb1a4b" /> <br>
The table above lists some of the common backslash escape sequences. The idea behind this representation using the backslash originated in the C programming language and has been adopted by many others, including the shell. <br>
Adding the -e option to echo will enable interpretation of escape sequences. You may also place them inside $' '. Here, using the sleep command, a simple program that just waits for the specified number of seconds and then exits, we can create a primitive countdown timer: <br>
sleep 10; echo -e "Time's up\a" <br>
We could also do this: <br>
sleep 10; echo "Time's up" $'\a' <br>

Without a proper understanding of expansion, the shell will always be a source of mystery and confusion, with much of its potential power wasted.
