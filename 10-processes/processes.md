
<h2>10 – Processes</h2>
Modern operating systems are usually multitasking, meaning they create the illusion of doing more than one thing at once by rapidly switching from one executing program to another. The Linux kernel manages this through the use of processes. Processes are how Linux organizes the different programs waiting for their turn at the CPU
In this chapter, we will look at some of the tools available at the command line that let us examine what programs are doing and how to terminate processes that are misbehaving.
<div>
 <ul type=bullet>
  <li/>  ps – Report a snapshot of current processes 
  <li/>  top – Display tasks
  <li/>  jobs – List active jobs
  <li/>  bg – Place a job in the background
  <li/>  fg – Place a job in the foreground
  <li/>  kill – Send a signal to a process
  <li/>  killall – Kill processes by name
  <li/>  nice - Run a program with modified scheduling priority
  <li/>  renice - Alter priority of running processes
  <li/>  nohup - Run a command immune to hangups
  <li/>  halt/poweroff/reboot - Halt, power-off, or reboot the system
  <li/>  shutdown – Shutdown or reboot the system
 </ul>
</div>


<h6>How a Process Works</h6>
When a system starts up, the kernel initiates a few of its own activities as processes and launches a program called init. init, in turn, starts systemd which starts all the system services. In older Linux distributions init runs a series of shell scripts (located in /etc) called init scripts to perform a similar function. Many system services are implemented as daemon programs, programs that just sit in the background and do their thing without having any user interface. So, even if we are not logged in, the system is at least a little busy performing routine stuff
The fact that a program can launch other programs is expressed in the process scheme as a parent process producing a child process.
The kernel maintains information about each process to help keep things organized. For example, each process is assigned a number called a process ID (PID). PIDs are assigned in ascending order, with init always getting PID 1. The kernel also keeps track of the memory assigned to each process, as well as the processes' readiness to resume execution. Like files, processes also have owners and user IDs, effective user IDs, etc. <br>



<h6>Viewing Processes</h6>
The most commonly used tool to view processes (there are several) is the ps command. The ps program has a lot of options <br><br>
<img width="259" height="97" alt="image" src="https://github.com/user-attachments/assets/25520815-ae36-4a8b-8a56-3a2f2413b2f5" /> <br><br>
The result in this example lists two processes, process 5198 and process 10129, which are bash and ps respectively. As we can see, by default, ps doesn't show us very much, just the processes associated with the current terminal session. <br>

<img width="651" height="534" alt="image" src="https://github.com/user-attachments/assets/cd9e2a7e-dc6e-49af-a146-ccf42b223f21" /> <br>

Adding the “x” option (note that there is no leading dash) tells ps to show all of our processes regardless of what terminal (if any) they are controlled by. The presence of a “?” in the TTY column indicates no controlling terminal. Using this option, we see a list of every process that we own. <br>
Since the system is running a lot of processes, ps produces a long list. It is often helpful to pipe the output from ps into less for easier viewing. <br>
A new column titled STAT has been added to the output. STAT is short for “state” and reveals the current status of the process, as shown in Table <br>
<img width="831" height="613" alt="image" src="https://github.com/user-attachments/assets/8c5cddb7-a35a-4362-89c4-c8e3ea61bc6c" /><br>
The process state may be followed by other characters. These indicate various exotic process characteristics. See the ps man page for more detail. <br>
Another popular set of options is “aux” (without a leading dash). This gives us even more information. <br>
<img width="683" height="541" alt="image" src="https://github.com/user-attachments/assets/6183cf08-ab29-415f-a07f-7dcd26aa35de" />
<img width="684" height="338" alt="image" src="https://github.com/user-attachments/assets/153f99e0-a2c3-4884-8f89-6c9b9bfa2a87" />

<br>
This set of options displays the processes belonging to every user. Using the options without the leading dash invokes the command with “BSD style” behavior. The Linux version of ps can emulate the behavior of the ps program found in several different Unix implementations. The most popular BSD options are shown in Table <br>
<img width="835" height="477" alt="image" src="https://github.com/user-attachments/assets/d34d45b2-21ad-448a-bbc3-a6b02794f6ae" />
<img width="827" height="259" alt="image" src="https://github.com/user-attachments/assets/d43a1768-29fb-402b-8bd6-390ac6018c2c" /> <br>
It’s also possible to produce a detailed snapshot of a single process by including a PID as a command argument as shown in the example <br>
<img width="720" height="155" alt="image" src="https://github.com/user-attachments/assets/24800355-7c9e-4d47-96fc-56cdbda334cc" />

