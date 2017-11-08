---
bg: "linux.jpg"
layout: post
comments: true
title:  "Managing Packages and Processes"
crawlertitle: "Managing Packages and Processes"
summary: "Менеджеры пакетов и процессы"
date:   2017-11-08 17:00:00 +0300
categories: posts
tags: ['linux']
author: DenIvTea
---

<p>A typical Linux system has thousands of files.  The Filesystem Hierarchy Standard (discussed in detail in a later chapter) provides a guideline for distributions on how to organize these files.  In this chapter, you will see how software package management systems can provide you with information about the location of files belonging to a package.</p>

<p>The <var>Linux kernel</var> is at the core of the GNU/Linux operating system.  This chapter will discuss the role of the Linux kernel and how it provides information about the system under the<code class="console">/proc</code> and <code class="console">/sys</code> <var>pseudo-filesystems</var>.  </p>

<p>You will see how each command that you execute causes a process to be run and how you can view running processes with the <code>ps</code> command.  You will also see discussion of how the system records or logs messages from the <var>background processes</var> called <var>daemons</var>. </p> 

<p>Finally, you will see how to view the kernel <var>ring buffer</var> to view messages it contains with the <code>dmesg</code> command.</p>

Навигация по статье:

* <a href="#1">1.1 Package Management</a>
* <a href="#2">1.1.1 Debian Package Management</a>
* <a href="#3">1.1.1.1 Debian - Adding Packages</a>
* <a href="#4">1.1.1.2 Debian - Updating Packages</a>
* <a href="#5">1.1.1.3 Debian - Removing Packages</a>
* <a href="#6">1.1.1.4 Debian - Querying Packages</a>
* <a href="#7">1.1.2 RPM Package Management</a>
* <a href="#8">1.1.2.1 RPM - Adding Packages</a>
* <a href="#9">1.1.2.2 RPM - Updating Packages</a>
* <a href="#10">1.1.2.3 RPM - Removing Packages</a>
* <a href="#11">1.1.2.4 RPM - Querying Packages</a>
* <a href="#12">1.2 Linux Kernel</a>
* <a href="#13">1.3 Process Hierarchy</a>
* <a href="#14">1.4 ps (Process) Command</a>
* <a href="#15">1.5 top Command</a>
* <a href="#16">1.6 free Command</a>
* <a href="#17">1.7 Log Files</a>
* <a href="#18">1.8 dmesg Command</a>

<h2><a name="1">1.1 Package Management</a></h2>
<p><var>Package management</var> is a system by which software can be installed, updated, queried or removed from a filesystem.  In Linux, there are many different software package management systems, but the two most popular are those from <strong>Debian</strong> and <strong>Red Hat</strong>.</p>
<h2><a name="2">1.1.1 Debian Package Management</a></h2>
<p>The Debian distribution and its derivatives such as Ubuntu and Mint, use the Debian package management system.  At the heart of Debian-derived distributions package management are the software packages that are distributed as files ending in "<code class="console">.deb</code>".   </p>

<p>The lowest level tool for managing these files is the <code>dpkg</code> command.  This command can be tricky for novice Linux users, so the Advanced Package Tool, <code>apt-get</code>, a front-end program to the <code>dpkg</code> tool, makes management of packages even easier.  There are other command line tools which serve as front-ends to <code>dpkg</code>, such as <code>aptitude</code>, as well as GUI front-ends like <code>synaptic</code> and <code>software-center</code> (shown below).</p>
 
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/11.3.1_1.png"></div>

<h2><a name="3">1.1.1.1 Debian - Adding Packages</a></h2>
<p>The Debian repositories contain more than 65,000 different packages of software.  To get an updated list from these Internet repositories, you can execute the <code>sudo apt-get update</code> command.</p>

<p>To search for keywords within these packages, you can use the <code>sudo apt-cache search <var>keyword</var></code> command.</p>

<p>Once you've found the package that you want to install, you can install it with the <code>sudo apt-get install <var>package</var></code> command.</p>

<div class="alert alert-danger">
<strong>Important: </strong>To execute these commands, your system will need access to the Internet.  The <code>apt-cache</code> command searches repositories on the Internet for these software programs.</div>

<h2><a name="4">1.1.1.2 Debian - Updating Packages</a></h2>
<p>If you want to update an individual package, you perform the command to install that package: <code>sudo apt-get install package</code> </p>

