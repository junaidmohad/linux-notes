
# linux-notes
My notes for learning linux



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
The chown command is used to change the owner and group owner of a file or directory. Superuser privileges are required to use this command. <br>

chown [owner][:[group]] file...

<br> chown can change the file owner and/or the file group owner depending on the first argument of the command. <br>
<img width="998" height="430" alt="image" src="https://github.com/user-attachments/assets/3e990c1f-c97c-41f7-a746-b516a90d0389" /> <br>
Let's say we have two users; janet, who has access to superuser privileges and tony, who does not. User janet wants to copy a file from her home directory to the home directory of user tony. Since user janet wants tony to be able to edit the file, janet changes the ownership of the copied file from janet to tony. <br>
<img width="502" height="471" alt="image" src="https://github.com/user-attachments/assets/e15f3ead-b9f0-4ea8-84e8-4f2fcdcbfaef" /> <br>

Notice that after the first use of sudo, janet was not prompted for her password. This is because sudo, in most configurations, “trusts” us for several minutes until its timer

<h6>chgrp – Change Group Ownership </h6>
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
The one remaining issue is umask. The necessary setting only lasts until the end of session and must be reset.<br><br>
<img width="273" height="119" alt="image" src="https://github.com/user-attachments/assets/7f7e6129-205f-43c9-91c4-f9240c5eecd4" /><br><br>
<img width="409" height="514" alt="image" src="https://github.com/user-attachments/assets/9b8b13f9-cbc0-41e1-b160-3437ef102826" /><br><br>
<img width="513" height="514" alt="image" src="https://github.com/user-attachments/assets/2f850616-8ad5-49fa-8876-e4fe35c72bfa" /><br><br>
<img width="472" height="299" alt="image" src="https://github.com/user-attachments/assets/be8dcd7c-1120-4ac4-996d-fe050b332c50" /> <br><br>

Changing Your Password
setting passwords for ourselves (and for other users if we have access to superuser privileges). To set or change a password, the passwd command is used. The command syntax looks like this:
passwd [user] <br><br>
<img width="328" height="167" alt="image" src="https://github.com/user-attachments/assets/720d465a-ea4c-40a0-8373-554159562b19" /> <br><br>
The passwd command will try to enforce use of “strong” passwords.
If we have superuser privileges, you can specify a username as an argument to the passwd command to set the password for another user. Other options are available to the superuser to allow account locking, password expiration, and so on. See the passwd man page for details

The passwd, addgroup, and usermod commands are part of a suite of commands in the shadow-utils package <br><br>
<img width="878" height="427" alt="image" src="https://github.com/user-attachments/assets/8d454135-cc47-4ffa-9e4d-e2347ece5115" /> <br><br>


