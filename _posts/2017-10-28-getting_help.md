---
bg: "linux.jpg"
layout: post
comments: true
title:  "Getting Help"
crawlertitle: "Getting Help"
summary: "Справка по командам"
date:   2017-10-28 00:00:00 +0300
categories: posts
tags: ['linux']
author: DenIvTea
---
<p>If you ask users what feature of the Linux Operating System they most enjoy, many will answer "the power provided by the command line environment".  This is because there are literally thousands of commands available with many options, making them powerful tools.</p>

<p>However, with this power comes complexity.  Complexity, in turn, can create confusion.  As a result, knowing how to find help while working in Linux is an essential skill for any user.  Referring to help allows you to be reminded of how a command works, as well as being an information resource when learning new commands. </p>

Навигация по статье:

* <a href="#1">5.1 man Pages</a>
* <a href="#2">5.1.1 Viewing man pages</a>
* <a href="#3">5.1.2 Controlling the man Page Display</a>
* <a href="#4">5.1.3 Sections of the man Page</a>
* <a href="#5">5.1.4 man Page SYNOPSIS Section</a>
* <a href="#6">5.1.5 Searching Within a man Page</a>
* <a href="#7">5.1.6 man Pages Categorized by Sections</a>
* <a href="#8">5.1.6.1 Determining Which Section</a>
* <a href="#9">5.1.6.2 Specifying a Section</a>
* <a href="#10">5.1.6.3 Searching Sections</a>
* <a href="#11">5.1.7 Searching man Pages by Keyword</a>

<h2><a name="1">5.1 man Pages</a></h2>
<p>As previously mentioned, UNIX was the operating system from which the Linux foundation was built.  The developers of UNIX created help documents called <var>man pages</var> (man stands for manual).</p>

<p>Man pages are used to describe the features of commands.  They will provide you with a basic description of the purpose of the command, as well as provide details regarding the options of the command.</p>

<h2><a name="2">5.1.1 Viewing man pages</a></h2>
<p>To view a man page for a command, execute <code class="input">man <var>command</var></code> in a terminal window.  For example, the command <code>man cal</code> will display the man page for the <code>cal</code> command:</p>

<pre class="content_terminal">CAL(1)                    BSD General Commands Manual             CAL(1) 

<strong>NAME</strong>                                                                
cal, ncal -- displays a calendar and the date of Easter               

<strong>SYNOPSIS</strong>                                                               
cal [-3hjy] [-A number] [-B number] [[month] year]                     
cal [-3hj] [-A number] [-B number] -m month [year]                     
ncal [-3bhjJpwySM] [-A number] [-B number] [-s country_code] [[month]  
year]                                                              
 ncal [-3bhJeoSM] [-A number] [-B number] [year]                      
 ncal [-CN] [-H yyyy-mm-dd] [-d yyyy-mm]                                    

<strong>DESCRIPTION</strong>                                                            
    The cal utility displays a simple calendar in traditional format and    ncal offers an alternative layout, more options and the date of         Easter. The new format is a little cramped but it makes a year fit      on a 25x80 terminal.  If arguments are not specified, the current       month is displayed.      
                                                                
         The options are as follows:                                               
 -h      Turns off highlighting of today.                                   
                                                 
 Manual page cal(1) line 1 (press h for help or q to quit)</pre>     

<h2><a name="3">5.1.2 Controlling the man Page Display</a></h2>
<p>The <code>man</code> command uses a "pager" to display documents.  Normally this pager is the <code>less</code> command, but on some distributions it may be the <code>more</code> command.  Both are very similar in how they perform and will be discussed in more detail in a later chapter.</p>

<p>If you want to view the various movement commands that are available, you can type the letter <strong>h</strong> while viewing a man page.  This will display a help page: </p>
<div class="alert alert-info">
<strong>Note:</strong> If you are working on a Linux distribution that uses the <code>more</code> command as a pager, your output will be different than the example shown here.</div>