<p>If an older version of the package is already installed, then it will be upgraded.  Otherwise, a new installation would take place.</p>

<p>If you want to update all possible packages, then you would execute the <code>sudo apt-get upgrade</code> command.</p>

<p>Users who log in with a graphical interface may have a message appear in the notification area from the <code>update-manager </code>indicating that updates are available, as shown below:</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/11.3.1.2_1.png"></div>

<h2><a name="5">1.1.1.3 Debian - Removing Packages</a></h2>
<p>Beware that removing one package of software may result in the removal of other packages.  Due to the <var>dependencies</var> between packages, if you remove a package, then all packages that need, or depend on that package will be removed as well.</p>

<p>If you want to remove all the files of a software package, except for the configuration files, then you can execute the <code>sudo apt-get remove <var>package</var></code> command.</p>

<p>If you want to remove all the files of a software package, including the configuration files, then you can execute the <code>sudo apt-get --purge remove <var>package</var></code> command.</p>

<div class="alert alert-info">You may want to keep the configuration files in the event that you plan to reinstall the software package at a later time.</div>

<h2><a name="6">1.1.1.4 Debian - Querying Packages</a></h2>
<p>There are several different kinds of queries that administrators need to use.  To get a list of all the packages that are currently installed on the system, execute the <code>dpkg -l</code> command.</p>

<p>To list the files that comprise a particular package, you can execute the <code>dpkg -L <var>package</var></code> command.</p>

<p>To query a package for information, or its state, use the <code>dpkg -s <var>package</var></code> command.</p>

<p>To determine if a particular file was put on the filesystem as the result of installing a package, use the <code>dpkg -S /path/to/file</code> command.  If the file was part of a package, then the package name could be provided. For example:</p> 

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> dpkg -S /usr/bin/who
coreutils: /usr/bin/who</pre>

<p>The previous example shows the file <code class="console">/usr/bin/who</code> is part of the <code class="console">coreutils</code> package.</p>

<h2><a name="7">1.1.2 RPM Package Management</a></h2>
<p>The <strong>Linux Standards Base</strong>, which is a Linux Foundation project, is designed to specify (through a consensus) a set of standards that increase the compatibility between conforming Linux systems.  According to the Linux Standards Base, the standard package management system is RPM.  </p>

<p>RPM makes use of an <code class="console">.rpm</code> file for each software package.  This system is what Red Hat-derived distributions (like Red Hat, Centos, and Fedora) use to manage software.  In addition, several other distributions that are not Red Hat-derived (such as SUSE, OpenSUSE and Mandriva) also use RPM.</p>

<div class="alert alert-info">
<strong>Note:</strong> RPM commands are not available within the virtual machine environment of this course.</div>

<p>Like the Debian system, RPM Package Management systems track dependencies between packages.  Tracking dependencies ensures that when you install a package, the system will also install any packages needed by that package to function correctly.  Dependencies also ensure that software updates and removals are performed properly.  </p>

<p>The back-end tool most commonly used for RPM Package Management is the <code>rpm</code> command.  While the <code>rpm</code> command can install, update, query and remove packages, the command line front end tools such as <code>yum</code> and <code>up2date</code> automate the process of resolving dependency issues.</p>

<p>In addition, there are GUI-based front end tools such as <code>yumex</code> and <code>gpk-application</code> (shown below) that also make RPM package management easier.</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/11.3.2_1.png"></div>

<p>You should note that the many of following commands will require root privileges.  The rule of thumb is that if a command affects the state of a package, you will need to have administrative access.  In other words, a regular user can perform a query or a search, but to add, update or remove a package requires the command be executed as the root user.</p>

<h2><a name="8">1.1.2.1 RPM - Adding Packages</a></h2>
<p>To search for a package from the configured repositories, execute the <code>yum search <var>keyword</var></code> command.</p>

<p>To install a package, along with its dependencies, execute the <code>yum install <var>package</var></code> command.</p>

<div class="alert alert-info">RPM commands are not available within the virtual machine environment of this course.</div>

<h2><a name="9">1.1.2.2 RPM - Updating Packages</a></h2>
<p>If you want to update an individual software package, you can execute the <code>yum update <var>package</var></code> command.</p>

<p>If you want to update all packages, you can execute the <code>yum update</code> command.</p>

