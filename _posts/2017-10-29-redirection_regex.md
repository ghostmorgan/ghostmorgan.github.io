---
bg: "linux.jpg"
layout: post
comments: true
title:  "Pipes, Redirection, and REGEX"
crawlertitle: "Pipes, Redirection, and REGEX"
summary: "Стандартные I/O потоки, перенаправление и регулярные выражения"
date:   2017-10-29 14:00:00 +0300
categories: posts
tags: ['linux']
author: DenIvTea
---
<p>A large number of the files in a typical filesystem are <var>text files</var>.  Text files contain simply text, no formatting features that you might see in a word processing file.</p>

<p>Because there are so many of these files on a typical Linux system, a great number of commands exist to help users manipulate text files.  There are commands to both view and modify these files in various ways.</p>

<p>In addition, there are features available for the shell to control the output of commands, so instead of having the output placed in the terminal window, the output can be <var>redirected</var> into another file or another command.  These redirection features provide users with a much more flexible and powerful environment to work within.</p>

Навигация по статье:

* <a href="#1">1.1 Command Line Pipes</a>
* <a href="#2">1.2 I/O Redirection</a>
* <a href="#3">1.2.1 STDIN</a>
* <a href="#4">1.2.2 STDOUT</a>
* <a href="#5">1.2.3 STDERR</a>
* <a href="#6">1.2.4 Redirecting STDOUT</a>
* <a href="#7">1.2.5 Redirecting STDERR</a>
* <a href="#8">1.2.6 Redirecting Multiple Streams</a>
* <a href="#9">1.2.7 Redirecting STDIN</a>
* <a href="#10">1.3 Searching for Files Using the Find Command</a>
* <a href="#11">1.3.1 Search by File Name</a>
* <a href="#12">1.3.2 Displaying File Detail</a>
* <a href="#13">1.3.3 Searching for Files by Size</a>
* <a href="#14">1.3.4 Additional Useful Search Options</a>
* <a href="#15">1.3.5 Using Multiple Options</a>
* <a href="#16">1.4 Viewing Files Using the less Command</a>
* <a href="#17">1.4.1 Help Screen in less</a>
* <a href="#18">1.4.2 less Movement Commands</a>
* <a href="#19">1.4.3 less Searching Commands</a>
* <a href="#20">1.5 Revisiting the head and tail Commands</a>
* <a href="#21">1.5.1 Negative Value with the -n Option</a>
* <a href="#22">1.5.2 Positive Value With the tail Command</a>
* <a href="#23">1.5.3 Following Changes to a File</a>
* <a href="#24">1.6 Sorting Files or Input</a>
* <a href="#25">1.6.1 Fields and Sort Options</a>
* <a href="#26">1.7 Viewing File Statistics With the wc Command</a>
* <a href="#27">1.8 Using the cut Command to Filter File Contents</a>
* <a href="#28">1.9 Using the grep Command to Filter File Contents</a>
* <a href="#29">1.10 Basic Regular Expressions</a>
* <a href="#30">1.10.1 Basic Regular Expressions - the . Character</a>
* <a href="#31">1.10.2 Basic Regular Expressions - the [ ] Characters</a>
* <a href="#32">1.10.3 Basic Regular Expressions - the * Character</a>
* <a href="#33">1.10.4 Basic Regular Expressions - the ^ and $ Characters</a>
* <a href="#34">1.10.5 Basic Regular Expressions - the \ Character</a>
* <a href="#35">1.11 Extended Regular Expressions</a>
* <a href="#36">1.12 xargs Command</a>

<h2><a name="#1">1.1 Command Line Pipes</a></h2>
<p>Previous chapters discussed how to use individual commands to perform actions on the operating system, including how to create/move/delete files and move around the system.  Typically, when a command has output or generates an error, the output is displayed to the screen; however, this does not have to be the case.</p>

<p>The <var>pipe</var> <code class="console">|</code> character can be used to send the output of one command to another.  Instead of being printed to the screen, the output of one command becomes input for the next command.  This can be a powerful tool, especially when looking for specific data; <var>piping</var> is often used to refine the results of an initial command. </p>

<p>The <code>head</code> and <code>tail</code> commands will be used in many examples below to illustrate the use of pipes.  These commands can be used to display only the first few or last few lines of a file (or, when used with a pipe, the output of a previous command).</p>

<p>By default the <code>head</code> and <code>tail</code> commands will display ten lines.  For example, the following command will display the first ten lines of the <code class="console">/etc/sysctl.conf</code> file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> head /etc/sysctl.conf                            
#                                                                     
# /etc/sysctl.conf - Configuration file for setting system variables  
# See /etc/sysctl.d/ for additional system variables                   
# See sysctl.conf (5) for information.                                 
#                                                                     

#kernel.domainname = example.com                                                
                                                               
# Uncomment the following to stop low-level messages on console
#kernel.printk = 3 4 1 3                                        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
<p>In the next example, the last ten lines of the file will be displayed:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> tail /etc/sysctl.conf                            
# Do not send ICMP redirects (we are not a router)                    
#net.ipv4.conf.all.send_redirects = 0                                  
#                                                                      
# Do not accept IP source route packets (we are not a router)         
#net.ipv4.conf.all.accept_source_route = 0                             
#net.ipv6.conf.all.accept_source_route = 0                             
#                                                                      
# Log Martian Packets                                                  
#net.ipv4.conf.all.log_martians = 1                                    
#                                                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>The pipe character will allow users to utilize these commands not only on files, but on the output of other commands.  This can be useful when listing a large directory, for example the <code class="console">/etc</code> directory:</p>

<pre class="content_terminal"><strong><span class="ansi-blue">ca-certificates         insserv</span></strong>              nanorc          services   
ca-certificates.conf    insserv.conf         <strong><span class="ansi-blue">network         sgml</span></strong>      
<strong><span class="ansi-blue">calendar                insserv.conf.d</span></strong>       networks        shadow    
<strong><span class="ansi-blue">cron.d                  iproute2</span></strong>             <strong><span class="ansi-red">nologin</span></strong>         shadow-   
<strong><span class="ansi-blue">cron.daily</span></strong>              issue                nsswitch.conf   shells    
<strong><span class="ansi-blue">cron.hourly</span></strong>             issue.net            <strong><span class="ansi-blue">opt             skel</span></strong>     
<strong><span class="ansi-blue">cron.monthly            kernel</span></strong>               os-release      <strong><span class="ansi-blue">ssh</span></strong>       
<strong><span class="ansi-blue">cron.weekly</span></strong>             ld.so.cache          pam.conf        <strong><span class="ansi-blue">ssl</span></strong>      
crontab                 ld.so.conf           <strong><span class="ansi-blue">pam.d</span></strong>           sudoers   
<strong><span class="ansi-blue">dbus-1                  ld.so.conf.d</span></strong>         passwd          <strong><span class="ansi-blue">sudoers.d</span></strong> 
debconf.conf            ldap                 passwd-         sysctl.conf
debian_version          legal                perl            sysctl.d  
<strong><span class="ansi-blue">default</span></strong>                 locale.alias         pinforc         <strong><span class="ansi-blue">systemd</span></strong>   
deluser.conf            localtime            <strong><span class="ansi-blue">ppp             terminfo</span></strong>  
<strong><span class="ansi-blue">depmod.d                logcheck</span></strong>             profile         timezone  
<strong><span class="ansi-blue">dpkg</span></strong>                    login.defs           profile.d       ucf.conf  
environment             logrotate.conf       protocols       <strong><span class="ansi-blue">udev</span></strong>      
fstab                   <strong><span class="ansi-blue">logrotate.d          python2.7       ufw</span></strong>       
<strong><span class="ansi-blue">fstab.d                 lsb-base</span></strong>             <strong><span class="ansi-green">rc.local</span></strong>        <strong><span class="ansi-blue">update-motd.d</span></strong>
gai.conf                lsb-base-logging.sh  <strong><span class="ansi-blue">rc0.d</span></strong>           updatedb.conf 
<strong><span class="ansi-blue">groff</span></strong>                   lsb-release          <strong><span class="ansi-blue">rc1.d           vim</span></strong>       
group                   magic                <strong><span class="ansi-blue">rc2.d</span></strong>           wgetrc    
group-                  magic.mime           <strong><span class="ansi-blue">rc3.d           xml</span></strong>      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre> 

