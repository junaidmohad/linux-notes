
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
The result in this example lists two processes, process 5198 and process 10129, which are bash and ps respectively. As we can see, by default, ps doesn't show us very much, just the processes associated with the current terminal session.