<p>If updates are available and the user is using the GUI, then the <code>gpk-update-viewer</code> may show a message in the notification area of the screen indicating that updates are available.</p>

<div class="alert alert-info">RPM commands are not available within the virtual machine environment of this course.</div>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/11.3.2.2_1.png"></div>

<h2><a name="10">1.1.2.3 RPM - Removing Packages</a></h2>
<p>As is the case with any package management system that tracks dependencies, if you want to remove one package, then you may end up removing more than one, due to the dependencies.  The easiest way to automatically resolve the dependency issues is to use a <code>yum</code> command:</p>

<pre class="config">yum remove <var>package</var></pre>

<p>While you can remove software packages with the <code>rpm</code> command, it won't remove dependency packages automatically. </p>

<div class="alert alert-info">RPM commands are not available within the virtual machine environment of this course.</div>

<h2><a name="11">1.1.2.4 RPM - Querying Packages</a></h2>
<p>Red Hat package management is similar to Debian package management when it comes to performing queries.  It is best to use the back-end tool, <code>rpm</code>, instead of the front-end tool, <code>yum</code>.  While front-end tools can perform some of these queries, performance suffers because these commands typically connect to multiple repositories across the network when executing any command.  The <code>rpm</code> command performs its queries by connecting to a database that is local to the machine and doesn't connect over the network to any repositories. </p>


<div class="alert alert-info">RPM commands are not available within the virtual machine environment of this course.</div>
<p>To get a list of all the packages that are currently installed on the system, execute the <code>rpm -qa</code> command.</p>

<p>To list the files that comprise a particular package, execute the <code>rpm -ql <var>package</var></code> command.</p>

<p>To query a package for information, or its state, execute the <code>rpm -qi <var>package</var></code> command.</p>

<p>To determine if a particular file was put on the filesystem as the result of installing a package, execute the <code>rpm -qf /path/to/file</code> command.</p>
<h2><a name="12">1.2 Linux Kernel</a></h2>
<p>When most people refer to Linux, they are really referring to <var>GNU/Linux</var>, which defines the operating system.  The <var>Gnu's Not Unix</var> (GNU) part of this combination is provided by a Free Software Foundation project.  GNU is what provides the open source equivalents of many common UNIX commands, the bulk of the essential command line commands.  The Linux part of this combination is the <var>Linux kernel</var>, which is core of the operating system.  The kernel is loaded at boot time and stays loaded to manage every aspect of the running system.</p>

<p>The implementation of the Linux kernel includes many subsystems that are a part of the kernel itself and others that may be loaded in a modular fashion when needed.  Some of the key functions of the Linux kernel include a system call interface, process management, memory management, virtual filesystem, networking, and device drivers.  </p>

<p>In a nutshell, the kernel accepts commands from the user and manages the processes that carry out those commands by giving them access to devices like memory, disks, network interfaces, keyboards, mice, monitors and more.</p>

<p>The kernel provides access to information about running processes through a <var>pseudo filesystem</var> that is visible under the <code class="console">/proc</code> directory.  Hardware devices are made available through special files under the <code class="console">/dev</code> directory, while information about those devices can be found in another pseudo filesystem under the <code class="console">/sys</code> directory.</p>

<p>The<code class="console">/proc</code> directory not only contains information about running processes, as its name would suggest (<var>process</var>), but it also contains information about the system hardware and the current kernel configuration.  See an example output below:</p>

<div class="alert alert-info">Keep in mind that the information displayed in the examples below will be different from 
what you may see within the virtual machine environment of this course.</div>

 <div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/11.4_1.png"></div>

<p>The output from executing <code>ls /proc</code> shows more than one hundred numbered directories.  There is a numbered directory for each running process on the system, where the name of the directory matches the PID (process ID) for the running process.  </p>

<p>Because the <code class="console">/sbin/init</code> process is always the first process, it has a PID of <code class="console">1</code> and the information about the <code class="console">/sbin/init</code> process can be found in the <code class="console">/proc/1</code> directory.  As you will see later in this chapter, there are several commands that allow you to view information about running processes, so it is rarely necessary for users to have to view the files for each running process directly.</p>

<p>You might also see that there are a number of regular files the <code class="console">/proc</code> directory, such as <code class="console">/proc/cmdline</code>, <code class="console">/proc/meminfo</code> and <code class="console">/proc/modules</code>.  These files  provide information about the running kernel:</p>