<p>If you look at the output of the previous command, you will note that first filename is <code class="console">ca-certificates</code>.  But there are other files listed "above" that can only be viewed if the user uses the scroll bar.  What if you just wanted to list the first few files of the <code class="console">/etc</code> directory? </p>

<p>Instead of displaying the full output of the above command, piping it to the <code>head</code> command will display only the first ten lines:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /etc | head                                   
adduser.conf                                                           
adjtime                                                               
alternatives                                                         
apparmor.d                                                             
apt                                                                    
bash.bashrc                                                           
bash_completion.d                                                     
bind                                                                  
bindresvport.blacklist                                                 
blkid.conf                                                             
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          

<p>The full output of the <code>ls</code> command is passed to the <code>head</code> command by the shell instead of being printed to the screen.  The <code>head</code> command takes this output (from <code>ls</code>) as "input data" and the output of <code>head</code> is then printed to the screen.</p>

<p>Multiple pipes can be used consecutively to link multiple commands together.  If three commands are piped together, the first command's output is passed to the second command.  The output of the second command is then passed to the third command.  The output of the third command would then be printed to the screen.</p> 

<p>It is important to carefully choose the order in which commands are piped, as the third command will only see input from the output of the second.  The examples below illustrate this using the <code>nl</code> command.  In the first example, the <code>nl</code> command is used to number the lines of the output of a previous command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l /etc/ppp | nl                                   1  total 44
     2  -rw------- 1 root root   78 Aug 22  2010 chap-secrets         
     3  -rwxr-xr-x 1 root root  386 Apr 27  2012 ip-down
     4  -rwxr-xr-x 1 root root 3262 Apr 27  2012 ip-down.ipv6to4      
     5  -rwxr-xr-x 1 root root  430 Apr 27  2012 ip-up  
     6  -rwxr-xr-x 1 root root 6517 Apr 27  2012 ip-up.ipv6to4
     7  -rwxr-xr-x 1 root root 1687 Apr 27  2012 ipv6-down
     8  -rwxr-xr-x 1 root root 3196 Apr 27  2012 ipv6-up
     9  -rw-r--r-- 1 root root    5 Aug 22  2010 options
    10  -rw------- 1 root root   77 Aug 22  2010 pap-secrets
    11  drwxr-xr-x 2 root root 4096 Jun 22  2012 peers                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
<p>In the next example, note that the <code>ls</code> command is executed first and its output is sent to the <code>nl</code> command, numbering all of the lines from the output of the <code>ls</code> command.  Then the <code>tail</code> command is executed, displaying the last five lines from the output of the <code>nl</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l /etc/ppp | nl | tail -5                   
     7  -rwxr-xr-x 1 root root 1687 Apr 27  2012 ipv6-down
     8  -rwxr-xr-x 1 root root 3196 Apr 27  2012 ipv6-up
     9  -rw-r--r-- 1 root root    5 Aug 22  2010 options
    10  -rw------- 1 root root   77 Aug 22  2010 pap-secrets
    11  drwxr-xr-x 2 root root 4096 Jun 22  2012 peers                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>Compare the output above with the next example:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l /etc/ppp | tail -5 | nl                   
    1  -rwxr-xr-x 1 root root 1687 Apr 27  2012 ipv6-down
    2  -rwxr-xr-x 1 root root 3196 Apr 27  2012 ipv6-up
    3  -rw-r--r-- 1 root root    5 Aug 22  2010 options
    4  -rw------- 1 root root   77 Aug 22  2010 pap-secrets
    5  drwxr-xr-x 2 root root 4096 Jun 22  2012 peers                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>Notice how the line numbers are different.  Why is this?</p>

<p>In the second example, the output of the <code>ls</code> command is first sent to the <code>tail</code> command which "grabs" only the last five lines of the output.  Then the <code>tail</code> command sends those five lines to the <code>nl</code> command, which numbers them <code class="console">1</code>-<code class="console">5</code>.</p>

<p>Pipes can be powerful, but it is important to consider how commands are piped to ensure that the desired output is displayed.</p>

<h2><a name="#2">1.2 I/O Redirection</a></h2>
<p>Input/Output (I/O) redirection allows for command line information to be passed to different <var>streams</var>.  Before discussing redirection, it is important to understand standard streams.</p>

<h2><a name="#3">1.2.1 STDIN</a></h2>
<p>Standard input, or STDIN, is information entered normally by the user via the keyboard.  When a command prompts the shell for data, the shell provides the user with the ability to type commands that, in turn, are sent to the command as STDIN.</p>

<h2><a name="#4">1.2.2 STDOUT</a></h2>
<p>Standard output, or STDOUT, is the normal output of commands.  When a command functions correctly (without errors) the output it produces is called STDOUT.  By default, STDOUT is displayed in the terminal window (screen) where the command is executing.</p>

<h2><a name="#5">1.2.3 STDERR</a></h2>
<p>Standard error, or STDERR, are error messages generated by commands.  By default, STDERR is displayed in the terminal window (screen) where the command is executing.</p>

<p>I/O redirection allows the user to redirect STDIN so data comes from a file and STDOUT/STDERR so output goes to a file.  Redirection is achieved by using the arrow characters: <code class="console"> &lt;</code> and <code class="console"> &gt;</code> .</p>

<h2><a name="#6">1.2.4 Redirecting STDOUT</a></h2>
<p>STDOUT can be directed to files.  To begin, observe the output of the following command which will display to the screen:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo "Line 1"                                    
Line 1                                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>Using the <code class="console">&gt;</code> character the output can be redirected to a file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo "Line 1" &gt; example.txt                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  example.txt  <strong><span class="ansi-blue">test</span></strong>           
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>     sample.txt                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                  
Line 1                                                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>             

<p>This command displays no output, because STDOUT was sent to the file <code>example.txt</code> instead of the screen.  You can see the new file with the output of the <code>ls</code> command.  The newly-created file contains the output of the <code>echo</code> command when the file is viewed with the <code>cat</code> command.</p>

<p>It is important to realize that the single arrow will overwrite any contents of an existing file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                  
Line 1                                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo "New line 1" &gt; example.txt                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                  
New line 1                                                             
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
<p>The original contents of the file are gone, replaced with the output of the new <code>echo</code> command.</p>
 
<p>It is also possible to preserve the contents of an existing file by appending to it.  Use "double arrow"  <code class="console">&gt;&gt;</code>  to append to a file instead of overwriting it:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                  
New line 1                                                             
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo "Another line" &gt;&gt; example.txt              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                  
New line 1                                                             
Another line                                                          
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
<p>Instead of being overwritten, the output of the most recent <code>echo</code> command is added to the bottom of the file.</p>

<h2><a name="#7">1.2.5 Redirecting STDERR</a></h2>
<p>STDERR can be redirected in a similar fashion to STDOUT.  STDOUT is also known as <var>stream</var> (or <var>channel</var>) #1.  STDERR is assigned stream #2.</p>

<p>When using arrows to redirect, stream #1 is assumed unless another stream is specified.  Thus, stream #2 must be specified when redirecting STDERR.</p> 

