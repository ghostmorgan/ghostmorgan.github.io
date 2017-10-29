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

* <a href="#1">1.1 man Pages</a>
* <a href="#2">1.1.1 Viewing man pages</a>
* <a href="#3">1.1.2 Controlling the man Page Display</a>
* <a href="#4">1.1.3 Sections of the man Page</a>
* <a href="#5">1.1.4 man Page SYNOPSIS Section</a>
* <a href="#6">1.1.5 Searching Within a man Page</a>
* <a href="#7">1.1.6 man Pages Categorized by Sections</a>
* <a href="#8">1.1.6.1 Determining Which Section</a>
* <a href="#9">1.1.6.2 Specifying a Section</a>
* <a href="#10">1.1.6.3 Searching Sections</a>
* <a href="#11">1.1.7 Searching man Pages by Keyword</a>
* <a href="#12">1.2 info Command</a>
* <a href="#13">1.2.1 Displaying Info Documentation for a Command</a>
* <a href="#14">1.2.2 Moving Around While Viewing an info Document</a>
* <a href="#15">1.2.3 Exploring info Documentation</a>
* <a href="#16">1.3 Additional Sources of Help</a>
* <a href="#17">1.3.1 Using the --help Option</a>
* <a href="#18">1.3.2 Additional System Documentation</a>
* <a href="#19">1.4 Finding Commands and Documentation</a>
* <a href="#20">1.4.1 Where Are These Commands Located?</a>
* <a href="#21">1.4.2 Find Any File or Directory</a>
* <a href="#22">1.4.3 Count the Number of Files</a>
* <a href="#23">1.4.4 Limiting the Output</a>

<h2><a name="1">1.1 man Pages</a></h2>
<p>As previously mentioned, UNIX was the operating system from which the Linux foundation was built.  The developers of UNIX created help documents called <var>man pages</var> (man stands for manual).</p>

<p>Man pages are used to describe the features of commands.  They will provide you with a basic description of the purpose of the command, as well as provide details regarding the options of the command.</p>

<h2><a name="2">1.1.1 Viewing man pages</a></h2>
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

<h2><a name="3">1.1.2 Controlling the man Page Display</a></h2>
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

<h2><a name="4">1.1.3 Sections of the man Page</a></h2>
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

<h2><a name="5">1.1.4 man Page SYNOPSIS Section</a></h2>
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

<h2><a name="6">1.1.5 Searching Within a man Page</a></h2>
<p>In order to search a man page for a term, press the <code class="console">/</code> and type the term followed by the <strong>Enter</strong> key.  The program will search from the current location down towards the bottom of the page to try to locate and highlight the term. </p>

<p>If the term is not found, or you have reached the end of the matches, then the program will report <code class="console">Pattern not found (press Return)</code>.  If a match is found and you want to move to the next match of the term, press <strong>n</strong>.  To return to a previous match of the term, press <strong>N</strong>.</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/5.3.5_1.png"></div>

<h2><a name="7">1.1.6 man Pages Categorized by Sections</a></h2>
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

<h2><a name="8">1.1.6.1 Determining Which Section</a></h2>
<p>To determine which section a specific man page belongs to, look at the numeric value on the first line of the output of the man page.  For example, if you execute the command <code>man cal</code>, you will see that the <code>cal</code> command belongs to the first section of man pages:</p>



<pre class="content_terminal">CAL<span class="attention"><span class="ansi-red">(1)</span></span>                    BSD General Commands Manual             CAL(1)</pre> 

<h2><a name="9">1.1.6.2 Specifying a Section</a></h2>
<p>In some cases you will need to specify the section in order to display the correct man page.  This is necessary because sometimes there will be man pages with the same name in different sections.</p>

<p>For example, there is a command called <code>passwd</code>that allows you to change your password.  There is also a file called <code class="console">passwd</code>that stores account information.  Both the command and the file have a man page.</p>

<p>The passwd command is a "user" command, so the command <code>man passwd</code> will display the man page for the <code>passwd</code> command by default:</p>

<pre class="content_terminal">PASSWD<span class="attention"><span class="ansi-red">(1)</span></span>                        User Commands                 PASSWD(1)</pre>                                            

<p>To specify a different section, provide the number of the section as the first argument of the man command.  For example, the command <code>man 5 passwd</code> will look for the <code>passwd</code> man page just in section <code class="console">1</code>:
</p>
 
<pre class="content_terminal">PASSWD<span class="attention"><span class="ansi-red">(5)</span></span>                File Formats and Conversions          PASSWD(5)</pre>