<ul type="disc" class="">
<li>The <code class="console">/proc/cmdline</code> file can be important because it contains all of the information that was passed to the kernel was first started.  </li>
<li>The <code class="console">/proc/meminfo</code> file contains information about the use of memory by the kernel.  </li>
<li>The <code class="console">/proc/modules</code> file holds a list of <var>modules</var> currently loaded into the kernel to add extra functionality.  </li>
</ul>

<p>Again, there is rarely a need to view these files directly, as other commands offer more "user friendly" output and an alternative way to view this information.</p>

<p>While most of the "files" underneath the <code class="console">/proc</code> directory cannot be modified, even by the root user, the "files" underneath the <code class="console">/proc/sys</code> directory can be changed by the root user.  Modifying these files will change the behavior of the Linux kernel. </p>

<p>Direct modification of these files cause only temporary changes to the kernel.  To make changes permanent, entries can be added to the <code class="console">/etc/sysctl.conf</code> file.  </p>

<p>For example, the <code class="console">/proc/sys/net/ipv4</code> directory contains a file named <code class="console">icmp_echo_ignore_all</code>.  If that file contains a zero <code class="console">0</code>, as it normally does, then the system will respond to <code class="console">icmp</code> requests.  If that file contains a one <code class="console">1</code>, then the system will not respond to <code class="console">icmp</code> requests:</p>

<pre class="config"><strong>[user@localhost ~]$</strong> su -
Password: 
<strong>[root@localhost ~]#</strong> cat /proc/sys/net/ipv4/icmp_echo_ignore_all 
0
<strong>[root@localhost ~]#</strong> ping -c1 localhost
PING localhost.localdomain (127.0.0.1) 56(84) bytes of data.
64 bytes from localhost.localdomain (127.0.0.1): icmp_seq=1 ttl=64 time=0.026 ms

--- localhost.localdomain ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.026/0.026/0.026/0.000 ms
<strong>[root@localhost ~]#</strong> echo 1 &gt; /proc/sys/net/ipv4/icmp_echo_ignore_all
<strong>[root@localhost ~]#</strong> ping -c1 localhost
PING localhost.localdomain (127.0.0.1) 56(84) bytes of data.

--- localhost.localdomain ping statistics ---
1 packets transmitted, 0 received, 100% packet loss, time 10000ms
</pre>

<h2><a name="13">1.3 Process Hierarchy</a></h2>
<p>When the kernel finishes loading during the boot procedure, it starts the <code class="console">/sbin/init</code> process and assigns it a Process Id (PID) of <code class="console">1</code>.  This process then starts other system processes and each process is assigned a PID in sequential order. </p>

<p>As the <code class="console">/sbin/init</code> process starts up other processes, they in turn may start up processes, which may start up other processes, on and on.  When one process starts another process, the process that performs the starting is called the <var>parent process</var> and the process that is started is called the <var>child process</var>.  When viewing processes, the parent  PID will be labeled PPID. </p>

<p>When the system has been running for a long time, it will eventually reach the <var>maximum PID value</var>, which can be viewed and configured through the <code class="console">/proc/sys/kernel/pid_max</code> file.  Once the largest PID has been used, the system will "roll over" and resume by assigning PID values that are available at the bottom of the range.</p>

<div class="alert alert-info">The graphics below provide an example and explanation of the <code>pstree</code> command. The output will vary from the results you will see if you enter the command in the virtual machine environment of this course.</div>

<p>You can "map" processes into a family tree of parent and child couplings.  If you want to view this tree, the command <code>pstree</code> will display it:</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/11.5_1.png"></div>

<p>If you were to examine the parent and child processes relationship, using the output of the previous command, you could consider it to be like the following:</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/11.5_2.png"></div>

<h2><a name="14">1.4 ps (Process) Command</a></h2>
<p>Another way of viewing processes is with the <code>ps</code> command.  By default, the <code>ps</code> command will only show the current processes running in the current shell.  Ironically, you will see <code>ps</code> running when you want to see what else is running in the current shell:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ps                                                        
  PID TTY          TIME CMD                                                     
 6054 ?        00:00:00 bash  
 6070 ?        00:00:01 xeyes
 6090 ?        00:00:01 firefox
 6146 ?        00:00:00 ps
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>     