<pre class="content_terminal"> SUMMARY OF LESS COMMANDS                                     
                                               
    Commands marked with * may be preceded by a number, N.     
    Notes in parentheses indicate the behavior if N is given.        
    A key preceded by a caret indicates the Ctrl key; thus ^K is ctrl-K.      
                                                                  
  h  H                 Display this help.                             
  q  :q  Q  :Q  ZZ     Exit.                                          
 -----------------------------------------------------------------------
                                                                    
                         MOVING                                         

e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).             
y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).              
f  ^F  ^V  SPACE  *  Forward  one window (or N lines).             
b  ^B  ESC-v      *  Backward one window (or N lines).
z                 *  Forward  one window (and set window to N).  
w                 *  Backward one window (and set window to N).      
ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
d  ^D             *  Forward  one half-window (and set half-window to N)
u  ^U             *  Backward one half-window (and set half-window to N)
ESC-)  RightArrow *  Left  one half screen width (or N positions).     
HELP -- Press RETURN for more, or q when done</pre>



<p>If your distribution uses the <code>less</code> command, you might be a bit overwhelmed with the large number of "commands" that are available.  The following table provides a summary of the more useful commands:</p>

<table class="table ">
<thead><tr>
<th>Command</th>
<th>Function</th>
</tr></thead>
<tbody>
<tr>
<td>
<strong>Return</strong> (or <strong>Enter</strong>)</td>
<td>Go down one line</td>
</tr>
<tr>
<td><strong>Space</strong></td>
<td>Go down one page</td>
</tr>
<tr>
<td>/<code class="console">term</code>
</td>
<td>Search for <var>term</var>
</td>
</tr>
<tr>
<td><strong>n</strong></td>
<td>Find next search item</td>
</tr>
<tr>
<td>
<strong>1</strong><strong>G</strong>
</td>
<td>Go to beginning</td>
</tr>
<tr>
<td><strong>G</strong></td>
<td>Go to end</td>
</tr>
<tr>
<td><strong>h</strong></td>
<td>Display help</td>
</tr>
<tr>
<td><strong>q</strong></td>
<td>Quit man page</td>
</tr>
</tbody>
</table>

<h2><a name="4">5.1.3 Sections of the man Page</a></h2>
<p>Man pages are broken into sections.  Each section is designed to provide specific information about a command.  While there are common sections that you will see in most man pages, some developers also create sections that you will only see in a specific man page.</p>

<p>The following table describes some of the more common sections that you will find in man pages:</p>

<table class="table ">
<thead><tr>
<th>Section name</th>
<th>Purpose</th>
</tr></thead>
<tbody>
<tr>
<td>NAME</td>
<td>Provides the name of the command and a very brief description.</td>
</tr>
<tr>
<td>SYNOPSIS</td>
<td>Provides examples of how the command is executed. See below for more information.</td>
</tr>
<tr>
<td>DESCRIPTION</td>
<td>Provides a more detailed description of the command.</td>
</tr>
<tr>
<td>OPTIONS</td>
<td>Lists the options for the command as well as a description of how they are used.  Often this information will be found in the <code class="console">DESCRIPTION</code>section and not in a separate <code class="console">OPTIONS</code> section.</td>
</tr>
<tr>
<td>FILES</td>
<td>Lists the files that are associated with the command as well as a description of how they are used.  These files may be used to configure the command's more advanced features.  Often this information will be found in the <code class="console">DESCRIPTION</code> section and not in a separate <code class="console">OPTIONS</code> section.</td>
</tr>
<tr>
<td>AUTHOR</td>
<td>The name of the person who created the man page and (sometimes) how to contact the person.</td>
</tr>
<tr>
<td>REPORTING BUGS</td>
<td>Provides details on how to report problems with the command.  </td>
</tr>
<tr>
<td>COPYRIGHT</td>
<td>Provides basic copyright information.</td>
</tr>
<tr>
<td>SEE ALSO</td>
<td>Provides you with an idea of where you can find additional information.  This also will often include other commands that are related to this command.</td>
</tr>
</tbody>
</table>