<p>To demonstrate redirecting STDERR, first observe the following command which will produce an error because the specified directory does not exist:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake                                 
ls: cannot access /fake: No such file or directory              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>Note that there is nothing in the example above that implies that the output is STDERR.  The output is clearly an error message, but how could you tell that it is being sent to STDERR?  One easy way to determine this is to redirect STDOUT:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake &gt; output.txt                    
ls: cannot access /fake: No such file or directory              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>In the example above, STDOUT was redirected to the <code class="console">output.txt</code> file.  So, the output that is displayed can't be STDOUT because it would have been placed in the <code class="console">output.txt</code> file.  Because all command output goes either to STDOUT or STDERR, the output displayed above must be STDERR.</p>

<p>The STDERR output of a command can be sent to a file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake 2&gt; error.txt                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> more error.txt                            
ls: cannot access /fake: No such file or directory              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre> 

<p>In the command above, the <code class="console">2&gt;</code> indicates that all error messages should be sent to the file <code class="console">error.txt</code>.</p>

<h2><a name="#8">1.2.6 Redirecting Multiple Streams</a></h2>
<p>It is possible to direct both the STDOUT and STDERR of a command at the same time.  The following command will produce both STDOUT and STDERR because one of the specified directories exists and the other does not:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake /etc/ppp                         
ls: cannot access /fake: No such file or directory              
/etc/ppp:                                                       
chap-secrets   <span class="ansi-green">ip-down   ip-down.ipv6to4    ip-up        ip-up.ipv6to4</span>
<span class="ansi-green">ipv6-down      ipv6-up</span>   options            pap-secrets  <strong><span class="ansi-blue">peers</span></strong> 
</pre>                                                                           

<p>If only the STDOUT is sent to a file, STDERR will still be printed to the screen:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake /etc/ppp &gt; example.txt           
ls: cannot access /fake: No such file or directory              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                           
/etc/ppp:                                              
chap-secrets         
ip-down
ip-down.ipv6to4      
ip-up  
ip-up.ipv6to4
ipv6-down
ipv6-up
options
pap-secrets
peers                                                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>      

<p>If only the STDERR is sent to a file, STDOUT will still be printed to the screen:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake /etc/ppp 2&gt; error.txt            
/etc/ppp:                                                       
hap-secrets    <span class="ansi-green">ip-down   ip-down.ipv6to4    ip-up        ip-up.ipv6to4</span>
<span class="ansi-green">ipv6-down      ipv6-up</span>   options            pap-secrets  <strong><span class="ansi-blue">peers</span></strong> 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat error.txt                             
ls: cannot access /fake: No such file or directory              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                       
    
<p>Both STDOUT and STDERR can be sent to a file by using <code class="console">&amp;&gt;</code>, a character set that means "both <code class="console">1&gt;</code> and <code class="console">2&gt;</code>”:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake /etc/ppp &amp;&gt; all.txt          
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat all.txt                               
ls: cannot access /fake: No such file or directory              
/etc/ppp:                                                       
chap-secrets         
ip-down
ip-down.ipv6to4      
ip-up  
ip-up.ipv6to4
ipv6-down
ipv6-up
options
pap-secrets
peers                                                            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>    
  
<p>Note that when you use <code class="console">&amp;&gt;</code>, the output appears in the file with all of the STDERR messages at the top and all of the STDOUT messages below all STDERR messages:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake /etc/ppp /junk /etc/sound &amp;&gt; all.txt       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat all.txt                               
ls: cannot access /fake: No such file or directory              
ls: cannot access /junk: No such file or directory              
/etc/ppp:                                                       
chap-secrets         
ip-down
ip-down.ipv6to4      
ip-up  
ip-up.ipv6to4
ipv6-down
ipv6-up
options
pap-secrets
peers                 

/etc/sound:
events                                                                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>If you don't want STDERR and STDOUT to both go to the same file, they can be redirected to different files by using both <code class="console">&gt; and 2&gt;</code>.  For example:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> rm error.txt example.txt                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                        
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  all.txt              
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>               
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /fake /etc/ppp &gt; example.txt 2&gt; error.txt        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                        
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  all.txt    example.txt
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>     error.txt  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat error.txt                             
ls: cannot access /fake: No such file or directory              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                           
/etc/ppp:                                                       
chap-secrets         
ip-down
ip-down.ipv6to4      
ip-up  
ip-up.ipv6to4
ipv6-down
ipv6-up
options
pap-secrets
peers                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                        
<div class="alert alert-info">The order the streams are specified in does not matter.</div>

<h2><a name="#9">1.2.7 Redirecting STDIN</a></h2>
<p>The concept of redirecting STDIN is a difficult one because it is more difficult to understand <var>why</var> you would want to redirect STDIN.  With STDOUT and STDERR, the answer to <var>why</var> is fairly easy: because sometimes you want to store the output into a file for future use.</p>

<p>Most Linux users end up redirecting STDOUT routinely, STDERR on occasion and STDIN...well, very rarely.  There are very few commands that require you to redirect STDIN because with most commands if you want to read data from a file into a command, you can just specify the filename as an argument to the command.  The command will then look into the file.</p>

<p>For some commands, if you don't specify a filename as an argument, they will revert to using STDIN to get data.  For example, consider the following <code>cat</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat                                       
hello                                                           
hello                                                           
how are you?                                                    
how are you?                                                    
goodbye                                                         
goodbye
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>                     

<p>In the example above, the <code>cat</code> command wasn't provided a filename as an argument.  So, it asked for the data to display on the screen from STDIN.  The user typed <code class="console">hello</code> and then the <code>cat</code> command displayed <code class="console">hello</code> on the screen.  Perhaps this is useful for lonely people, but not really a good use of the <code>cat</code> command.  </p>

<p>However, perhaps if the output of the <code>cat</code> command were redirected to a file, then this method could be used either to add to an existing file or to place text into a new file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat &gt; new.txt                             
Hello                                                           
How are you?                                                    
Goodbye                                                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat new.txt                               
Hello                                                           
How are you?                                                    
Goodbye
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                   
 
<p>While the previous example demonstrates another advantage of redirecting STDOUT, it doesn't address why or how STDIN can be directed.  To understand this, first consider a new command called <code>tr</code>.  This command will take a set of characters and translate them into another set of characters.</p>

<p>For example, suppose you wanted to capitalize a line of text.  You could use the <code>tr</code> command as follows:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> tr 'a-z' 'A-Z'                         
watch how this works                                            
WATCH HOW THIS WORKS                                            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                         
<p>The <code>tr</code> command took the STDIN from the keyboard (<code class="console">watch how this works</code>) and converted all lower case letters before sending STDOUT to the screen (<code class="console">WATCH HOW THIS WORKS</code>).</p>

<p>It would seem that a better use of the <code>tr</code> command would be to perform translation on a file, not keyboard input.  However, the <code>tr</code> command does not support filename arguments:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> more example.txt                                
/etc/ppp:
chap-secrets
ip-down
ip-down.ipv6to4
ip-up
ip-up.ipv6to4
ipv6-down
ipv6-up
options
pap-secrets
peers                                          
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> tr 'a-z' 'A-Z' example.txt
tr: extra operand `example.txt'
Try `tr --help' for more information
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
<p>You can, however, tell the shell to get STDIN from a file instead of from the keyboard by using the <code class="console">&lt;</code> character:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> tr 'a-z' 'A-Z' &lt; example.txt 
/ETC/PPP:                   
CHAP-SECRETS                                             
IP-DOWN                                                               
IP-DOWN.IPV6TO4                                                      
IP-UP                                                                 
IP-UP.IPV6TO4                                                         
IPV6-DOWN                                                             
IPV6-UP                                                               
OPTIONS                                                               
PAP-SECRETS                                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>This is fairly rare because most commands do accept filenames as arguments.  But, for those that do not, this method could be used to have the shell read from the file instead of relying on the command to have this ability.</p>