<p>Similar to the <code>pstree</code> command, if you run <code>ps</code> with the option <code>--forest</code>, then it will show lines indicating the parent and child relationship:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ps --forest                                               
  PID TTY          TIME CMD                                                     
 6054 ?        00:00:00 bash  
 6090 ?        00:00:02   \_ firefox 
 6180 ?        00:00:00   \_ dash
 6181 ?        00:00:00        \_ xeyes
 6188 ?        00:00:00        \_ ps
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>  

<p>To be able to view all processes on the system  you can execute either the <code>ps aux</code> command or the <code>ps -ef</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ps aux | head                                          
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND     
root         1  0.0  0.0  17872  2892 ?        Ss   08:06   0:00 /sbin?? /ini
syslog      17  0.0  0.0 175744  2768 ?        Sl   08:06   0:00 /usr/sbin/rsyslogd -c5                                                                       
root        21  0.0  0.0  19124  2092 ?        Ss   08:06   0:00 /usr/sbin/cron
root        23  0.0  0.0  50048  3460 ?        Ss   08:06   0:00 /usr/sbin/sshd
bind        39  0.0  0.0 385988 19888 ?        Ssl  08:06   0:00 /usr/sbin/named -u bind                                                                     
root        48  0.0  0.0  54464  2680 ?        S    08:06   0:00 /bin/login -f
sysadmin    60  0.0  0.0  18088  3260 ?        S    08:06   0:00 -bash        
sysadmin   122  0.0  0.0  15288  2164 ?        R+   16:26   0:00 ps aux       
sysadmin   123  0.0  0.0  18088   496 ?        D+   16:26   0:00 -bash        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ps -ef | head                                           
UID        PID  PPID  C STIME TTY          TIME CMD                           
root         1     0  0 08:06 ?        00:00:00 /sbin?? /init                 
syslog      17     1  0 08:06 ?        00:00:00 /usr/sbin/rsyslogd -c5        
root        21     1  0 08:06 ?        00:00:00 /usr/sbin/cron                
root        23     1  0 08:06 ?        00:00:00 /usr/sbin/sshd                
bind        39     1  0 08:06 ?        00:00:00 /usr/sbin/named -u bind       
root        48     1  0 08:06 ?        00:00:00 /bin/login -f                 
sysadmin    60    48  0 08:06 ?        00:00:00 -bash                         
sysadmin   124    60  0 16:46 ?        00:00:00 ps -ef                        
sysadmin   125    60  0 16:46 ?        00:00:00 head                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>The output of all processes running on a system can definitely be overwhelming. In the example provided, the output of the <code>ps</code> command was filtered by the <code>head</code> command, so only the first ten processes were shown. If you don't filter the output of the <code>ps</code> command, then you are likely to have to scroll through hundreds of processes to find what might interest you.</p>

<p>A common way to run the <code>ps</code> command is to use the <code>grep</code> command to filter the output display lines that match a keyword, such as the process name.  For example, if you wanted to view the information about the <code>firefox</code> process, you may execute a command like:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ps -e | grep firefox
 6090 pts/0    00:00:07 firefox
</pre>

<p>As the root user, you may be more concerned about the processes of another user, than you are over your own processes.  Because of the several styles of options that the <code>ps</code> command supports, there are different ways to view an individual user's processes.  Using the traditional UNIX option, to view the processes of the <code class="console">sysadmin</code> user, execute the following command:</p>

<pre class="config"><strong>[root@localhost ~]#</strong> ps -u username</pre>

<p>Or use the BSD style of options and execute:</p>

<pre class="config"><strong>[root@localhost ~]#</strong> ps u U username</pre>

<h2><a name="15">1.5 top Command</a></h2>
<p>The <code>ps</code> command provides a "snapshot" of the processes running at the instant the command is executed, the <code>top</code> command that will regularly update the output of running processes. The <code>top</code> command is executed as follows:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> top</pre>

<p>By default, the output of the <code>top</code> command is sorted by the % of CPU time that each process is currently using, with the higher values listed first.  This means processes that are "CPU hogs" are listed first:</p>