<h2><a name="5">5.1.4 man Page SYNOPSIS Section</a></h2>
<p>The <code class="console">SYNOPSIS</code> section of a man page can be difficult to understand, but is very important because it provides a concise example of how to use the command.  For example, consider the <code class="console">SYNOPSIS</code> of the man page for the <code>cal</code> command:</p>



<pre class="content_terminal">SYNOPSIS                                                              
     cal [-3hjy] [-A number] [-B number] [[[day] month] year]</pre>

<p>The square brackets  <code class="console">[ ] </code>are used to indicate that this feature is not required to run the command.  For example, <code class="console">[-3hjy]</code>means you can use the options <code class="console">-h</code>,  <code class="console">-j</code>, <code class="console">-y</code>, <code class="console">1</code> or <code class="console">3</code>, but none of these options are required for the <code>cal</code> command to function properly.</p>

<p>The second set of square brackets in the <code>cal</code> <code class="console">SYNOPSIS</code> (<code class="console">[[[day] month] year]</code>) demonstrates another feature; it means that you can specify a year by itself, but if you specify a month you must also specify a year.  Additionally, if you specify a day then you also need to specify a month and a year.</p>

<p>Another component of the <code class="console">SYNOPSIS</code> that might cause some confusion can be seen in the <code class="console">SYNOPSIS</code> of the <code>date</code> command:</p>

<pre class="content_terminal">SYNOPSIS                                                              
       date [OPTION]... [+FORMAT]                                      
       date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]</pre>                      
                                                            

<p>In this <code class="console">SYNOPSIS</code> there are two syntaxes for the <code>date</code> command.  The first one is used to display the date on the system while the second is used to set the date.</p>

<p>The ellipses following <code class="console">[OPTION]</code>,<code class="console">...</code>, indicate that one or more of the items before it may be used.</p>

<p>Additionally the <code class="console">[-u|--utc|--universal]</code> notation means that you can either use the <code class="console">-u</code> option or the <code class="console">--utc</code> option or the <code class="console">--universal </code>option.  Typically this means that all three options really do the same thing, but sometimes this format (use of the <code class="console">|</code> character) is used to indicate that the options can't be used in combination, like a logical “or".</p>

<h2><a name="6">5.1.5 Searching Within a man Page</a></h2>
<p>In order to search a man page for a term, press the <code class="console">/</code> and type the term followed by the <strong>Enter</strong> key.  The program will search from the current location down towards the bottom of the page to try to locate and highlight the term. </p>

<p>If the term is not found, or you have reached the end of the matches, then the program will report <code class="console">Pattern not found (press Return)</code>.  If a match is found and you want to move to the next match of the term, press <strong>n</strong>.  To return to a previous match of the term, press <strong>N</strong>.</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/5.3.5_1.png"></div>

<h2><a name="7">5.1.6 man Pages Categorized by Sections</a></h2>
<p>Until now, we have been displaying man pages for commands.  However, sometimes configuration files also have man pages.  Configuration files (sometimes called system files) contain information that is used to store information about the Operating System or services.</p>

<p>Additionally, there are several different types of commands (user commands, system commands, and administration commands) as well as other features that require documentation, such as libraries and Kernel components.</p>

<p>As a result, there are thousands of man pages on a typical Linux distribution.  To organize all of these man pages, the pages are categorized by sections, much like each individual man page is broken into sections.</p>

<div class="alert alert-info">
<strong>Consider This:</strong><p>By default there are nine default sections of man pages:</p>
<ol type="disc" class="">
<li>Executable programs or shell commands</li>
<li>System calls (functions provided by the kernel)</li>
<li>Library calls (functions within program libraries)</li>
<li>Special files (usually found in <code class="console">/dev</code>)</li>
<li>File formats and conventions, e.g. <code class="console">/etc/passwd</code>
</li>
<li>Games</li>
<li>Miscellaneous (including  macro  packages and conventions), e.g. <code class="console">man(7)</code>, <code class="console">groff(7)</code>
</li>
<li>System administration commands (usually only for root)</li>
<li>Kernel routines [Non standard]</li>
</ol>
</div>