<p>One last note: In most cases you probably want to take the resulting output and place it back into another file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> tr 'a-z' 'A-Z' &lt; example.txt &gt; newexample.txt 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> more newexample.txt
/ETC/PPP:           
CHAP-SECRETS                                             
IP-DOWN                                                               
IP-DOWN.IPV6TO4                                                      
IP-UP                                                                 
IP-UP.IPV6TO4                                                         
IPV6-DOWN                                                             
IPV6-UP                                                               
OPTIONS                                                               
PAP-SECRETS                                                          
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<h2><a name="#10">1.3 Searching for Files Using the Find Command</a></h2>
<p>One of the challenges that users face when working with the filesystem, is trying to recall the location where files are stored.  There are thousands of files and hundreds of directories on a typical Linux filesystem, so recalling where these files are located can pose challenges.</p>

<p>Keep in mind that most of the files that you will work with are ones that you create.  As a result, you often will be looking in your own home directory to find files.  However, sometimes you may need to search in other places on the filesystem to find files created by other users.</p>

<p>The <code>find</code> command is a very powerful tool that you can use to search for files on the filesystem.  This command can search for files by name, including using wildcard characters for when you are not certain of the exact filename.  Additionally, you can search for files based on file metadata, such as file type, file size and file ownership.</p>

<p>The syntax of the <code>find</code> command is:</p>

<pre class="config">find [starting directory] [search option] [search criteria] [result option]</pre>

<p>A description of all of these components:</p>

<table class="table ">
<thead><tr>
<th>Component</th>
<th>Description</th>
</tr></thead>
<tbody>
<tr>
<td>[starting&nbsp;directory]</td>
<td>This is where the user specifies where to start searching.  The <code>find</code> command will search this directory and all of its subdirectories.  If no starting directory is provided, then the current directory is used for the starting point.</td>
</tr>
<tr>
<td>[search&nbsp;option]</td>
<td>This is where the user specifies an option to determine what sort of metadata to search for; there are options for file name, file size and many other file attributes.</td>
</tr>
<tr>
<td>[search&nbsp;criteria]</td>
<td>This is an argument that compliments the search option.  For example, if the user uses the option to search for a file name, the search criteria would be the filename.</td>
</tr>
<tr>
<td>[result&nbsp;option]</td>
<td>This option is used to specify what action should be taken once the file is found.  If no option is provided, the file name will be printed to STDOUT.</td>
</tr>
</tbody>
</table>