<pre class="content_terminal">top - 16:58:13 up 26 days, 19:15,  1 user,  load average: 0.60, 0.74, 0.60      
Tasks:   8 total,   1 running,   7 sleeping,   0 stopped,   0 zombie            
Cpu(s):  6.0%us,  2.5%sy,  0.0%ni, 90.2%id,  0.0%wa,  1.1%hi,  0.2%si,  0.0%st  
Mem:  32953528k total, 28126272k used,  4827256k free,     4136k buffers        
Swap:        0k total,        0k used,        0k free, 22941192k cached         
                                                                                
  <code class="input">PID</code> <code class="input">USER</code>      <code class="input">PR</code>   <code class="input">NI</code> <code class="input">VIRT</code> <code class="input">RES</code>  <code class="input">SHR</code>  <code class="input">S</code> <code class="input">%CPU</code> <code class="input">%MEM</code>     <code class="input">TIME+</code> <code class="input">COMMAND</code>            
    1 root      20   0 17872 2892 2640 S    0  0.0   0:00.02 init               
   17 syslog    20   0  171m 2768 2392 S    0  0.0   0:00.20 rsyslogd           
   21 root      20   0 19124 2092 1884 S    0  0.0   0:00.02 cron               
   23 root      20   0 50048 3460 2852 S    0  0.0   0:00.00 sshd               
   39 bind      20   0  376m  19m 6100 S    0  0.1   0:00.12 named              
   48 root      20   0 54464 2680 2268 S    0  0.0   0:00.00 login              
   60 sysadmin  20   0 18088 3260 2764 S    0  0.0   0:00.01 bash               
  127 sysadmin  20   0 17216 2308 2072 R    0  0.0   0:00.01 top</pre>           
     

<p>There is an extensive list of commands that can be executed from within the running top program:</p>

<table class="table ">
<thead><tr>
<th>Keys</th>
<th>Meaning</th>
</tr></thead>
<tbody>
<tr>
<td>
<strong>h</strong> or <strong>?</strong>
</td>
<td>Help</td>
</tr>
<tr>
<td><strong>l</strong></td>
<td>Toggle load statistics</td>
</tr>
<tr>
<td><strong>t</strong></td>
<td>Toggle time statistics</td>
</tr>
<tr>
<td><strong>m</strong></td>
<td>Toggle memory usage statistics</td>
</tr>
<tr>
<td><strong>&lt;</strong></td>
<td>Move sorted column to the left</td>
</tr>
<tr>
<td><strong>&gt;</strong></td>
<td>Move sorted column to the right</td>
</tr>
<tr>
<td>
<strong>F</strong>
</td>
<td>Choose sorted field</td>
</tr>
<tr>
<td><strong>R</strong></td>
<td>Toggle sort direction</td>
</tr>
<tr>
<td><strong>P</strong></td>
<td>Sort by % CPU</td>
</tr>
<tr>
<td><strong>M</strong></td>
<td>Sort by % memory used</td>
</tr>
<tr>
<td><strong>k</strong></td>
<td>Kill a process (or send it a signal)</td>
</tr>
<tr>
<td><strong>r</strong></td>
<td>Renice priority of a process</td>
</tr>
</tbody>
</table>

<p>One of the advantages of the <code>top</code> command is that it can be left running to stay on "top" of processes for monitoring purposes.  If a process begins to dominate, or "run away" with the system, then it will by default appear at the top of the list presented by the <code>top</code> command.  An administrator that is running the <code>top</code> command can then take one of two actions:</p>

<ol type="disc" class="">
<li>Terminate the "run away" process:  Pressing the <strong>k</strong> key while the <code>top</code> command is running will prompt the user to provide the PID and then a signal number.  Sending the default signal will <var>request</var> the process terminate, but sending signal number <code class="console">9</code>, the <code class="console">KILL</code> signal, will <var>force</var> the process to terminate.</li>
<li>Adjust the priority of the process:  Pressing the <strong>r</strong> key while the <code>top</code> command is running will prompt the user for the process to <code>renice</code>, and then a niceness value.  <var>Niceness</var> values can range from -20 to 19, and affect priority.  Only the root user can use a niceness that is a lower number than the current niceness, or a negative niceness value, which causes the process to run with an increased priority.  Any user can provide a niceness value that is higher than the current niceness value, which will cause the process to run with a lowered priority.</li>
</ol>