<h2><a name="10">1.1.6.3 Searching Sections</a></h2>
<p>Sometimes it isn't clear what section a man page is stored in.  In cases like this, you can search for a man page by name.</p>

<p>The <code>-f</code> option to the man command will display man pages that match, or partially match, a specific name and provide a brief description of each man page:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> man -f passwd                                    
passwd (5)           - the password file                              
passwd (1)           - change user password                           
passwd (1ssl)        - compute password hashes                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          
                                         

<p>Note that on most Linux distributions, the <code>whatis</code> command does the same thing as <code>man -f.</code>  On those distributions, both will produce the same output.</p>

<h2><a name="11">1.1.7 Searching man Pages by Keyword</a></h2>
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

<h2><a name="12">1.2 info Command</a></h2>
  <p>Man pages are great sources of information, but they do tend to have a few disadvantages.  One example of a disadvantage is that each man page is a separate document, not related to any other man page.  While some man pages have a <code class="console">SEE ALSO</code> section that may refer to other man pages, they really tend to be unrelated sources of documentation.</p>

  <p>The <code>info</code> command also provides documentation on operating system commands and features.  The goal of this command is slightly different from man pages: to provide a documentation resource that provides a logical organizational structure, making reading documentation easier.</p>

  <p>Within info documents, information is broken down into categories that work much like a table of contents that you would find in a book.  Hyperlinks are provided to pages with information on individual topics for a specific command or feature.  In fact, all of the documentation is merged into a single "book" in which you can go to the top level of documentation and view the table of contents representing all of the documentation available.</p>

  <p>Another advantage of info over man pages is that the writing style of info documents is typically more conducive to learning a topic.  Consider man pages to be more of a reference resource and info documents to be more of a learning guide.</p>
  <h2><a name="13">1.2.1 Displaying Info Documentation for a Command</a></h2>
  <p>To display the info documentation for a command, execute <code class="input">info <var>command</var></code> (replace <code class="console"><var>command</var></code> with the name of the command that you are seeking information about).  For example, the following demonstrates the output of the command <code>info ls</code>:</p>

  <pre class="content_terminal">File: coreutils.info,  Node: ls invocation,  Next: dir invocation,  Up: Directo\ry listing                                                                      
                                                                         
  10.1 `ls': List directory contents                                     
  ==================================                                              
                                                                        
      The `ls' program lists information about files (of any type, including directories).  Options and file arguments can be intermixed arbitrarily, as usual.                                                          
                                                                         
      For non-option command-line arguments that are directories, by    
  default `ls' lists the contents of directories, not recursively, and   
  omitting files with names beginning with `.'.  For other non-option    
  arguments, by default `ls' lists just the file name.  If no non-option 
  argument is specified, `ls' operates on the current directory, acting  
  as if it had been invoked with a single argument of `.'.                        
                                                                         
      By default, the output is sorted alphabetically, according to the  
  locale settings in effect.(1) If standard output is a terminal, the    
  output is in columns (sorted vertically) and control characters are    
  output as question marks; otherwise, the output is listed one per line 
  and control characters are output as-is.                              
  --zz-Info: (coreutils.info.gz)ls invocation, 58 lines --Top-------------
  Welcome to Info version 5.2. Type h for help, m for menu item.</pre>

  <p>Notice that the first line provides some information that tells you where you are in the info documentation.  This documentation is broken up into <code class="console">nodes</code> and in the example above you are currently in the <code class="console">ls invocation</code> node.  If you went to the next node (like going to the next chapter in a book), you would be in the <code class="console">dir invocation</code> node.  If you went up one level you would be in the <code class="console">Directory listing</code> node.</p>
  <h2><a name="14">1.2.2 Moving Around While Viewing an info Document</a></h2>
  <p>Like the <code>man</code> command, you can get a listing of movement commands by typing the letter <strong>h</strong> while reading the info documentation:</p>

  <pre class="content_terminal">Basic Info command keys                                                        
  l           Close this help window.                                   
  q           Quit Info altogether.                                     
  H           Invoke the Info tutorial.                                           
  Up          Move up one line.                                          
  Down        Move down one line.                                        
  DEL         Scroll backward one screenful.                             
  SPC         Scroll forward one screenful.                              
  Home        Go to the beginning of this node.                          
  End         Go to the end of this node.                                         
  TAB         Skip to the next hypertext link.                           
  RET         Follow the hypertext link under the cursor.               
  l           Go back to the last node seen in this window.                       
  [           Go to the previous node in the document.                   
  ]           Go to the next node in the document.                       
  p           Go to the previous node on this level.                    
  n           Go to the next node on this level.                         
  u           Go up one level.                                           
  -----Info: *Info Help*, 466 lines --Top---------------------------------</pre>
                                                         

  <p>Note that if you want to close the help screen, you type the letter <strong>l</strong>.  This brings you back to your document and allows you to continue reading.  To quit entirely, you type the letter <strong>q</strong>.</p>

  <p>The following table provides a summary of useful commands:</p>

  <table class="table ">
  <thead><tr>
  <th>Command</th>
  <th>Function</th>
  </tr></thead>
  <tbody>
  <tr>
  <td>
  <strong>Down arrow</strong> ↓ </td>
  <td>Go down one line</td>
  </tr>
  <tr>
  <td><strong>Space</strong></td>
  <td>Go down one page</td>
  </tr>
  <tr>
  <td><strong>s</strong></td>
  <td>Search for term</td>
  </tr>
  <tr>
  <td><strong>[</strong></td>
  <td>Go to previous node</td>
  </tr>
  <tr>
  <td><strong>]</strong></td>
  <td>Go to next node</td>
  </tr>
  <tr>
  <td><strong>u</strong></td>
  <td>Go up one level</td>
  </tr>
  <tr>
  <td><strong>TAB</strong></td>
  <td>Skip to next hyperlink</td>
  </tr>
  <tr>
  <td><strong>HOME</strong></td>
  <td>Go to beginning</td>
  </tr>
  <tr>
  <td><strong>END</strong></td>
  <td>Go to end</td>
  </tr>
  <tr>
  <td><strong>h</strong></td>
  <td>Display help</td>
  </tr>
  <tr>
  <td><strong>L</strong></td>
  <td>Quit help page</td>
  </tr>
  <tr>
  <td><strong>q</strong></td>
  <td>Quit info command</td>
  </tr>
  </tbody>
  </table>

  <p>If you scroll through the document, you will eventually see the menu for the <code>ls</code> command:</p>

  <pre class="content_terminal">* Menu:                                                                         
                             
  * Which files are listed::                     
  * What information is listed::                 
  * Sorting the output::                          
  * Details about version sort::                   
  * General output formatting::                    
  * Formatting file timestamps::                    
  * Formatting the file names::                                                   
                                           
     ---------- Footnotes ----------                                              
            
   (1) If you use a non-POSIX locale (e.g., by setting `LC_ALL' to 
  `en_US'), then `ls' may produce output that is sorted differently than
  you're accustomed to.  In that case, set the `LC_ALL' environment     
  variable to `C'.                                                                
  --zz-Info: (coreutils.info.gz)ls invocation, 58 lines --Top-------------</pre>
                                                                                  

  <p>The items under the menu are hyperlinks that can take you to nodes that describe more about the <code>ls</code> command.  For example, if you placed your cursor on the line "<code class="console">* Sorting the output::</code>" and pressed the <strong>Enter</strong> key, you would be taken to a node that describes sorting the output of the <code>ls</code> command:</p>
  <pre class="content_terminal">File: coreutils.info,  Node: Sorting the output,  Next: Details about version s\ort,  Prev: What information is listed,  Up: ls invocation                      
  10.1.3 Sorting the output                                             
  -------------------------                                                      
  These options change the order in which `ls' sorts the information it  
  outputs.  By default, sorting is done by character code (e.g., ASCII   
  order).                                                                         
                                                                        
  `-c'                                                                  
  `--time=ctime'                                                        
  `--time=status'                                                        
       If the long listing format (e.g., `-l', `-o') is being used, print 
       the status change time (the `ctime' in the inode) instead of the  
       modification time.  When explicitly sorting by time (`--sort=time'
       or `-t') or when not using a long listing format, sort according  
       to the status change time.                                                 
                                                                      
  `-f'                                                                  
       Primarily, like `-U'--do not sort; list the files in whatever     
       order they are stored in the directory.  But also enable `-a' (lis
  --zz-Info: (coreutils.info.gz)Sorting the output, 68 lines --Top--------</pre>
                                                                   

  <p>Note that by going into the node about sorting, you essentially went into a sub-node of the one in which you originally started.  To go back to your previous node, you can use the <strong>u</strong> key.  While <strong>u</strong> will take you to the start of the node one level up, you could also use the <strong>l</strong> key to return you exactly to the previous location that you were before entering the sorting node.</p>
  <h2><a name="15">1.2.3 Exploring info Documentation</a></h2>
  <p>Instead of using info documentation to look up information about a specific command or feature, consider exploring the capabilities of Linux by reading through the info documentation.  If you execute the <code>info</code> command without any arguments, you are taken to the top level of the documentation.  From there you can explore many features:</p>

  <pre class="content_terminal">File: dir,      Node: Top       This is the top of the INFO tree                
    This (the Directory node) gives a menu of major topics.              
    Typing "q" exits, "?" lists all Info commands, "d" returns here,    
    "h" gives a primer for first-timers,                                
    "mEmacslt&lt;Return&gt;" visits the Emacs manual, etc.                               
    In Emacs, you can click mouse button 2 on a menu item or cross referen  ce to select it.                                                                 
  * Menu:                                                                        

  Basics                                                                 
  * Common options: (coreutils)Common options.                           
  * Coreutils: (coreutils).       Core GNU (file, text, shell) utilities.
  * Date input formats: (coreutils)Date input formats.                   
  * File permissions: (coreutils)File permissions.                      
                             Access modes.                          
  * Finding files: (find).   Operating on files matching certain criteria.   
                                                                         
  C++ libraries                                                        
  * autosprintf: (autosprintf).  Support for printf format strings in C+
  -----Info: (dir)Top, 211 lines --Top------------------------------------
  Welcome to Info version 5.2. Type h for help, m for menu item.</pre>                  

  <h2><a name="16">1.3 Additional Sources of Help</a></h2>
  <p>In many cases, you will find that either man pages or info documentation will provide you with the answers you need.  However, in some cases, you may need to look in other locations. </p>

  <h2><a name="17">1.3.1 Using the --help Option</a></h2>
  <p>Many commands will provide you basic information, very similar to the <code class="console">SYNOPSIS</code> found in man pages, when you apply the <code>--help</code> option to the command.  This is useful to learn the basic usage of a command:</p>

  <pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>  ps --help                                              
  ********* simple selection *********  ********* selection by list *********   
  -A all processes                      -C by command name                      
  -N negate selection                   -G by real group ID (supports names)    
  -a all w/ tty except session leaders  -U by real user ID (supports names)     
  -d all except session leaders         -g by session OR by effective group name
  -e all processes                      -p by process ID                        
  T  all processes on this terminal     -s processes in the sessions given     
  a  all w/ tty, including other users  -t by tty                               
  g  OBSOLETE -- DO NOT USE             -u by effective user ID (supports names)
  r  only running processes             U  processes for specified users        
  x  processes w/o controlling ttys     t  by tty                               
  *********** output format **********  *********** long options ***********    
  -o,o user-defined  -f full            --Group --User --pid --cols --ppid      
  -j,j job control   s  signal          --group --user --sid --rows --info      
  -O,O preloaded -o  v  virtual memory  --cumulative --format --deselect        
  -l,l long          u  user-oriented   --sort --tty --forest --version         
  -F   extra full    X  registers       --heading --no-headi
                      ********* misc options *********                          
  -V,V  show version      L  list format codes  f  ASCII art forest             
  -m,m,-L,-T,H  threads   S  children in sum    -y change -l format             
  -M,Z  security data     c  true command name  -c scheduling class             
  -w,w  wide output       n  numeric WCHAN,UID  -H process hierarchy            
  <strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> </pre>

  <h2><a name="18">1.3.2 Additional System Documentation</a></h2>
  <p>On most systems, there is a directory where additional documentation is found.  This will often be a place where vendors who create additional (third party) software can store documentation files.</p>

  <p>Typically, this will be a place where system administrators will go to learn how to set up more complex software services.  However, sometimes regular users will also find this documentation to be useful.
  </p>

  <p>These documentation files are often called "readme" files, since the files typically have names such as <code class="console">README</code> or <code class="console">readme.txt</code>.  The location of these files can vary depending on the distribution that you are using.  Typical locations include <code class="console">/usr/share/doc</code> and <code class="console">/usr/doc</code>.</p>

  <h2><a name="19">1.4 Finding Commands and Documentation</a></h2>
  <p>Recall that the <code>whatis</code> command (or <code>man -f</code>) will tell you which section a man page is stored in.  If you use this command often enough, you will likely come across an unusual output, such as the following:</p>

  <pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> whatis ls                                              
  ls (1)               - list directory contents 
  ls (lp)              - list directory contents                                 
  <strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> </pre>  

  <p>Based on this output, there are two commands that list directory contents.  The simple answer to why there are two <code>ls</code> commands is that UNIX had two main variants, which resulted in some commands being developed "in parallel".  This resulted in some commands behaving differently on different variants of UNIX.  Many modern distributions of Linux include commands from both UNIX variants.</p>

  <p>This does, however, pose a bit of a problem: when you run the <code>ls</code> command, which command is executed?  The focus of the next few sections will be to answer this question as well as to provide you with the tools to find where these files reside on the system.</p>

  <h2><a name="20">1.4.1 Where Are These Commands Located?</a></h2>
  <p>To search for the location of a command or the man pages for a command, use the <code>whereis</code> command.  This command searches for commands, source files and man pages in specific locations where these files are typically stored:</p>

  <pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> whereis ls                                              
  ls: /bin/ls /usr/share/man/man1p/ls.1.gz /usr/share/man/man1/ls.1.gz                                       
  <strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>  

  <p>Man pages are normally easily distinguished between commands as they are normally compressed with a command called <code>gzip</code>, resulting in a filename that ends in <code class="console">.gz</code>. </p>

  <p>The interesting note is that you see there are two man pages listed, but only one command (<code class="console">/bin/ls</code>).  This is because the <code>ls</code> command can be used with the options/features that are described by <var>either</var> man page.  So, when you are learning what you can do with the <code>ls</code> command, you can explore both man pages.  Fortunately, this is more of an exception as most commands only have one man page.</p>
  <h2><a name="21">1.4.2 Find Any File or Directory</a></h2>
  <p>The <code>whereis</code> command is designed to specifically find commands and man pages.  While this is useful, there are times where you want to find a file or directory, not just files that are commands or man pages.</p>

  <p>To find any file or directory, you can use the <code>locate</code> command.  This command will search a database of all files and directories that were on the system when the database was created.  Typically, the command to generate this database is run nightly.</p>

  <pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> locate gshadow                                   
  /etc/gshadow                                                           
  /etc/gshadow-                                                          
  /usr/include/gshadow.h                                                
  /usr/share/man/cs/man5/gshadow.5.gz                                   
  /usr/share/man/da/man5/gshadow.5.gz                                    
  /usr/share/man/de/man5/gshadow.5.gz                                    
  /usr/share/man/fr/man5/gshadow.5.gz                                    
  /usr/share/man/it/man5/gshadow.5.gz                                    
  /usr/share/man/man5/gshadow.5.gz                                       
  /usr/share/man/ru/man5/gshadow.5.gz                                   
  /usr/share/man/sv/man5/gshadow.5.gz                                    
  /usr/share/man/zh_CN/man5/gshadow.5.gz                                 
  <strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
                                                                                  
                                                

  <p>Any files that you created today will not normally be searchable with the <code>locate</code> command.  If you have access to the system as the <code class="console">root</code> user (the system administrator account), you can manually update the <code>locate</code> database by running the <code>updatedb</code> command.  Regular users cannot update the database file.</p>

  <p>Also note that when you use the <code>locate</code> command as a regular user, your output may be limited due to file permissions.  Essentially, if you don't have access to a file or directory on the filesystem due to permissions, the <code>locate</code> command won't return those names.  This is a security feature designed to keep users from "exploring" the filesystem by using the <code>locate</code> database.  The <code class="console">root</code> user can search for any file in the <code>locate</code> database.</p>
  <h2><a name="22">1.4.3 Count the Number of Files</a></h2>
  <p>The output of the <code>locate</code> command can be quite large.  When you search for a filename, such as <code class="console">passwd</code>, the <code>locate</code> command will produce every file that contains the string <code class="console">passwd</code>, not just files named <code class="console">passwd</code>.</p>
    
  <p>In many cases, you may want to start by listing how many files will match.  You can do this by using the <code>-c</code> option to the <code>locate</code> command:</p>

  <pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> locate -c passwd                                 
  97                                                                     
  <strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>   


  <h2><a name="23">1.4.4 Limiting the Output</a></h2>
  <p>You can limit the output produced by the <code>locate</code> command by using the <code>-b</code> option.  This option will only include listings that have the search term in the <var>basename</var> of the filename.  The basename is the portion of the filename not including the directory names.</p>

  <pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> locate -c -b passwd                              
  83                                                                     
  <strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
  <p>As you can see from the previous output, there will still be many results when you use the <code>-b</code> option.  To limit the output even further, you place a <code class="console">\</code>character in front of the search term.  This character limits the output to filenames that exactly match the term:
  </p>

  <pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> locate -b "\passwd"                              
  /etc/passwd                                                           
  /etc/cron.daily/passwd                                                 
  /etc/pam.d/passwd                                                      
  /usr/bin/passwd                                                        
  /usr/share/doc/passwd                                                 
  /usr/share/lintian/overrides/passwd                                    
  <strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                        
*Все материалы взяты с официального курса <i class="fa fa-link"></i> [NDG Linux Essential](https://www.netacad.com/ru/courses/ndg-linux-essentials/)*
