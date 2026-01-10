
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

The top program accepts a number of keyboard commands. The two most interesting are h, which displays the program's help screen, and q, which quits top.
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
fg command followed by a percent sign and the job number (called a jobspec) does the trick. If we only have one background job, the jobspec is optional. To terminate xlogo, press Ctrl-c
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