<p>Another advantage of the <code>top</code> command is that it is able to give you an overall representation of how busy the system is currently and the trend over time.  The <var>load averages</var> shown in the first line of output from the <code>top</code> command indicate how busy the system has been during the last one, five and fifteen minutes.  This information can also be viewed by executing the <code>uptime</code> command or directly by displaying the contents of the <code class="console">/proc/loadavg</code> file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat /proc/loadavg
0.12 0.46 0.25 1/254 3052
</pre>

<p>The first three numbers in this file indicate the load average over the last one, five and fifteen minute intervals.  The fourth value is a fraction which shows the number of processes currently executing code on the CPU <code class="console">1</code> and the total number of processes <code class="console">254</code>.  The fifth value is the last PID value that executed code on the CPU.</p>

<p>The number reported as a load average is proportional to the number of CPU cores that are able to execute processes.  On a single core CPU, a value of one would mean that the system is fully loaded.  On a four core CPU, a value of one would mean that the system is only 1/4 or 25% loaded.  </p>

<p>Another reason administrators like to keep the <code>top</code> command running is the ability to monitor memory usage in real-time.  Both the <code>top</code> and the <code>free</code> command display statistics for how overall memory is being used.  </p>

<p>The <code>top</code> command also has the ability to show the percent of memory used by each process, so a process that is consuming an inordinate amount of memory can quickly be identified.</p>

<h2><a name="16">1.6 free Command</a></h2>
<p>Executing the <code>free</code> command without any options provides a snapshot of the memory used at that moment.</p>

<p>If you want to monitor memory usage over time with the <code>free</code> command, then you can execute it with the <code>-s</code> option and specify that number of seconds.  For example, executing <code>free -s 10</code> would update the output every ten seconds.  </p>

<p>To make it easier to interpret what the <code>free</code> command is outputting the <code>-m</code> or <code>-g</code> options can be useful to show the output in either megabytes or gigabytes, respectively.  Without these options, the output is displayed in bytes:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> free                                                      
             total       used       free     shared    buffers     cached       
Mem:      32953528   26171772    6781756          0       4136   22660364       
-/+ buffers/cache:    3507272   29446256                                        
Swap:            0          0          0                                        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
                  
<p>When reading the output of the <code>free</code> command:</p>

<ul type="disc" class="">
<li>The first line is a descriptive header. </li>
<li>The second line labeled <code class="console">Mem:</code> is the statistics for the physical memory of the system.</li>
<li>The third line represents the amount of physical memory after adjusting those values by not taking into account any memory that is in use by the kernel for buffers and caches.  Technically, this "used" memory could be "reclaimed" if needed. </li>
<li>The fourth line of output refers to <code class="console">Swap</code> memory, also known as virtual memory.  This is space on the hard disk that is used like physical memory when the amount of physical memory becomes low.  Effectively, this makes it seem that the system has more memory than it really does, but using swap space can also slow down the system.</li>
</ul>

<p>If the amount of memory and swap that is available becomes very low, then the system will begin to automatically terminate processes.  This is one reason why it is important to monitor the system's memory usage.  An administrator that notices the system becoming low on free memory can use <code>top</code> or <code>kill</code> to terminate the processes of their own choice, rather than letting the system choose.</p>

<h2><a name="17">1.7 Log Files</a></h2>
<p>As the kernel and various processes run on the system, they produce output that describes how they are running.  Some of this output is displayed in the terminal window where the process was executed, but some of this data is not sent to the screen, but instead it is written to various files.  This is called "log data" or "log messages".</p>

<p>These log files are very important for a number of reasons;  they can be helpful in trouble-shooting problems and they can be used for determining whether or not unauthorized access has been attempted.  </p>

<p>Some processes are able to "log" their own data to these files, other processes rely on another process (a daemon) to handle these log data files.  </p>

<p>These logging daemons can vary from one distribution to another.  For example, on some distributions, the daemons that run in the background to perform logging are called as <code>syslogd</code> and <code>klogd</code>.  In other distributions, a single daemon such as <code>rsyslogd</code> in Red Hat and Centos or <code>systemd-journald</code> in the Fedora may serve this logging function.</p>

<p>Regardless of what the daemon process is named, the log files themselves are almost always placed into the <code class="console">/var/log</code> directory structure.  Although some of the file names may vary, here are some of the more common files to be found in this directory:</p>