<h6>Viewing Processes Dynamically with top</h6>
While the ps command can reveal a lot about what the machine is doing, it provides only a snapshot of the machine's state at the moment the ps command is executed. To see a more dynamic view of the machine's activity, we use the top command <br>
<img width="722" height="531" alt="image" src="https://github.com/user-attachments/assets/f97c8c48-739f-47e8-9f10-7bfea8a081ef" /> <br>
top program displays a continuously updating (by default, every three seconds) display of the system processes listed in order of process activity. The name top comes from the fact that the top program is used to see the “top” processes on the system. The top display consists of two parts: a system summary at the top of the display, followed by a table of processes sorted by CPU activity: <br>
<img width="834" height="428" alt="image" src="https://github.com/user-attachments/assets/5142cdef-ed13-4782-a800-b3988319e883" />
<img width="668" height="550" alt="image" src="https://github.com/user-attachments/assets/f63ecf19-a3e1-49b3-b79b-18cd40ceda4b" /> <br>

The top program accepts a number of keyboard commands. The two most interesting are h, which displays the program's help screen, and q, which quits top. <br>
<img width="646" height="388" alt="image" src="https://github.com/user-attachments/assets/dd67a7d4-febd-4fa6-ac0d-9aa1261845ea" />

<h6>Controlling Processes </h6>

For our experiments, we're going to use a little program called xlogo as our guinea pig. The xlogo program is a sample program supplied with the X Window System which simply displays a re-sizable window containing the X logo After entering the command, a small window containing the logo should appear somewhere on the screen. On some systems, xlogo may print a warning message, but it may be safely ignored <br>
Tip: If your system does not include the xlogo program, try using gedit or kwrite instead. <br>
We can verify that xlogo is running by resizing its window. If the logo is redrawn in the new size, the program is running.<br>
Notice how our shell prompt has not returned? This is because the shell is waiting for the program to finish, just like all the other programs we have used so far. If we close the xlogo window, the prompt returns <br>
<img width="455" height="473" alt="image" src="https://github.com/user-attachments/assets/e7cccf99-56a8-447d-94fb-59b144851724" />

<h6>Interrupting a Process</h6>
In a terminal, pressing Ctrl-c, interrupts a program. This means we are politely asking the program to terminate. After we pressed Ctrl-c, the xlogo window closed and the shell prompt returned. <br>
Many (but not all) command-line programs can be interrupted by using this technique <br>
<img width="195" height="127" alt="image" src="https://github.com/user-attachments/assets/72e74c7e-39c9-46c2-bb58-7ce2be1f60e5" />

<h6>Putting a Process in the Background</h6>
we wanted to get the shell prompt back without terminating the xlogo program. We can do this by placing the program in the background. <br>
To launch a program so that it is immediately placed in the background, we follow the command with an ampersand (&) character <br>
<img width="431" height="327" alt="image" src="https://github.com/user-attachments/assets/d87f49ab-a079-4357-a013-a27ecdf6667d" /> <br>
After entering the command, the xlogo window appeared and the shell prompt returned, but some funny numbers were printed too. This message is part of a shell feature called job control. With this message, the shell is telling us that we have started job number 1 ([1]) and that it has PID 28236. If we run ps, we can see our process <br>
<img width="280" height="112" alt="image" src="https://github.com/user-attachments/assets/b185238a-376a-48e8-9274-6b1b1e8037f3" /> <br>
shell's job control facility also gives us a way to list the jobs that have been launched from our terminal. Using the jobs command, we can see this list: <br>
<img width="206" height="65" alt="image" src="https://github.com/user-attachments/assets/6c660f80-131a-48e8-add9-2b10f41c7b13" /> <br>
results show that we have one job, numbered 1, that it is running, and that the command was xlogo &.
Note that we can put multiple commands in the background by using this shortcut as shown below <br>
<img width="453" height="300" alt="image" src="https://github.com/user-attachments/assets/11f82773-4996-41f3-9ff7-ca66d8d4aff2" />

<h6>Returning a Process to the Foreground</h6>
A process in the background is immune from terminal keyboard input, including any attempt to interrupt it with Ctrl-c. To return a process to the foreground, use the fg command <br>
<img width="301" height="139" alt="image" src="https://github.com/user-attachments/assets/900db444-f4c2-4a35-a150-db777939be28" /> <br>
fg command followed by a percent sign and the job number (called a jobspec) does the trick. If we only have one background job, the jobspec is optional. To terminate xlogo, press Ctrl-c <br>
<img width="225" height="173" alt="image" src="https://github.com/user-attachments/assets/b7801e02-c104-4abd-86ff-64aa64065376" />