<h2><a name="#11">1.3.1 Search by File Name</a></h2>
<p>To search for a file by name, use the <code>-name</code> option to the <code>find</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> find /etc -name hosts                           
find: `/etc/dhcp': Permission denied
find: `/etc/cups/ssl': Permission denied  
find: `/etc/pki/CA/private': Permission denied  
find: `/etc/pki/rsyslog': Permission denied
find: `/etc/audisp': Permission denied 
find: `/etc/named': Permission denied
find: `/etc/lvm/cache': Permission denied 
find: `/etc/lvm/backup': Permission denied
find: `/etc/lvm/archive': Permission denied                           
/etc/hosts
find: `/etc/ntp/crypto': Permission denied
find: `/etc/polkit-l/localauthority': Permission denied   
find: `/etc/sudoers.d': Permission denied  
find: `/etc/sssd': Permission denied 
/etc/avahi/hosts
find: `/etc/selinux/targeted/modules/active': Permission denied  
find: `/etc/audit': Permission denied                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>Note that two files were found: <code class="console">/etc/hosts</code> and <code class="console">/etc/avahi/hosts</code>.  The rest of the output was STDERR messages because the user who ran the command didn't have the permission to access certain subdirectories.</p>

<p>Recall that you can redirect STDERR to a file so you don't need to see these error messages on the screen:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> find /etc -name hosts 2&gt; errors.txt             
/etc/hosts 
/etc/avahi.hosts                                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>While the output is easier to read, there really is no purpose to storing the error messages in the <code class="console">error.txt</code> file.  The developers of Linux realized that it would be good to have a "junk file" to send unnecessary data; any file that you send to the <code class="console">/dev/null</code> file is discarded:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> find /etc -name hosts 2&gt; /dev/null              
/etc/hosts
/etc/avahi/hosts                                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre> 

<h2><a name="#12">1.3.2 Displaying File Detail</a></h2>
<p>It can be useful to obtain file details when using the <code>find</code> command because just the file name itself might not be enough information for you to find the correct file.</p>

<p>For example, there might be seven files named hosts; if you knew that the host file that you needed had been modified recently, then the modification timestamp of the file would be useful to see.</p>

<p>To see these file details, use the <code>-ls</code> option to the <code>find</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> find /etc -name hosts -ls 2&gt; /dev/null
    41   4 -rw-r--r--   1 root     root      158 Jan 12 2010 /etc/hosts
  6549   4 -rw-r--r--   1 root     root      1130 Jul 19 2011 /etc/avahi/hosts 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<div class="alert alert-info">
<strong>Note:</strong> The first two columns of the output above are the <var>inode number</var> of the file and the number of <var>blocks</var> that the file is using for storage.  Both of these are beyond the scope of the topic at hand.  The rest of the columns are typical output of the <code>ls -l</code> command: file type, permissions, hard link count, user owner, group owner, file size, modification timestamp and file name.</div>


<h2><a name="#13">1.3.3 Searching for Files by Size</a></h2>
<p>One of the many useful searching options is the option that allows you to search for files by size.  The <code>-size</code> option allows you to search for files that are either larger than or smaller then a specified size as well as search for an exact file size.</p>

<p>When you specify a file size, you can give the size in bytes (c), kilobytes (k), megabytes (M) or gigabytes (G).  For example, the following will search for files in the /etc directory structure that are exactly 10 bytes large:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> find /etc -size 10c -ls 2&gt;/dev/null    
   432    4 -rw-r--r--   1 root     root           10 Jan 28  2015 /etc/adjtime
 8814    0 drwxr-xr-x   1 root     root           10 Jan 29  2015 /etc/ppp/ip-d
own.d                                                           
8816    0 drwxr-xr-x   1 root     root           10 Jan 29  2015 /etc/ppp/ip-u
p.d                                                            
 8921    0 lrwxrwxrwx   1 root     root           10 Jan 29  2015 /etc/ssl/cert
s/349f2832.0 -&gt; EC-ACC.pem                                    
  9234    0 lrwxrwxrwx   1 root     root           10 Jan 29  2015 /etc/ssl/cert
s/aeb67534.0 -&gt; EC-ACC.pem                                     
 73468    4 -rw-r--r--   1 root     root           10 Nov 16 20:42 /etc/hostname
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>If you want to search for files that are larger than a specified size, you place a <code class="console">+</code> character before the size.  For example, the following will look for all files in the <code class="console">/usr</code> directory structure that are over 100 megabytes in size:</p>
 
<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> find /usr -size +100M -ls 2&gt; /dev/null
574683 104652 -rw-r--r--   1 root      root      107158256 Aug  7 11:06 /usr/share/icons/oxygen/icon-theme.cache                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>To search for files that are smaller than a specified size, place a <code class="console">-</code> character before the file size.</p>


<h2><a name="#14">1.3.4 Additional Useful Search Options</a></h2>
<p>There are many search options.  The following table illustrates a few of these options:</p>

<table class="table ">
<thead><tr>
<th>Option</th>
<th>Meaning</th>
</tr></thead>
<tbody>
<tr>
<td><code>-maxdepth</code></td>
<td>Allows the user to specify how deep in the directory structure to search.  For example, <code>-maxdepth 1</code> would mean only search the specified directory and its immediate subdirectories. </td>
</tr>
<tr>
<td><code>-group</code></td>
<td>Returns files owned by a specified group.  For example, <code>-group payroll</code> would return files owned by the payroll group.</td>
</tr>
<tr>
<td><code>-iname</code></td>
<td>Returns files that match specified filename, but unlike <code>-name</code>, <code>-iname</code> is case insensitive.  For example, <code>-iname hosts</code> would match files named <code class="console">hosts</code>, <code class="console">Hosts</code>, <code class="console">HOSTS</code>, etc.</td>
</tr>
<tr>
<td><code>-mmin</code></td>
<td>Returns files that were modified based on modification time in minutes.  For example, <code>-mmin 10</code> would match files that were modified 10 minutes ago.</td>
</tr>
<tr>
<td><code>-type</code></td>
<td>Returns files that match file type.  For example, <code>-type f</code> would return files that are regular files.</td>
</tr>
<tr>
<td><code>-user</code></td>
<td>Returns files owned by a specified user.  For example, <code>-user bob</code> would return files owned by the <code class="console">bob</code> user.</td>
</tr>
</tbody>
</table>

<h2><a name="#15">1.3.5 Using Multiple Options</a></h2>
<p>If you use multiple options, they act as an "and", meaning for a match to occur, all of the criteria must match, not just one.  For example, the following command will display all files in the <code class="console">/etc</code> directory structure that are 10 bytes in size <var>and</var> are plain files:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> find /etc -size 10c -type f -ls 2&gt;/dev/null       
432    4 -rw-r--r--   1 root     root           10 Jan 28  2015 /etc/adjtime
73468    4 -rw-r--r--   1 root     root           10 Nov 16 20:42 /etc/hostname
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<h2><a name="#16">1.4 Viewing Files Using the less Command</a></h2>
<p>While viewing small files with the <code>cat</code> command poses no problems, it is not an ideal choice for large files.  The <code>cat</code> command doesn't provide any way to easily pause and restart the display, so the entire file contents are dumped to the screen.</p>

<p>For larger files, you will want to use a <var>pager</var> command to view the contents.  Pager commands will display one page of data at a time, allowing you to move forward and backwards in the file by using movement keys.  </p>

<p>There are two commonly used pager commands:</p>

<ul type="disc" class="">
<li>The <code>less</code> command: This command provides a very advanced paging capability.  It is normally the default pager used by commands like the <code>man</code> command.</li>
<li>The <code>more</code> command: This command has been around since the early days of UNIX.  While it has fewer features than the <code>less</code> command, it does have one important advantage: The <code>less</code> command isn't always included with all Linux distributions (and on some distributions, it isn't installed by default).  The <code>more</code> command is always available.</li>
</ul>

<p>When you use the <code>more</code> or <code>less</code> commands, they will allow you to "move around" a document by using <var>keystroke commands</var>.  Because the developers of the <code>less</code> command based the command from the functionality of the <code>more </code>command, all of the keystroke commands available in the <code>more</code> command also work in the <code>less</code> command.</p>

<p>For the purpose of this manual, the focus will be on the more advanced command (<code>less</code>).  The <code>more</code> command is still useful to remember for times when the <code>less</code> command isn't available.  Remember that most of the keystroke commands provided work for both commands.</p>

<h2><a name="#17">1.4.1 Help Screen in less</a></h2>
<p>When you view a file with the <code>less</code> command, you can use the <strong>h</strong> key to display a help screen.  The help screen allows you to see which other commands are available.  In the following example, the <code>less /usr/share/dict/words</code> command is executed.  Once the document is displayed, the <strong>h</strong> key was pressed, displaying the help screen:</p>

 <pre class="content_terminal">                    SUMMARY OF LESS COMMANDS                                     
      Commands marked with * may be preceded by a number, N.      
      Notes in parentheses indicate the behavior if N is given.                 
                                                                       
  h  H                 Display this help.                              
  q  :q  Q  :Q  ZZ     Exit.                                           
 ------------------------------------------------------------------------ 
                           MOVING                                               
                                                                        
  e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).                 
  y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).               
  f  ^F  ^V  SPACE  *  Forward  one window (or N lines).                
  b  ^B  ESC-v      *  Backward one window (or N lines).               
  z                 *  Forward  one window (and set window to N).       
  w                 *  Backward one window (and set window to N).               
  ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.    
  d  ^D             *  Forward  one half-window (and set half-window to N).     
  u  ^U             *  Backward one half-window (and set half-window to N).     
  ESC-)  RightArrow *  Left  one half screen width (or N positions).    
  ESC-(  LeftArrow  *  Right one half screen width (or N positions).      
HELP -- Press RETURN for more, or q when done</pre>

<h2><a name="#18">1.4.2 less Movement Commands</a></h2>
<p>There are many movement commands for the <code>less</code> command, each with multiple possible keys or key combinations.  While this may seem intimidating, remember you don't need to memorize all of these movement commands; you can always use the <strong>h</strong> key whenever you need to get help.</p>

<p>The first group of movement commands that you may want to focus upon are the ones that are most commonly used.  To make this even easier to learn, the keys that are identical in <code>more</code> and <code>less</code> will be summarized.  In this way, you will be learning how to move in <code>more</code> and <code>less</code> at the same time:</p>

<table class="table ">
<thead><tr>
<th>Movement</th>
<th>Key</th>
</tr></thead>
<tbody>
<tr>
<td>Window forward</td>
<td><strong>Spacebar</strong></td>
</tr>
<tr>
<td>Window backward</td>
<td><strong>b</strong></td>
</tr>
<tr>
<td>Line forward</td>
<td><strong>Enter</strong></td>
</tr>
<tr>
<td>Exit</td>
<td><strong>q</strong></td>
</tr>
<tr>
<td>Help</td>
<td><strong>h</strong></td>
</tr>
</tbody>
</table>

<p>When simply using <code>less</code> as a pager, the easiest way to advance forward a page is to press the <strong>spacebar</strong>.</p>

<h2><a name="#19">1.4.3 less Searching Commands</a></h2>
<p>There are two ways to search in the <code>less</code> command: you can either search forward or backwards from your current position using patterns called regular expressions.  More details regarding regular expressions are provided later in this chapter. </p>

<p>To start a search to look forward from your current position, use the <strong>/</strong> key.  Then, type the text or pattern to match and press the <strong>Enter</strong> key. </p>

<p>If a match can be found, then your cursor will move in the document to the match.  For example, in the following graphic the expression "frog" was searched for in the <code class="console">/usr/share/dict/words</code> file:</p>

<pre class="content_terminal">bull<code class="input">frog</code>                                                                
bull<code class="input">frog</code>'s                                                              
bull<code class="input">frog</code>s                                                               
bullheaded                                                              
bullhorn                                                                
bullhorn's                                                              
bullhorns                                                               
bullied                                                                 
bullies                                                                 
bulling                                                                 
bullion                                                                 
bullion's                                                              
bullish                                                                 
bullock                                                                 
bullock's                                                               
bullocks                                                                
bullpen                                                                 
bullpen's                                                               
bullpens                                                                
bullring                                                                
bullring's                                                              
bullrings                                                               
bulls                                                                    
:</pre>

<p>Notice that "frog" didn't have to be a word by itself.  Also notice that while the <code>less</code> command took you to the first match from the current position, all matches were highlighted.</p>

<p>If no matches forward from your current position can be found, then the last line of the screen will report “<code class="console">Pattern not found</code>“:</p>

<pre class="content_terminal"><code class="input">Pattern not found  (press RETURN)</code></pre> 
 
<p>To start a search to look backwards from your current position, press the <strong>?</strong>  key, then type the text or pattern to match and press the <strong>Enter</strong> key.  Your cursor will move backward to the first match it can find or report that the pattern cannot be found.</p>

<p>If more than one match can be found by a search, then using the <strong>n</strong> key will allow you to move to the next match and using the <strong>N</strong> key will allow you to go to a previous match.</p>

<h2><a name="#20">1.5 Revisiting the head and tail Commands</a></h2>
<p>Recall that the <code>head</code> and <code>tail</code> commands are used to filter files to show a limited number of lines.  If you want to view a select number of lines from the top of the file, you use the <code>head</code> command and if you want to view a select number of lines at the bottom of a file, then you use the <code>tail</code> command. </p>

<p>By default, both commands display ten lines from the file.  The following table provides some examples:</p>

<table class="table ">
<thead><tr>
<th>Command Example</th>
<th>Explanation of Displayed Text</th>
</tr></thead>
<tbody>
<tr>
<td><code>head /etc/passwd</code></td>
<td>First ten lines of <code class="console">/etc/passwd</code>
</td>
</tr>
<tr>
<td><code>head -3 /etc/group</code></td>
<td>First three lines of <code class="console">/etc/group</code>
</td>
</tr>
<tr>
<td><code>head -n 3 /etc/group</code></td>
<td>First three lines of <code class="console">/etc/group</code>
</td>
</tr>
<tr>
<td><code>help | head</code></td>
<td>First ten lines of output piped from the <code>help</code> command</td>
</tr>
<tr>
<td><code>tail /etc/group</code></td>
<td>Last ten lines of <code class="console">/etc/group</code>
</td>
</tr>
<tr>
<td><code>tail -5 /etc/passwd</code></td>
<td>Last five lines of <code class="console">/etc/passwd</code>
</td>
</tr>
<tr>
<td><code>tail -n 5 /etc/passwd</code></td>
<td>Last five lines of <code class="console">/etc/passwd</code>
</td>
</tr>
<tr>
<td><code>help | tail</code></td>
<td>Last ten lines of output piped from the <code>help</code> command</td>
</tr>
</tbody>
</table>

<p>As seen from the above examples, both commands will output text from either a regular file or from the output of any command sent through a pipe.  They both use the <code>-n</code> option to indicate how many lines to output.</p>


<h2><a name="#21">1.5.1 Negative Value with the -n Option</a></h2>
<p>Traditionally in UNIX, the number of lines to output would be specified as an option with either command, so <code>-3</code> meant show three lines.  For the <code>tail</code> command, either <code>-3</code> or <code>-n -3</code> still means show three lines.  However, the GNU version of the <code>head</code> command recognizes <code>-n -3</code> as show <strong>all but the last three lines</strong>, and yet the <code>head </code>command still recognizes the option <code>-3</code> as show the first three lines.</p>

<h2><a name="#22">1.5.2 Positive Value With the tail Command</a></h2>
<p>The GNU version of the <code>tail</code> command allows for a variation of how to specify the number of lines to be printed.  If you use the <code>-n</code> option with a number prefixed by the plus sign, then the <code>tail</code> command recognizes this to mean to display the contents starting at the specified line and continuing all the way to the end. </p>

<p>For example, the following will display line #<code class="console">22</code> to the end of the output of the <code>nl</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> nl /etc/passwd | tail -n +22                     
    22  sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin               
    23  operator:x:1000:37::/root:/bin/sh                               
    24  sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<h2><a name="#23">1.5.3 Following Changes to a File</a></h2>
<p>You can view live file changes by using the <code>-f</code> option to the <code>tail</code> command.  This is useful when you want to see changes to a file as they are happening.</p>

<p>A good example of this would be when viewing log files as a system administrator.  Log files can be used to troubleshoot problems and administrators will often view them "interactively" with the <code>tail</code> command as they are performing the commands they are trying to troubleshoot in a separate window.</p>

<p>For example, if you were to log in as the <code class="console">root</code> user, you could troubleshoot issues with the email server by viewing live changes to its log file with the following command: <code>tail -f /var/log/mail.log</code></p>

<h2><a name="#24">1.6 Sorting Files or Input</a></h2>
<p>The <code>sort</code> command can be used to rearrange the lines of files or input in either dictionary or numeric order based upon the contents of one or more fields.  Fields are determined by a field separator contained on each line, which defaults to whitespace (spaces and tabs). </p>
<p>The following example creates a small file, using the <code>head</code> command to grab the first 5 lines of the <code class="console">/etc/passwd</code> file and send the output to a file called <code class="console">mypasswd</code>.</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> head -5 /etc/passwd &gt; mypasswd                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat mypasswd                                      
root:x:0:0:root:/root:/bin/bash                                         
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                   
bin:x:2:2:bin:/bin:/bin/sh                                              
sys:x:3:3:sys:/dev:/bin/sh                                              
sync:x:4:65534:sync:/bin:/bin/sync                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>Now we will <code>sort</code> the <code class="console">mypasswd</code> file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> sort mypasswd                                     
bin:x:2:2:bin:/bin:/bin/sh                                              
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                   
root:x:0:0:root:/root:/bin/bash                                         
sync:x:4:65534:sync:/bin:/bin/sync                                      
sys:x:3:3:sys:/dev:/bin/sh                                              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<h2><a name="#25">1.6.1 Fields and Sort Options</a></h2>
<p>In the event that the file or input might be separated by another delimiter like a comma or colon, the <code>-t</code> option will allow for another field separator to be specified.  To specify fields to <code>sort</code> by, use the <code>-k</code> option with an argument to indicate the field number (starting with 1 for the first field). </p>

<p>The other commonly used options for the <code>sort</code> command are the <code>-n</code> to perform a numeric <code>sort</code> and <code>-r</code> to perform a reverse <code>sort</code>.</p>

<p>In the next example, the <code>-t</code> option is used to separate fields by a colon character and performs a numeric <code>sort</code> using the third field of each line:</p>
 
<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> sort -t: -n -k3 mypasswd                          
root:x:0:0:root:/root:/bin/bash                                         
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                   
bin:x:2:2:bin:/bin:/bin/sh                                              
sys:x:3:3:sys:/dev:/bin/sh                                              
sync:x:4:65534:sync:/bin:/bin/sync                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>Note that the <code>-r</code> option could have been used to reverse the <code>sort</code>, making the higher numbers in the third field appear at the top of the output:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> sort -t: -n -r -k3 mypasswd                       
sync:x:4:65534:sync:/bin:/bin/sync                                      
sys:x:3:3:sys:/dev:/bin/sh                                              
bin:x:2:2:bin:/bin:/bin/sh                                              
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                   
root:x:0:0:root:/root:/bin/bash                                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>Lastly, you may want to perform more complex sorts, such as <code>sort</code> by a primary field and then by a secondary field.  For example, consider the following data:</p>

<pre class="content_terminal">bob:smith:23
nick:jones:56
sue:smith:67</pre>

<p>You might want to <code>sort</code> first by the last name (field #2) and then first name (field #1) and then by age (field #3).  This can be done with the following command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> sort -t: -k2 -k1 -k3n <var>filename</var></pre>


<h2><a name="#26">1.7 Viewing File Statistics With the wc Command</a></h2>
<p>The <code>wc</code> command allows for up to three statistics to be printed for each file provided, as well as the total of these statistics if more than one filename is provided.  By default, the <code>wc</code> command provides the number of lines, words and bytes (1 byte = 1 character in a text file):</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> wc /etc/passwd /etc/passwd-                         
  35   56 1710 /etc/passwd                                                
  34   55 1665 /etc/passwd-                                          
  69  111 3375 total                                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>The above example shows the output from executing: <code>wc /etc/passwd /etc/passwd-</code>.  The output has four columns: number of lines in the file, number of words in the file, number of bytes in the file and the file name or <code class="console">total</code>. </p>

<p>If you are interested in viewing just specific statistics, then you can use <code>-l</code> to show just the number of lines, <code>-w</code> to show just the number of words and <code>-c</code> to show just the number of bytes.</p>

<p>The <code>wc</code> command can be useful for counting the number of lines output by some other command through a pipe.  For example, if you wanted to know the total number of files in the <code class="console">/etc</code> directory, you could execute <code>ls /etc | wc -l</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /etc/ | wc -l                                  
136                                                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>             

<h2><a name="#27">1.8 Using the cut Command to Filter File Contents</a></h2>
<p>The <code>cut</code> command can extract columns of text from a file or standard input.  A primary use of the <code>cut</code> command is for working with delimited database files.  These files are very common on Linux systems.</p>

<p>By default, it considers its input to be separated by the <strong>Tab</strong> character, but the <code>-d</code> option can specify alternative delimiters such as the colon or comma. </p>

<p>Using the <code>-f</code>option, you can specify which fields to display, either as a hyphenated range or a comma separated list. </p>

<p>In the following example, the first, fifth, sixth and seventh fields from <code class="console">mypasswd</code> database file are displayed:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cut -d: -f1,5-7 mypasswd                          
root:root:/root:/bin/bash                                               
daemon:daemon:/usr/sbin:/bin/sh                                        
bin:bin:/bin:/bin/sh                                                    
sys:sys:/dev:/bin/sh                                                    
sync:sync:/bin:/bin/sync                                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>       

<p>Using the <code>cut</code> command, you can also extract columns of text based upon character position with the <code>-c</code> option.  This can be useful for extracting fields from fixed-width database files.  For example, the following will display just the file type (character #1), permissions (characters #2-10) and filename (characters #50+) of the output of the <code>ls -l</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l | cut -c1-11,50-                            
total 12                                                                
drwxr-xr-x Desktop                                                      
drwxr-xr-x Documents                                                    
drwxr-xr-x Downloads                                                   
drwxr-xr-x Music                                                        
drwxr-xr-x Pictures                                                     
drwxr-xr-x Public                                                    
drwxr-xr-x Templates                                                   
drwxr-xr-x Videos                                                       
-rw-rw-r-- errors.txt                                                   
-rw-rw-r-- mypasswd                                                     
-rw-rw-r-- new.txt                                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>      

<h2><a name="#28">1.9 Using the grep Command to Filter File Contents</a></h2>
<p>The <code>grep</code> command can be used to filter lines in a file or the output of another command based on matching a pattern.  That pattern can be as simple as the exact text that you want to match or it can be much more advanced through the use of regular expressions (discussed later in this chapter).</p>

<p>For example, you may want to find all the users who can login to the system with the BASH shell, so you could use the <code>grep </code>command to filter the lines from the <code class="console">/etc/passwd</code> file for the lines containing the characters <code class="console">bash</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep bash /etc/passwd                             
root:x:0:0:root:/root:/bin/bash                                         
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>To make it easier to see what exactly is matched, use the <code>--color</code> option.  This option will highlight the matched items in red:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color bash /etc/passwd                             
root:x:0:0:root:/root:/bin/<strong><span class="ansi-red">bash</span></strong>                                         
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/<strong><span class="ansi-red">bash</span></strong>  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>In some cases you don't care about the specific lines that match the pattern, but rather how many lines match the pattern.  With the <code>-c</code> option, you can get a count of how many lines that match:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep -c bash /etc/passwd                          
2                                                                       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>When you are viewing the output from the <code>grep</code> command, it can be hard to determine the original line numbers.  This information can be useful when you go back into the file (perhaps to edit the file) as you can use this information to quickly find one of the matched lines.</p>

<p>The <code>-n</code> option to the <code>grep</code> command will display original line numbers:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep -n bash /etc/passwd                          
<span class="ansi-green">1</span><span class="ansi-blue">:</span>root:x:0:0:root:/root:/bin/bash                                       
<span class="ansi-green">24</span><span class="ansi-blue">:</span>sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bas
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
<p>Some additional useful <code>grep</code> options:</p>

<table class="table ">
<thead><tr>
<th>Examples</th>
<th>Output</th>
</tr></thead>
<tbody>
<tr>
<td><code>grep -v nologin /etc/passwd</code></td>
<td>All lines not containing <code class="console">nologin</code> in the <code class="console">/etc/passwd</code> file</td>
</tr>
<tr>
<td><code>grep -l linux /etc/*</code></td>
<td>List of files in the <code class="console">/etc</code> directory containing <code class="console">linux</code> </td>
</tr>
<tr>
<td><code>grep -i linux /etc/*</code></td>
<td>Listing of lines from files in the <code class="console">/etc</code> directory containing any case (capital or lower) of the character pattern <code class="console">linux</code>
</td>
</tr>
<tr>
<td><code>grep -w linux /etc/*</code></td>
<td>Listing of lines from files in the <code class="console">/etc</code> directory containing  the word pattern <code class="console">linux</code>
</td>
</tr>
</tbody>
</table>

<h2><a name="#29">1.10 Basic Regular Expressions</a></h2>
<p>A <var>Regular Expression</var> is a collection of "normal" and "special" characters that are used to match simple or complex patterns.  Normal characters are alphanumeric characters which match themselves.  For example, an <code class="console">a</code> would match an <code class="console">a</code>.  </p>

<p>Some characters have special meanings when used within patterns by commands like the <code>grep</code> command.  There are both <var>Basic Regular Expressions</var> (available to a wide variety of Linux commands) and <var>Extended Regular Expressions</var> (available to more advanced Linux commands).  Basic Regular Expressions include the following:</p>

<table class="table ">
<thead><tr>
<th>Regular Expression</th>
<th>Matches</th>
</tr></thead>
<tbody>
<tr>
<td><code class="console">.</code></td>
<td>Any single character</td>
</tr>
<tr>
<td><code class="console">[ ]</code></td>
<td>A list or range of characters to match one character, unless the first character is the caret <code class="console">^</code>, and then it means any character not in the list</td>
</tr>
<tr>
<td><code class="console">*</code></td>
<td>Previous character repeated zero or more times</td>
</tr>
<tr>
<td><code class="console">^</code></td>
<td>Following text must appear at beginning of line</td>
</tr>
<tr>
<td><code class="console">$</code></td>
<td>Preceding text must appear at the end of the line</td>
</tr>
</tbody>
</table>

<p>The <code>grep</code> command is just one of many commands that support regular expressions.  Some other commands include the <code>more</code> and <code>less</code> commands.  While some of the regular expressions are unnecessarily quoted with single quotes, it is a good practice to use single quotes around your regular expressions to prevent the shell from trying to interpret special meaning from them. </p>

<h2><a name="#30">1.10.1 Basic Regular Expressions - the . Character</a></h2>
<p>In the example below, a simple file is first created using redirection.  Then the <code>grep</code> command is used to demonstrate a simple pattern match:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo 'abcddd' &gt; example.txt                       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                   
abcddd                                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color 'a..' example.txt                    
<strong><span class="ansi-red">abc</span></strong>ddd                                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>In the previous example, you can see that the pattern <code class="console">a..</code> matched <code class="console">abc</code> .  The first <code class="console">.</code> character matched the <code class="console">b</code> and the second matched the <code class="console">c</code>.</p>

<p>In the next example, the pattern <code class="console">a..c</code> won't match anything, so the <code>grep</code> command will not product any output.  For the match to be successful, there would need to be two characters between the <code class="console">a</code> and the <code class="console">c</code> in <code class="console">example.txt</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color 'a..c' example.txt                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<h2><a name="#31">1.10.2 Basic Regular Expressions - the [ ] Characters</a></h2>
<p>If you use the <code class="console">.</code> character, then any possible character could match.  In some cases you want to specify exactly which characters you want to match.  For example, maybe you just want to match a lower-case alpha character or a number character.  For this, you can use the <code class="console">[  ]</code> Regular Expression characters and specify the valid characters inside the <code class="console">[ ]</code> characters.</p>

<p>For example, the following command matches two characters, the first is either an <code class="console">a</code> or a <code class="console">b</code> while the second is either an <code class="console">a</code>, <code class="console">b</code>, <code class="console">c</code> or <code class="console">d</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color '[ab][a-d]' example.txt              
<strong><span class="ansi-red">ab</span></strong>cddd                                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
<p>Note that you can either list out each possible character <code class="console">[abcd]</code> or provide a range <code class="console">[a-d]</code> as long as the range is in the correct order.  For example, <code class="console">[d-a]</code> wouldn't work because it isn't a valid range:</p>
 
<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color '[d-a]' example.txt                  
grep: Invalid range end                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>The range is specified by a standard called the ASCII table.  This table is a collection of all printable characters in a specific order.  You can see the ASCII table with the <code>man ascii</code> command.  A small example:</p>

<pre class="content_terminal">      041  33  21  !                                 141   97  61  a 
      042  34  22  “                                 142   98  62  b
      043  35  23  #                                 143   99  63  c
      044  36  24  $                                 144   100 64  d
      045  37  25  %                                 145   101 65  e
      046  38  26  &amp;                                 146   102 66  f</pre>

<p>Since <code class="console">a</code> has a smaller numeric value (<code class="console">141</code>) then <code class="console">d</code> (<code class="console">144</code>), the range <code class="console">a-d</code> includes all characters from <code class="console">a</code> to <code class="console">d</code>.</p>
 
<p>What if you want to match a character that can be anything but an <code class="console">x</code>, <code class="console">y</code> or <code class="console">z</code>?   You wouldn't want to have to provide a <code class="console">[ ]</code>  set with all of the characters except <code class="console">x</code>, <code class="console">y</code> or <code class="console">z</code>.   </p>

<p>To indicate that you want to match a character that is not one of the listed characters, start your <code class="console">[ ]</code> set with a <code class="console">^</code> symbol.  For example, the following will demonstrate matching a pattern that includes a character that isn't an <code class="console">a</code>, <code class="console">b</code> or <code class="console">c</code> followed by a <code class="console">d</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color '[^abc]d' example.txt                
abc<strong><span class="ansi-red">dd</span></strong>d                                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<h2><a name="#32">1.10.3 Basic Regular Expressions - the * Character</a></h2>
<p>The <code class="console">*</code> character can be used to match "zero or more of the previous character".  For example, the following will match zero or more <code class="console">d</code> characters:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color 'd*' example.txt                     
abc<strong><span class="ansi-red">ddd</span></strong>                                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<h2><a name="#33">1.10.4 Basic Regular Expressions - the ^ and $ Characters</a></h2>
<p>When you perform a pattern match, the match could occur anywhere on the line.  You may want to specify that the match occurs at the beginning of the line or the end of the line.  To match at the beginning of the line, begin the pattern with a <code class="console">^</code> symbol. </p>

<p>In the following example, another line is added to the <code class="console">example.txt</code> file to demonstrate the use of the <code class="console">^</code> symbol:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo "xyzabc" &gt;&gt; example.txt                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                   
abcddd                                                                  
xyzabc                                                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color "a" example.txt                     
<strong><span class="ansi-red">a</span></strong>bcddd                                                                  
xyz<strong><span class="ansi-red">a</span></strong>bc                                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color "^a" example.txt                     
<strong><span class="ansi-red">a</span></strong>bcddd                                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>     

<p>Note that in the first grep output, both lines match because they both contain the letter <code class="console">a</code>.  In the second grep output, only the line that began with the letter <code class="console">a</code> matched.</p>

<p>In order to specify the match occurs at the end of line, end the pattern with the <code class="console">$</code> character. For example, in order to only find lines which end with the letter <code class="console">c</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep "c$" example.txt                             
xyzab<strong><span class="ansi-red">c</span></strong>                                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>        

<h2><a name="#34">1.10.5 Basic Regular Expressions - the \ Character</a></h2>
<p>In some cases you may want to match a character that happens to be a special Regular Expression character.  For example, consider the following:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo "abcd*" &gt;&gt; example.txt                       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt                                   
abcddd                                                                  
xyzabc                                                                  
abcd*                                                                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color "cd*" example.txt                    
ab<strong><span class="ansi-red">cddd</span></strong>                                                                  
xyzab<strong><span class="ansi-red">c</span></strong>                                                                  
ab<strong><span class="ansi-red">cd</span></strong>*                                                                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<p>In the output of the <code>grep</code> command above, you will see that every line matches because you are looking for a <code class="console">c</code> character followed by zero or more <code class="console">d</code> characters.  If you want to look for an actual <code class="console">*</code> character, place a <code class="console">\</code> character before the <code class="console">*</code> character:
</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep --color "cd\*" example.txt                   
ab<strong><span class="ansi-red">cd*</span></strong>                                                                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<h2><a name="#35">1.11 Extended Regular Expressions</a></h2>
<p>The use of Extended Regular Expressions often requires a special option be provided to the command to recognize them.  Historically, there is a command called <code>egrep</code>, which is similar to <code>grep</code>, but is able to understand their usage.  Now, the <code>egrep</code> command is deprecated in favor of using grep with the <code>-E</code> option. </p>

<p>The following regular expressions are considered "extended":</p>

<table class="table ">
<thead><tr>
<th>RE</th>
<th>Meaning</th>
</tr></thead>
<tbody>
<tr>
<td><code class="console">?</code></td>
<td>Matches previous character zero or one time, so it is an optional character</td>
</tr>
<tr>
<td><code class="console">+</code></td>
<td>Matches previous character repeated one or more times</td>
</tr>
<tr>
<td><code class="console">|</code></td>
<td>Alternation or like a logical or operator</td>
</tr>
</tbody>
</table>

<p>Some extended regular expressions examples:</p>

<table class="table ">
<thead><tr>
<th>Command</th>
<th>Meaning</th>
<th>Matches</th>
</tr></thead>
<tbody>
<tr>
<td><code>grep -E 'colou?r' 2.txt</code></td>
<td>Match <code class="console">colo</code> following by zero or one <code class="console">u</code> character</td>
<td><code class="console">color colour</code></td>
</tr>
<tr>
<td><code>grep -E 'd+' 2.txt</code></td>
<td>Match one or more <code class="console">d</code> characters</td>
<td><code class="console">d dd ddd dddd</code></td>
</tr>
<tr>
<td><code>grep -E 'gray|grey' 2.txt</code></td>
<td>Match either <code class="console">gray</code> or <code class="console">grey</code>
</td>
<td><code class="console">gray grey</code></td>
</tr>
</tbody>
</table>

<h2><a name="#36">1.12 xargs Command</a></h2>
<p>The <code>xargs</code> command is used to build and execute command lines
from standard input.  This command is very helpful when you need to execute a command
with a very long list of arguments, which in some cases can result in an error if the list of arguments is too long.</p>

<p>The <code>xargs</code> command has an option <code>-0</code> which disables
the end-of-file string, allowing the use of arguments containing spaces, quotes, or backslashes.</p>

<p>The <code>xargs</code> command is useful for allowing commands to be executed more efficiently.  Its goal is to build the command line for a command to execute as few times as possible with as many arguments as possible, rather than to execute the command many times with one argument each time.</p>

<p>The <code>xargs</code> command functions by breaking up the list of arguments into sublists and executing the command with each sublist.  The number of arguments in each sublist will not exceed the maximum number of argments for the command being executed and therefore avoids an “<code class="console">Argument list too long</code>” error.</p>

<p>The following example shows a scenario where the <code>xargs</code> command allowed for many files to be removed, where using a normal wildcard (glob) character failed:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/many</span>$</strong> rm *                
bash: /bin/rm: Argument list too long
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/many</span>$</strong> ls | xargs rm
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/many</span>$</strong>
</pre>

*Все материалы взяты с официального курса <i class="fa fa-link"></i> [NDG Linux Essential](https://www.netacad.com/ru/courses/ndg-linux-essentials/)*