<table class="table ">
<thead><tr>
<th>File</th>
<th>Contents</th>
</tr></thead>
<tbody>
<tr>
<td><code class="console">boot.log</code></td>
<td>Messages generated as services are started during the startup of the system.</td>
</tr>
<tr>
<td><code class="console">cron</code></td>
<td>Messages generated by the <code class="console">crond</code> daemon for jobs to be executed on a recurring basis.</td>
</tr>
<tr>
<td><code class="console">dmesg</code></td>
<td>Messages generated by the kernel during system boot up.</td>
</tr>
<tr>
<td><code class="console">maillog</code></td>
<td>Messages produced by the mail daemon for e-mail messages sent or received</td>
</tr>
<tr>
<td><code class="console">messages</code></td>
<td>Messages from the kernel and other processes that don't belong elsewhere.  Sometimes named <code class="console">syslog</code> instead of <code class="console">messages</code> after the daemon that writes this file.</td>
</tr>
<tr>
<td><code class="console">secure</code></td>
<td>Messages from processes that required authorization or authentication (such as the login process).  </td>
</tr>
<tr>
<td><code class="console">Xorg.0.log</code></td>
<td>Messages from the  X windows (GUI) server.</td>
</tr>
</tbody>
</table>

<p>Log files are <var>rotated</var><var></var>, meaning older log files are renamed and replaced with newer log files.  The file names that appear in the table above may have a numeric or date suffix added to them, for example: <code class="console">secure.0</code> or <code class="console">secure-20131103</code> </p>

<p>Rotating a log file typically occurs on a regularly scheduled basis, for example, once a week.  When a log file is rotated, the system stops writing to the log file and adds a suffix to it.  Then a new file with the original name is created and the logging process continues using this new file.</p>

<p>With the modern daemons, a date suffix is typically used.  So, at the end of the week ending November 3, 2013, the logging daemon might stop writing to <code class="console">/var/log/messages</code>, rename that file <code class="console">/var/log/messages-20131103</code>, and then begin writing to a new <code class="console">/var/log/messages</code> file.</p>

<p>Although most log files contain text as their contents, which can be viewed safely with many tools, other files such as the <code class="console">/var/log/btmp</code> and <code class="console">/var/log/wtmp</code> files contain binary.  By using the <code>file</code> command, you can check the file content type before you view it to make sure that it is safe to view.</p>

<p>For the files that contain binary data, there are normally commands available that will read the files, interpret their contents and then output text.  For example, the <code>lastb</code> and <code>last</code> commands can be used to view the <code class="console">/var/log/btmp</code> and <code class="console">/var/log/wtmp</code> files respectively.</p>

<p>For security reasons, most of the files found are not readable by ordinary users, so be sure to execute commands that interact with these files with root privileges.</p>

<h2><a name="18">1.8 dmesg Command</a></h2>
<p>The <code class="console">/var/log/dmesg</code> file contains the kernel messages that were produced during system startup.  The <code class="console">/var/log/messages</code> file will contain kernel messages that are produced as the system is running, but those messages will be mixed in with other messages from daemons or processes. </p>

<p>Although the kernel doesn't have its own log file normally, one can be configured for them typically by modifying either the <code class="console">/etc/syslog.conf</code> or the <code class="console">/etc/rsyslog.conf</code> file.  In addition, the <code>dmesg</code> command can be used to view the <var>kernel ring buffer</var>, which will hold a large number of messages that are generated by the kernel.</p>

<p>On an active system, or one experiencing many kernel errors, the capacity of this buffer may be exceeded and some messages might be lost.  The size of this buffer is set at the time the kernel is compiled, so it is not trivial to change.</p>

<p>Executing the <code>dmesg</code> command can produce up to 512 kilobytes of text, so filtering the command with a pipe to another command like <code>less</code> or <code>grep</code> is recommended.  For example, if you were troubleshooting problems with your USB device, then searching for the text "USB" with the <code>grep</code> command being case insensitive may be helpful:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> dmesg | grep -i usb 
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
ohci_hcd: USB 1.1 'Open' Host Controller (OHCI) Driver
ohci_hcd 0000:00:06.0: new USB bus registered, assigned bus number 1
usb usb1: New USB device found, idVendor=1d6b, idProduct=0001
usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1</pre>
                                                                                
                                                                       
*Все материалы взяты с официального курса <i class="fa fa-link"></i> [NDG Linux Essential](https://www.netacad.com/ru/courses/ndg-linux-essentials/)*