<h6>Stopping (Pausing) a Process</h6>
Sometimes we'll want to stop a process without terminating it. This is often done to allow a foreground process to be moved to the background. To stop a foreground process and place it in the background, press Ctrl-z. Let's try it. At the command prompt, type xlogo, press the Enter key, and then press Ctrl-z <br>
<img width="215" height="185" alt="image" src="https://github.com/user-attachments/assets/ebe8f0fb-22eb-4ee9-8edf-83c7345ee684" /> <br>
After stopping xlogo, we can verify that the program has stopped by attempting to resize the xlogo window. We will see that it appears quite dead. We can either continue the program's execution in the foreground, using the fg command, or resume the program's execution in the background with the bg command <br>
<img width="236" height="69" alt="image" src="https://github.com/user-attachments/assets/13bd78e5-015f-440f-b526-203dc10e0d79" /> <br>

As with the fg command, the jobspec is optional if there is only one job. <br>
Moving a process from the foreground to the background is handy if we launch a graphical program from the command line, but forget to place it in the background by appending the trailing &. <br>
Why would we want to launch a graphical program from the command line? There are two reasons. <br>
<ul type=bullets>
<li/> The program we want to run might not be listed on the window manager's menus (such as xlogo).
<li/> By launching a program from the command line, we might be able to see error messages that would otherwise be invisible if the program were launched graphically. Sometimes, a program will fail to start up when launched from the graphical menu. By launching it from the command line instead, we may see an error message that will reveal the problem. Also, some graphical programs have interesting and useful command line options

<h6>Changing Process Priority</h6>
we saw in the output of the ps command (as well as top) there is a process attribute called “niceness” which refers to the scheduling priority given to a process. In certain circumstances such as when video transcoding or performing CPU-based ray tracing for example, we may want to give a process more priority (less niceness) or alternately if we want a process to use less CPU time we could give it more niceness. Niceness can be adjusted with the nice and renice commands. It is important to remember that only the superuser may increase the priority of a process and that regular users may only decrease the priority of processes that they own <br>
nice command launches a process with a specified niceness. Niceness adjustments are expressed from -20 (the most favorable) to 19 (the least favorable) with a default of value of zero (no adjustment).<br>

Imagine we have a program called cpu-hog that we want to run at a lower priority than it’s normal 20. We can launch the program with nice <br>
[me@linuxbox ~]$ nice -n 10 cpu-hog <br>
<img width="472" height="375" alt="image" src="https://github.com/user-attachments/assets/09d1a661-876d-4820-8d3c-7fb6f6888097" /> <br>

if we have a program called must-run-fast that needs to be given more CPU priority, we (as the superuser) could do this <br>
[me@linuxbox ~]$ sudo nice -n -10 must-run-fast <br>

rarely necessary to run a command with increased priority and doing so runs the risk of starving essential system processes of needed CPU time, so be careful <br>

renice command adjusts the priority of a running process. For example, if we had launched the cpu-hog program and wanted to increase its niceness after the fact <br>
<img width="426" height="331" alt="image" src="https://github.com/user-attachments/assets/d8c8218e-ab6d-41c8-9cbd-d45707afc02e" /> <br>
First, we run ps to determine the process id of the running cpu-hog program followed by the renice command with the desired niceness level and the process id. The niceness level of 19 (the maximum value) is useful as it makes the process only use CPU cycles when nothing else is waiting

<h5>Signals</h5>
kill command is used to “kill” processes. This allows us to terminate programs that need killing (that is, some kind of pausing or termination).
<img width="268" height="288" alt="image" src="https://github.com/user-attachments/assets/cdb5c19c-b1db-433e-b87b-e76409a71e3d" /> <br>

first launch xlogo in the background. The shell prints the jobspec and the PID of the background process. Next, we use the kill command and specify the PID of the process we want to terminate. We could have also specified the process using a jobspec (for example, %1) instead of a PID <br>

this is all very straightforward, there is more to it than that. The kill command doesn't exactly “kill” processes: rather it sends them signals. Signals are one of several <br>
ways that the operating system communicates with programs. We have already seen signals in action with the use of Ctrl-c and Ctrl-z. When the terminal receives one of these keystrokes, it sends a signal to the program in the foreground. In the case of Ctrl-c, a signal called INT (interrupt) is sent; with Ctrl-z, a signal called TSTP (terminal stop) is sent <br>
The fact that a program can listen and act upon signals allows a program to do things such as save work in progress when it is sent a termination signal.

<h6>Sending Signals to Processes with kill</h6>
The kill command is used to send signals to programs. Its most common syntax looks like this: <br>
kill [-signal] PID... <br>

If no signal is specified on the command line, then the TERM (terminate) signal is sent by default. The kill command is most often used to send the following signals <br>
<img width="822" height="600" alt="image" src="https://github.com/user-attachments/assets/02c74398-e7f5-4ace-8693-9dd32c6c7c10" />
<img width="505" height="534" alt="image" src="https://github.com/user-attachments/assets/2b3d866c-1765-4237-9e9d-06fca762ac62" />