<p>When you use the <code>man</code> command, it searches each of these sections in order until it finds the first "match".  For example, if you execute the command <code>man cal</code>, the first section (Executable programs or shell commands) is searched for a man page called <code class="console">cal</code>.  If not found, then the second section is searched.  If no <strong>man</strong> page is found after searching all sections, you will receive an error message:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> man zed                                          
No manual entry for zed                                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<h2><a name="8">5.1.6.1 Determining Which Section</a></h2>
<p>To determine which section a specific man page belongs to, look at the numeric value on the first line of the output of the man page.  For example, if you execute the command <code>man cal</code>, you will see that the <code>cal</code> command belongs to the first section of man pages:</p>



<pre class="content_terminal">CAL<span class="attention"><span class="ansi-red">(1)</span></span>                    BSD General Commands Manual             CAL(1)</pre> 

<h2><a name="9">5.1.6.2 Specifying a Section</a></h2>
<p>In some cases you will need to specify the section in order to display the correct man page.  This is necessary because sometimes there will be man pages with the same name in different sections.</p>

<p>For example, there is a command called <code>passwd</code>that allows you to change your password.  There is also a file called <code class="console">passwd</code>that stores account information.  Both the command and the file have a man page.</p>

<p>The passwd command is a "user" command, so the command <code>man passwd</code> will display the man page for the <code>passwd</code> command by default:</p>

<pre class="content_terminal">PASSWD<span class="attention"><span class="ansi-red">(1)</span></span>                        User Commands                 PASSWD(1)</pre>                                            

<p>To specify a different section, provide the number of the section as the first argument of the man command.  For example, the command <code>man 5 passwd</code> will look for the <code>passwd</code> man page just in section <code class="console">5</code>:
</p>
 
<pre class="content_terminal">PASSWD<span class="attention"><span class="ansi-red">(5)</span></span>                File Formats and Conversions          PASSWD(5)</pre>

<h2><a name="10">5.1.6.3 Searching Sections</a></h2>
<p>Sometimes it isn't clear what section a man page is stored in.  In cases like this, you can search for a man page by name.</p>

<p>The <code>-f</code> option to the man command will display man pages that match, or partially match, a specific name and provide a brief description of each man page:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> man -f passwd                                    
passwd (5)           - the password file                              
passwd (1)           - change user password                           
passwd (1ssl)        - compute password hashes                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
                                         

<p>Note that on most Linux distributions, the <code>whatis</code> command does the same thing as <code>man -f.</code>  On those distributions, both will produce the same output.</p>

<h2><a name="11">5.1.7 Searching man Pages by Keyword</a></h2>
<p>Unfortunately, you won't always remember the exact name of the man page that you want to view.  In these cases you can search for man pages that match a keyword by using the <code>-k</code> option to the <code>man</code> command.</p>

For example, what if you knew you wanted a man page that displays how to change your password, but you didn't remember the exact name?  You could run the command <code>man -k password</code>:

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> man -k passwd                                    
chgpasswd (8)        - update group passwords in batch mode            
chpasswd (8)         - update passwords in batch mode                 
fgetpwent_r (3)      - get passwd file entry reentrantly               
getpwent_r (3)       - get passwd file entry reentrantly               
gpasswd (1)          - administer /etc/group and /etc/gshadow         
pam_localuser (8)    - require users to be listed in /etc/passwd      
passwd (1)           - change user password                           
passwd (1ssl)        - compute password hashes                        
passwd (5)           - the password file                               
passwd2des (3)       - RFS password encryption                         
update-passwd (8)    - safely update /etc/passwd, /etc/shadow and /etc/group    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>
                                                          
<div class="alert alert-info">When you use this option, you may end up with a large amount of output.  The preceding command, for example, provided over 60 results.</div>

<p>Recall that there are thousands of man pages, so when you search for a keyword, be as specific as possible.  Using a generic word, such as "the" could result in hundreds or even thousands of results.</p>

<p>Note that on most Linux distributions, the <code>apropos</code> command does the same thing as <code>man -k</code>.  On those distributions, both will produce the same output.</p>