trying the kill command: <br>
<img width="262" height="274" alt="image" src="https://github.com/user-attachments/assets/02ddca07-b1c7-4f1b-adaa-d1b978d270bf" /> <br>

we start the xlogo program in the background and then send it a HUP signal with kill. The xlogo program terminates, and the shell indicates that the background process has received a hangup signal. We may need to press the Enter key a couple of times before the message appears. Note that signals may be specified either by number or by name, including the name prefixed with the letters SIG <br>
<img width="223" height="304" alt="image" src="https://github.com/user-attachments/assets/7efad8a7-f4af-43e9-9b9a-f4ae47502339" /> <br>
we can also use jobspecs in place of PIDs.
Processes, like files, have owners, and you must be the owner of a process (or the superuser) to send it signals with kill.
In addition to the list of signals above, which are most often used with kill, there are other signals frequently used by the system as listed

<img width="815" height="383" alt="image" src="https://github.com/user-attachments/assets/c0444b24-47a8-4c8b-b716-46fd9dc574d6" /> <br>

a complete list of signals can be displayed with the following command <br>

<img width="512" height="77" alt="image" src="https://github.com/user-attachments/assets/2bee80fb-1c5d-4549-bc1b-1df89b907c94" /> <br>

<h6>Making a Process Hangup Proof</h6>
As we discussed, above many command line programs will respond to the HUP signal by terminating when its controlling terminal “hangs up” (i.e. closes or disconnects). To prevent this behavior, we can launch the program with the nohup command.
If we launch the xlogo program again then close our terminal window, the xlogo program will terminate because it is sent a HUP signal when its controlling terminal is closed. To prevent this we can launch xlogo with the nohup command
<br>
<img width="463" height="200" alt="image" src="https://github.com/user-attachments/assets/556efec0-eeed-49d1-ae45-5910904f1063" /> <br>
when we close the terminal window, xlogo will continue running.

<h6>Sending Signals to Multiple Processes with killall</h6>
It's also possible to send signals to multiple processes matching a specified program or username by using the killall command.<br>
killall [-u user] [-signal] name... <br>
<img width="300" height="526" alt="image" src="https://github.com/user-attachments/assets/1739c8c9-9d20-4d68-8540-fbd82d012a29" />
<br>
Remember, as with kill, we must have superuser privileges to send signals to processes that do not belong to us

<h6>Shutting Down the System</h6>
The process of shutting down the system involves the orderly termination of all the processes on the system, as well as performing some vital housekeeping chores (such as syncing all of the mounted file systems) before the system powers off. There are four commands that can perform this function. They are halt, poweroff, reboot, and shutdown. The first three are pretty self-explanatory and are generally used without any command line options <br>
[me@linuxbox ~]$ sudo reboot <br>

The shutdown command is a bit more interesting. With it, we can specify which of the actions to perform (halt, power down, or reboot) and provide a time delay to the shutdown event. Most often it is used like this to halt the system <br>
[me@linuxbox ~]$ sudo shutdown -h now <br>
or like this to reboot the system: <br>
[me@linuxbox ~]$ sudo shutdown -r now <br>

The delay can be specified in a variety of ways. See the shutdown man page for details. Once the shutdown command is executed, a message is “broadcast” to all logged-in users warning them of the impending event


<h6>More Process-Related Commands</h6>
Since monitoring processes is an important system administration task, there are a lot of commands for it.
<img width="816" height="395" alt="image" src="https://github.com/user-attachments/assets/c71b810e-fe85-4e95-afab-e287ae361f49" /> <br>
<img width="786" height="397" alt="image" src="https://github.com/user-attachments/assets/02767ea4-1e0b-475a-bcc0-3f2b77974413" />
<img width="680" height="92" alt="image" src="https://github.com/user-attachments/assets/a8b9d3d7-a1fb-4a4a-8e8a-25686293186b" />
<img width="360" height="255" alt="image" src="https://github.com/user-attachments/assets/aeddbd20-5e49-4225-939a-8c514cd64501" />
<img width="236" height="554" alt="image" src="https://github.com/user-attachments/assets/ca7a390c-f44a-430e-88fc-18b7cbbd8303" />



Most modern systems feature a mechanism for managing multiple processes. Linux provides a rich set of tools for this purpose. Given that Linux is the world's most deployed server operating system, this makes a lot of sense. However, unlike some other systems, Linux relies primarily on command line tools for process management. Though there are graphical process tools for Linux, the command line tools are greatly preferred because of their speed and light footprint. While the GUI tools may look pretty, they often create a lot of system load themselves, which somewhat defeats the purpose
