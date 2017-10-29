---
bg: "linux.jpg"
layout: post
comments: true
title:  "Working with Files and Directories"
crawlertitle: "Working with Files and Directories"
summary: "Работа с файлами и каталогами"
date:   2017-10-28 22:00:00 +0300
categories: posts
tags: ['linux']
author: DenIvTea
---

<p>When working in a Linux Operating System, you will need to know how to manipulate files and directories.  Some Linux distributions have GUI-based applications that allow you to manage files, but it is important to know how to perform these operations via the command line.</p>

<p>The command line features a rich collection of commands that allow you to manage files.  In this chapter you will learn how to list files in a directory as well as how to copy, move and delete files.  </p>

<p>The core concepts taught in this chapter will be expanded in later chapters as more file manipulation commands are covered, such as how to view files, compress files and set file permissions.</p>

Навигация по статье:

* <a href="#1">1.1 Understanding Files and Directories</a>
* <a href="#2">1.1.1 Directory Path</a>
* <a href="#3">1.1.2 Home Directory</a>
* <a href="#4">1.1.3 Current Directory</a>
* <a href="#5">1.1.4 Changing Directories</a>
* <a href="#6">1.1.5 Absolute vs. Relative Pathnames</a>
* <a href="#7">1.2 Listing Files in a Directory</a>
* <a href="#8">1.2.1 Listing Colors</a>
* <a href="#9">1.2.2 Listing Hidden Files</a>
* <a href="#10">1.2.3 Long Display Listing</a>
* <a href="#11">1.2.3.1 Human Readable Sizes</a>
* <a href="#12">1.2.4 Listing Directories</a>
* <a href="#13">1.2.5 Recursive Listing</a>
* <a href="#14">1.2.6 Sort a Listing</a>
* <a href="#15">1.2.7 Listing With Globs</a>
* <a href="#16">1.3 Copying Files</a>
* <a href="#17">1.3.1 Verbose Mode</a>
* <a href="#18">1.3.2 Avoid Overwriting Data</a>
* <a href="#19">1.3.3 Copying Directories</a>
* <a href="#20">1.4 Moving Files</a>
* <a href="#21">1.5 Moving Files While Renaming</a>
* <a href="#22">1.5.1 Renaming Files</a>
* <a href="#23">1.5.2 Additional mv Options</a>
* <a href="#24">1.6 Creating Files</a>
* <a href="#25">1.7 Removing Files</a>
* <a href="#26">1.8 Removing Directories</a>
* <a href="#27">1.9 Making Directories</a>

<h2><a name="1">1.1 Understanding Files and Directories</a></h2>
<p>Files are used to store data such as text, graphics and programs.  Directories (AKA, "folders") are used to provide a hierarchical organization structure.  This structure is somewhat different than what you might be used to if you have previously worked on Microsoft Windows systems.</p>

<p>On a Windows system, the <var>top level</var> of the directory structure is called <var>My Computer</var>.  Each physical device (hard drive, DVD drive, USB thumb drive, network drive, etc.) shows up under My Computer, each assigned a drive letter, such as <var>C:</var> or <var>D:</var>.  A visual representation of this structure:</p>

<div class="alert alert-info">The directory structures shown below are provided as examples only. These directories may not be present within the virtual machine environment of this course.</div>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.3_1.png"></div>

<p>Like Windows, a Linux directory structure has a top level, however it is not called My Computer, but rather the <var>root directory</var> and it is symbolized by the <code class="console">/</code> character.  There are also no drives in Linux; each physical device is accessible under a directory, not a drive letter.  A visual representation of a typical Linux directory structure:</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.3_2.png"></div>

<div class="alert alert-info">This directory structure is called the <var>filesystem</var> by most Linux users.</div>

<p>To view the root filesystem, type <code>ls /</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /                                            
<strong><span class="ansi-blue">bin   dev  home  lib    media  opt   root  sbin     selinux  sys  usr</span>  
<span class="ansi-blue">boot  etc</span>  <span class="ansi-green">init</span>  <span class="ansi-blue">lib64  mnt    proc  run</span>   <span class="ansi-cyan">sbin???</span>  <span class="ansi-blue">srv</span>   <span class="ansi-green">tmp</span>  <span class="ansi-blue">var</span></strong></pre>   

<p>Notice that there are many descriptive directories including <code class="console">/boot</code>, which contains files to boot the computer.</p>

<h2><a name="2">1.1.1 Directory Path</a></h2>
<p>Using the graphic in the previous section as a point of reference, you will see that there is a directory named <code class="console">sound</code> under a directory named <code class="console">etc</code>, which is under the <code class="console">/</code> directory.  An easier way to say this, is to refer to  the <var>path</var>.</p>

<div class="alert alert-info">
<strong>Consider This:</strong><p>The <code class="console">/etc</code> directory originally stood for “et cetera” in early documentation from Bell Labs and used to contain files that did not belong elsewhere.  In modern Linux distributions, the <code class="console">/etc</code> directory typically holds static configuration files as defined by the File Hierarchy Standard (FHS).</p>
</div>

<p>A path allows you to specify the exact location of a directory.  For the <code class="console">sound</code> directory, the path would be <code class="console">/etc/sound</code>.  The first <code class="console">/</code> character represents the <code class="console">root</code> directory, while each other <code class="console">/</code> character is used to separate the directory names.</p>

<p>This sort of path is called an <var>absolute path</var>.  With an absolute path, you always provide directions to a directory (or a file) starting from the top of the directory structure, the <code class="console">root</code> directory.  Later in this chapter, we will cover a different sort of path called a <var>relative path</var>.</p>

<div class="alert alert-info">
<strong>Note:</strong> The directory structures shown below are provided as examples only. These directories may not be present within the virtual machine environment of this course.</div>

<p>The following graphic demonstrates three additional absolute paths:</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.3.1_1.png"></div>

<h2><a name="3">1.1.2 Home Directory</a></h2>
<p>The term <var>home directory</var> often causes confusion to beginning Linux users.  To begin with, on most Linux distributions there is a directory called <code class="console">home</code> under the <code class="console">root</code> directory: <code class="console">/home</code>.</p>

<p>Under this <code class="console">/home</code> directory there will be a directory for each user on the system.  The directory name will be the same as the name of the user, so a user named "bob" would have a <var>home directory</var> called <code class="console">/home/bob</code>.</p>

<p>Your home directory is a very important directory.  To begin with, when you open a shell, you should automatically be placed in your home directory, as this is where you will do most of your work.</p>

<p>Additionally, your home directory is one of the few directories where you have the full control to create and delete additional files and directories.  Most other directories in a Linux filesystem are protected with <var>file permissions</var>, a topic that will be covered in detail in a later chapter.</p>

<p>On most Linux distributions, the only users who can access any files in your home directory are you and the administrator on the system (the <code class="console">root</code> user).  This can be changed by using file permissions.</p>

<p>Your home directory even has a special symbol that you can use to represent it: <code class="console">~</code>.  If your home directory is <code class="console">/home/sysadmin</code>, you can just type <code class="console">~</code> on the command line in place of <code class="console">/home/sysadmin</code>.  You can also refer to another user's home directory by using the notation <code class="console">~<var>user</var></code>, where <var><code class="console">user</code></var> is the name of the user account whose home directory you want to refer to.  For example, <code class="console">~bob</code> would be the same as <code class="console">/home/bob</code>. Here, we will change to the user's home directory:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd ~                                             
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop  Documents  Downloads  Music  Pictures  Public  Templates  
Videos</span></strong>      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>         

Note that a listing reveals subdirectories contained in the home directory.  Changing directories requires attention to detail:

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd downloads                                     
-bash: cd: downloads: No such file or directory                        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

Why did the command above result in an error? That is because Linux environments are case sensitive.  Changing into the <code class="console">Downloads</code> directory requires the correct spelling - including the capital <code class="console">D</code>:

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd Downloads                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/Downloads</span>$</strong></pre>   


<h2><a name="4">1.1.3 Current Directory</a></h2>
<p>Your <var>current directory</var> is the directory where you are currently working in a terminal.  When you first open a terminal, the current directory should be your home directory, but this can change as you explore the filesystem and change to other directories.</p>

<p>While you are in a command line environment, you can determine your current directory by using the <code>pwd</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> pwd                                             
/home/sysadmin                                                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>

<p>Additionally, most systems have the default user prompt display the current directory:</p>

<pre class="config">[sysadmin@localhost ~]$</pre>

<p>In the graphic above, the <code class="console">~</code> character indicates your current directory.  As mentioned previously, the <code class="console">~</code> character represents your home directory.</p>

<p>Normally the prompt only displays the name of the current directory, not the full path from the root directory down.  In other words, if you were in the <code class="console">/usr/share/doc</code> directory, your prompt will likely just provide you with the name <code class="console">doc</code> for the current directory.  If you want the full path, use the <code>pwd</code> command.</p>

<h2><a name="5">1.1.4 Changing Directories</a></h2>
<p>If you want to change to a different directory, use the <code>cd</code> (change directory) command.  For example, the following command will change the current directory to a directory called <code class="console">/etc/sound/events</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd /etc/sound/events                                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/sound/events</span>$</strong></pre>                                           

<p>Note that there is no output if the <code>cd</code> command is successful.  This is one of those "no news is good news" type of things.  If you try to change to a directory that does not exist, you will receive an error message:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/sound/events</span>$</strong> cd /etc/junk                           
-bash: cd: /etc/junk: No such file or directory                               
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/sound/events</span>$</strong></pre>                                           


<p>If you want to return to your home directory, you can either type the <code>cd</code> command with no arguments or use the <code>cd</code> command with the <code class="console">~</code> character as an argument:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/sound/events</span>$</strong> cd                                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> pwd                                                     
/home/sysadmin                                                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd /etc                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc</span>$</strong> cd ~                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> pwd                                                     
/home/sysadmin                                                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>  

<h2><a name="6">1.1.5 Absolute vs. Relative Pathnames</a></h2>
<p>Recall that a pathname is essentially a description of where a file or directory is located in the filesystem.  You can also consider a pathname to be directions that tell the system where to find a file or directory.  For example, the <code>cd /etc/perl/Net</code> command means "change to the <code class="console">Net</code> directory, that you will find under the <code class="console">perl</code> directory, that you will find under the <code class="console">etc</code> directory, that you will find under the <code class="console">/</code> directory".</p>

<p>When you give a pathname that starts from the root directory, it is called an <var>absolute path</var>.  In many cases, providing an absolute path makes sense.  For example, if you are in your <code class="console">home</code> directory and you want to go to the <code class="console">/etc/perl/Net</code> directory, then providing an absolute path to the <code>cd</code> command makes sense:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd /etc/perl/Net                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl/Net</span>$</strong> </pre>

<p>However, what if you were in the <code class="console">/etc/perl</code> directory and you wanted to go to the <code class="console">/etc/perl/Net</code> directory?  It would be tedious to type the complete path to get to a directory that is only one level below your current location.  In a situation like this, you want to use a <var>relative path</var>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl</span>$</strong> cd Net                                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl/Net</span>$</strong> </pre>                                             


<p>A relative path provides directions using your <strong>current location</strong> as a point of reference.  Recall that this is different from absolute paths, which always require you to use the <strong>root directory</strong> as a point of reference.</p>
 
<p>There is a handy relative path technique that you can use to move up one level in the directory structure: the <code class="console">..</code>  directory.  Regardless of which directory you are in, <code class="console">..</code>  always represents one directory higher than your current directory (with the exception of when you are in the <code class="console">/</code> directory):</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl/Net</span>$</strong> pwd                                 
/etc/perl/Net                                                          
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl/Net</span>$</strong> cd ..                                
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl</span>$</strong> pwd                                      
/etc/perl                                                              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl</span>$</strong></pre>                                                  

<p>Sometimes using relative pathnames are a better choice than absolute pathnames, however this is not always the case.  Consider if you were in the <code class="console">/etc/perl/Net</code> directory and then you wanted to go to the <code class="console">/usr/share/doc</code> directory.  Using an absolute pathname, you would execute the <code>cd /usr/share/doc</code> command.  Using relative pathnames, you would execute the <code>cd ../../../usr/share/doc</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl/Net</span>$</strong> cd                                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd /etc/perl/Net                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/etc/perl/Net</span>$</strong> cd /../../../usr/share/doc           
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/usr/share/doc</span>$</strong> pwd                                 
/usr/share/doc                                                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">/usr/share/doc</span>$</strong></pre>  

<div class="alert alert-info">
<strong>Note:</strong> Relative and absolute paths are not just for the <code>cd</code> command.  Any time you specify a file or a directory you can use either relative or absolute paths.</div>

<p>While the double dot (<code class="console">..</code>) is used to refer to the directory above the current directory, the single dot (<code class="console">.</code>) is used to refer to the current directory.  It would be pointless for an administrator to move to the current directory by typing <code>cd .</code> (although it actually works).  It is more useful to refer to an item in the current directory by using the <code>./</code> notation.  For instance:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> pwd                                              
/home/sysadmin                                                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd ./Downloads/                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/Downloads</span>$</strong> pwd                                    
/home/sysadmin/Downloads                                               
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/Downloads</span>$</strong> cd ..                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> pwd                                              
/home/sysadmin                                                         
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<div class="alert alert-info">Note: This use of the single dot (<code class="console">.</code>) as a reference point is not to be confused with using it at the beginning of a filename.  Read more about hidden files in Section 6.4.2.</div>

<h2><a name="7">1.2 Listing Files in a Directory</a></h2>
<p>Now that you are able to move from one directory to another, you will want to start displaying the contents of these directories.  The <code>ls</code> command (<code>ls</code> is short for list) can be used to display the contents of a directory as well as detailed information about the files that are within a directory.</p>

<p>By itself, the <code>ls</code> command will list the files in the current directory:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop  Documents  Downloads  Music  Pictures  Public  Templates  
Videos</span></strong>      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>          

<h2><a name="8">1.2.1 Listing Colors</a></h2>
<p>There are many different types of files in Linux.  As you learn more about Linux, you will discover many of these types.  The following is a brief summary of some of the more common file types:</p>

<table class="table ">
<thead><tr>
<th>Type</th>
<th>Description</th>
</tr></thead>
<tbody>
<tr>
<td>plain file</td>
<td>A file that isn't a special file type; also called a normal file</td>
</tr>
<tr>
<td>directory</td>
<td>A directory file (contains other files)</td>
</tr>
<tr>
<td>executable</td>
<td>A file that can be run like a program</td>
</tr>
<tr>
<td>symbolic link</td>
<td>A file that points to another file</td>
</tr>
</tbody>
</table>

<p>On many Linux distributions, regular user accounts are modified so that the <code>ls</code> command displays filenames, color-coded by file type.  For example, directories may be displayed in blue, executable files may be displayed in green, and symbolic links may be displayed in cyan (light blue).</p>

<p>This is not a normal behavior for the <code>ls</code> command, but rather something that happens when you use the <code>--color</code> option to the <code>ls</code> command.  The reason why <code>ls</code> seems to automatically perform this coloring, is that there is an <var>alias</var> for the <code>ls</code> command so it runs with the <code>--color</code> option:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> alias                                           
alias egrep='egrep --color=auto'                                       
alias fgrep='fgrep --color=auto'                                      
alias grep='grep --color=auto'                                         
alias l='ls -CF'                                                    
alias la='ls -A'                                                       
alias ll='ls -alF'                                                    
alias ls='ls --color=auto'                                             
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
  </pre>
<p>As you can see from the output above, when the <code>ls</code> command is executed, it really runs the command <code>ls --color=auto</code>.</p>

<p>In some cases, you might not want to see all of the colors (they can be a bit distracting sometimes).  To avoid using the alias, place a backslash character  <code class="console">\</code> in front of your command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop  Documents  Downloads  Music  Pictures  Public  Templates  
Videos</span></strong>       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> \ls                                             
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  
Videos       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>  

<h2><a name="9">1.2.2 Listing Hidden Files</a></h2>
<p>When you use the <code>ls</code> command to display the contents of a directory, not all files are shown automatically.  The <code>ls</code> command doesn't display <var>hidden files</var> by default.  A hidden file is any file (or directory) that begins with a dot <code class="console">.</code> character.</p>

<p>To display all files, including hidden files, use the <code>-a</code> option to the <code>ls</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -a                                            
<strong><span class="ansi-blue">.</span></strong>             .bashrc   .selected_editor  <strong><span class="ansi-blue">Downloads  Public</span></strong>           
<strong><span class="ansi-blue">..</span></strong>            <strong><span class="ansi-blue">.cache</span></strong>    <strong><span class="ansi-blue">Desktop           Music      Templates</span></strong>         
.bash_logout  .profile  <strong><span class="ansi-blue">Documents         Pictures   Videos</span></strong></pre>

<p>Why are files hidden in the first place?  Most of the hidden files are <var>customization files</var>, designed to customize how Linux, your shell or programs work.  For example, the <code class="console">.bashrc</code> file in your home directory customizes features of the shell, such as creating or modifying variables and aliases.</p>

<p>These customization files are not ones that you work with on a regular basis.  There are also many of them, as you can see, and having them displayed will make it more difficult to find the files that you do regularly work with.  So, the fact that they are hidden is to your benefit.</p>

<h2><a name="10">1.2.3 Long Display Listing</a></h2>
<p>There is information about each file, called <var>metadata</var> that is sometimes helpful to display.  This may include who owns a file, the size of a file and the last time the contents of a file were modified.  You can display this information by using the <code>-l</code> option to the <code>ls</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l                                           
total 0                                                                
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Desktop</span></strong>                  
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Documents</span></strong>                
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Downloads</span></strong>                
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Music</span></strong>                   
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Pictures</span></strong>                 
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Public</span></strong>                   
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Templates</span></strong>                
drwxr-xr-x 1 sysadmin sysadmin 0 Jan 29  2015 <strong><span class="ansi-blue">Videos</span></strong>                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>In the output above, each line describes metadata about a single file.  The following describes each of the fields of data that you will see in the output of the <code>ls -l</code> command:</p>

<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.4.3_2.png"></div>
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.4.3_3.png"></div>
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.4.3_4.png"></div>
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.4.3_5.png"></div>
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.4.3_6.png"></div>
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.4.3_7.png"></div>
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/linux-essentials/linux_643_redo.png"></div>
<div class="content-image "><img alt="" class="img-responsive" src="https://ndg-content-dev.s3.amazonaws.com/media/images/6.4.3_9.png"></div>

<h2><a name="11">1.2.3.1 Human Readable Sizes</a></h2>
<p>When you display file sizes with the <code>-l</code> option to the <code>ls</code> command, you end up with file sizes in bytes.  For text files, a byte is 1 character.  </p>

<p>For smaller files, byte sizes are fine.  However, for larger files it is hard to comprehend how large the file is.  For example, consider the output of the following command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l /usr/bin/omshell                                 
-rwxr-xr-c 1 root root 1561400 Oct 9 2012 <strong><span class="ansi-green">/usr/bin/omshell</span></strong>              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>As you can see, the file size is hard to determine in bytes.  Is 1561400 a large file or small?  It seems fairly large, but it is hard to determine using bytes.  </p>

<p>Think of it this way: if someone were to give you the distance between Boston and New York using inches, that value would essentially be meaningless because for a distance like that, you think in terms of miles.</p>

<p>It would be better if the file size was presented in a more human readable size, like megabytes or gigabytes.  To accomplish this, add the <code>-h</code> option to the <code>ls</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -lh /usr/bin/omshell                                 
-rwxr-xr-c 1 root root 1.5M Oct 9 2012 <strong><span class="ansi-green">/usr/bin/omshell</span></strong>              
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<div class="alert alert-danger">Important: The <code>-h</code> option must be used with the <code>-l</code> option.</div>  

<h2><a name="12">1.2.4 Listing Directories</a></h2>
<p>When the command <code>ls -d</code> is used, it refers to the current directory, and not the contents within it.  Without any other options, it is rather meaningless, although it is important to note that the current directory is always referred to with a single period (<code class="console">.</code>):</p>


<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<strong>~</strong>$</strong> ls -d                                            
.                                                                      
</pre>                                                           

<p>To use the <code>ls -d</code> command in a meaningful way requires the addition of the <code>-l</code> option.  In this case, note that the first command lists the details of the contents in the <code class="console">/home/sysadmin</code> directory, while the second command lists the <code class="console">/home/sysadmin</code> directory itself.</p>


<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l                                            
total 0                                                                
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Desktop</span></strong>                 
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Documents</span></strong>              
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Downloads</span></strong>              
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Music</span></strong>                 
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Pictures</span></strong>              
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Public</span></strong>                 
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Templates</span></strong>              
drwxr-xr-x 1 sysadmin sysadmin   0 Apr 15  2015 <strong><span class="ansi-blue">Videos</span></strong>                
drwxr-xr-x 1 sysadmin sysadmin 420 Apr 15  2015 <strong><span class="ansi-blue">test</span></strong>                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -ld                                           
drwxr-xr-x 1 sysadmin sysadmin 224 Nov  7 17:07 <strong><span class="ansi-blue">.</span></strong>                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                                                                                    

<p>Note the single period at the end of the second long listing.  This indicates that the current directory is being listed, and not the contents.</p>

<h2><a name="13">1.2.5 Recursive Listing</a></h2>
<p>There will be times when you want to display all of the files in a directory as well as all of the files in all subdirectories under a directory.  This is called a <var>recursive listing</var>.  </p>

<p>To perform a recursive listing, use the <code>-R</code> option to the <code>ls</code> command:</p>

<div class="alert alert-info">
<strong>Note:</strong> The output shown below will vary from the results you will see if you execute the command within the virtual machine environment of this course.</div>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -R /etc/ppp                                         
/etc/ppp:                                                                     
chap-secrets   <strong><span class="ansi-green">ip-down.ipv6to4    ip-up.ipv6to4    ipv6-up</span></strong>    pap-secrets
<strong><span class="ansi-green">ip-down        ip-up              ipv6-down</span></strong>        options    <strong><span class="ansi-blue">peers</span></strong>

/etc/ppp/peers:
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>Note that in the previous example, the files in the <code class="console">/etc/ppp</code> directory were listed first.  After that, the files in the <code class="console">/etc/ppp/peers </code>directory were listed (there were no files in this case, but if any file had been in this directory, they would have been displayed).</p>

<p>Be careful with this option; for example, running the command <code>ls -R /</code> would list every file on the file system, including all files on any attached USB device and DVD in the system.  Limit the use of the <code>-R</code> option to smaller directory structures.</p>

<h2><a name="14">1.2.6 Sort a Listing</a></h2>
<p>By default, the <code>ls</code> command sorts files alphabetically by file name.  Sometimes, It may  be useful to sort files using different criteria. </p>

<p>To sort files by size, we can use the <code>-S</code> option.  Note the difference in the output of the following two commands:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /etc/ssh moduli           
ssh_host_dsa_key.pub    ssh_host_rsa_key     sshd_confi
ssh_config        ssh_host_ecdsa_key      ssh_host_rsa_key.pub        
ssh_host_dsa_key  ssh_host_ecdsa_key.pub  ssh_import_id               
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -S /etc/ssh moduli            
ssh_host_dsa_key      ssh_host_ecdsa_key            
sshd_config       ssh_host_dsa_key.pub  ssh_host_ecdsa_key.pub         
ssh_host_rsa_key  ssh_host_rsa_key.pub                                 
ssh_config        ssh_import_id                                        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>The same files and directories are listed, but in a different order.  While the <code>-S</code> option works by itself, you can't really tell that the output is sorted by size, so it is most useful when used with the <code>-l</code> option.  The following command will list files from largest to smallest and display the actual size of the file.</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -lS /etc/ssh                                  
total 160                                                             
-rw-r--r-- 1 root root 125749 Apr 29  2014 moduli                      
-rw-r--r-- 1 root root   2489 Jan 29  2015 sshd_config                
-rw------- 1 root root   1675 Jan 29  2015 ssh_host_rsa_key            
-rw-r--r-- 1 root root   1669 Apr 29  2014 ssh_config                  
-rw------- 1 root root    668 Jan 29  2015 ssh_host_dsa_key           
-rw-r--r-- 1 root root    607 Jan 29  2015 ssh_host_dsa_key.pub       
-rw-r--r-- 1 root root    399 Jan 29  2015 ssh_host_rsa_key.pub       
-rw-r--r-- 1 root root    302 Jan 10  2011 ssh_import_id               
-rw------- 1 root root    227 Jan 29  2015 ssh_host_ecdsa_key         
-rw-r--r-- 1 root root    179 Jan 29  2015 ssh_host_ecdsa_key.pub     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          

<p>It may also be useful to use the <code>-h</code> option to display human-readable file sizes:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -lSh /etc/ssh                                
total 160K                                                             
-rw-r--r-- 1 root root 123K Apr 29  2014 moduli                        
-rw-r--r-- 1 root root 2.5K Jan 29  2015 sshd_config                   
-rw------- 1 root root 1.7K Jan 29  2015 ssh_host_rsa_key              
-rw-r--r-- 1 root root 1.7K Apr 29  2014 ssh_config                   
-rw------- 1 root root  668 Jan 29  2015 ssh_host_dsa_key              
-rw-r--r-- 1 root root  607 Jan 29  2015 ssh_host_dsa_key.pub          
-rw-r--r-- 1 root root  399 Jan 29  2015 ssh_host_rsa_key.pub          
-rw-r--r-- 1 root root  302 Jan 10  2011 ssh_import_id           
-rw------- 1 root root  227 Jan 29  2015 ssh_host_ecdsa_key           
-rw-r--r-- 1 root root  179 Jan 29  2015 ssh_host_ecdsa_key.pub      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>

<p>
It is also possible to sort files based on the time they were modified.  You can do this by using the <code>-t</code> option.
</p>

<p>The <code>-t</code> option will list the most recently modified files first.  This option can be used alone, but again, is usually more helpful when paired with the <code>-l</code> option:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -tl /etc/ssh                                 
total 160                                                             
-rw------- 1 root root    668 Jan 29  2015 ssh_host_dsa_key            
-rw-r--r-- 1 root root    607 Jan 29  2015 ssh_host_dsa_key.pub        
-rw------- 1 root root    227 Jan 29  2015 ssh_host_ecdsa_key          
-rw-r--r-- 1 root root    179 Jan 29  2015 ssh_host_ecdsa_key.pub     
-rw------- 1 root root   1675 Jan 29  2015 ssh_host_rsa_key            
-rw-r--r-- 1 root root    399 Jan 29  2015 ssh_host_rsa_key.pub       
-rw-r--r-- 1 root root   2489 Jan 29  2015 sshd_config                
-rw-r--r-- 1 root root 125749 Apr 29  2014 moduli                      
-rw-r--r-- 1 root root   1669 Apr 29  2014 ssh_config                  
-rw-r--r-- 1 root root    302 Jan 10  2011 ssh_import_id               
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<div class="alert alert-danger">It is important to remember that the modified date on directories represents the last time a file was added to or removed from the directory.</div>

<p>If the files in a directory were modified many days or months ago, it may be harder to tell exactly when they were modified, as only the date is provided for older files.  For more detailed modification time information you can use the <code>--full-time</code> option to display the complete timestamp (including hours, seconds, minutes...):</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -t --full-time /etc/ssh                       
total 160                                                             
-rw------- 1 root root    668 2015-01-29 03:17:33.000000000 +0000 ssh_host_dsa_key                                                            
-rw-r--r-- 1 root root    607 2015-01-29 03:17:33.000000000 +0000 ssh_host_dsa_key.pub                                                         
-rw------- 1 root root    227 2015-01-29 03:17:33.000000000 +0000 ssh_host_ecdsa_key                                                           
-rw-r--r-- 1 root root    179 2015-01-29 03:17:33.000000000 +0000 ssh_host_ecdsa_key.pub                                                      
-rw------- 1 root root   1675 2015-01-29 03:17:33.000000000 +0000 ssh_host_rsa_key                                                             
-rw-r--r-- 1 root root    399 2015-01-29 03:17:33.000000000 +0000 ssh_host_rsa_key.pub                                                         
-rw-r--r-- 1 root root   2489 2015-01-29 03:17:33.000000000 +0000 sshd_config   
-rw-r--r-- 1 root root 125749 2014-04-29 23:58:51.000000000 +0000 moduli
-rw-r--r-- 1 root root   1669 2014-04-29 23:58:51.000000000 +0000 ssh_config    
-rw-r--r-- 1 root root    302 2011-01-10 18:48:29.000000000 +0000 ssh_import_id 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                      

<p>The <code>--full-time</code> option will assume the <code>-l</code> option automatically.</p>

<p>It is possible to perform a reverse sort with either the <code>-S</code> or <code>-t</code> options by using the <code>-r</code> option.  The following command will sort files by size, smallest to largest:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -lrS /etc/ssh                                 
total 160                                                              
-rw-r--r-- 1 root root    179 Jan 29  2015 ssh_host_ecdsa_key.pub      
-rw------- 1 root root    227 Jan 29  2015 ssh_host_ecdsa_key          
-rw-r--r-- 1 root root    302 Jan 10  2011 ssh_import_id               
-rw-r--r-- 1 root root    399 Jan 29  2015 ssh_host_rsa_key.pub        
-rw-r--r-- 1 root root    607 Jan 29  2015 ssh_host_dsa_key.pub        
-rw------- 1 root root    668 Jan 29  2015 ssh_host_dsa_key            
-rw-r--r-- 1 root root   1669 Apr 29  2014 ssh_config                  
-rw------- 1 root root   1675 Jan 29  2015 ssh_host_rsa_key            
-rw-r--r-- 1 root root   2489 Jan 29  2015 sshd_config                 
-rw-r--r-- 1 root root 125749 Apr 29  2014 moduli                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>The following command will list files by modification date, oldest to newest:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -lrt /etc/ssh                                 
total 160                                                              
-rw-r--r-- 1 root root    302 Jan 10  2011 ssh_import_id               
-rw-r--r-- 1 root root   1669 Apr 29  2014 ssh_config                  
-rw-r--r-- 1 root root 125749 Apr 29  2014 moduli                      
-rw-r--r-- 1 root root   2489 Jan 29  2015 sshd_config                 
-rw-r--r-- 1 root root    399 Jan 29  2015 ssh_host_rsa_key.pub        
-rw------- 1 root root   1675 Jan 29  2015 ssh_host_rsa_key            
-rw-r--r-- 1 root root    179 Jan 29  2015 ssh_host_ecdsa_key.pub      
-rw------- 1 root root    227 Jan 29  2015 ssh_host_ecdsa_key          
-rw-r--r-- 1 root root    607 Jan 29  2015 ssh_host_dsa_key.pub        
-rw------- 1 root root    668 Jan 29  2015 ssh_host_dsa_key            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre> 


<h2><a name="15">1.2.7 Listing With Globs</a></h2>
<p>In a previous chapter, we discussed the use of file globs to match filenames using wildcard characters.  For example, we demonstrated that you can list all of the files in the <code class="console">/etc</code> directory that begin with the letter <code class="console">e</code> with the following command:</p>



<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo /etc/e*                                    
/etc/encript.cfg /etc/environment /etc/ethers /etc/event.d /etc/exports
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>Now that you know that the <code>ls</code> command is normally used to list files in a directory, using the <code>echo</code> command may seem to have been a strange choice.  However, there is something about the <code>ls</code> command that might have caused confusion while we were discussing globs.  This "feature" might also cause problems when you try to list files using glob patterns.</p>

<p>Keep in mind that it is the shell, not the <code>echo</code> or <code>ls</code> command, that expands the glob pattern into corresponding file names.  In other words, when you typed the <code>echo /etc/e*</code> command, what the shell did <strong>before</strong> executing the <code>echo</code> command was replace <code class="console">e*</code> with all of the files and directories within the <code class="console">/etc</code> directory that match the pattern. </p> 

<p>So, if you were to run the <code>ls /etc/e*</code> command, what the shell would really run would be this:</p>

<pre class="config">ls /etc/encript.cfg /etc/environment /etc/ethers /etc/event.d /etc/exports</pre>

<p>When the <code>ls</code> command sees multiple arguments, it performs a list operation on each item separately.  In other words, the command <code>ls /etc/encript.cfg /etc/environment</code> is essentially the same as <code>ls /etc/encript.cfg; ls /etc/environment</code>.</p>

<p>Now consider what happens when you run the <code>ls</code> command on a file, such as <code class="console">encript.cfg</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /etc/enscript.cfg                             
/etc/enscript.cfg        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>As you can see, running the <code>ls</code> command on a single file results in the name of the file being printed.  Typically this is useful if you want to see details about a specific file by using the <code>-l</code> option to the <code>ls</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l /etc/enscript.cfg                         
-r--r--r--. 1 root root 4843 Nov 11 2010 /etc/enscript.cfg      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>However, what if the <code>ls</code> command is given a directory name as an argument?  In this case, the output of the command is different than if the argument was a file name:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /etc/event.d                                    
ck-log-system-restart  ck-log-system-start  ck-log-system-stop            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>If you give a directory name as an argument to the <code>ls</code> command, the command will display the <strong><var>contents</var></strong> of the directory (the names of the files in the directory), not just provide the directory name.  The filenames you see in the example above are the names of the files in the <code class="console">/etc/event.d</code> directory.
</p> 

<p>Why is this a problem when using globs?  Consider the following output:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /etc/e*                                          
/etc/encript.cfg /etc/environment /etc/ethers /etc/event.d /etc/exports       
/etc/event.d:
ck-log-system-restart  ck-log-system-start  ck-log-system-stop            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>   

<p>As you can see, when the <code>ls</code> command sees a filename as an argument, it just displays the filename.  However, for any directory, it will display the contents of the directory, not just the directory name.</p>

<p>This becomes even more confusing in a situation like the following:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls /etc/ev*                                        
ck-log-system-restart  ck-log-system-start  ck-log-system-stop            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                     

<p>In the previous example, it seems like the <code>ls</code> command is just plain wrong.  But what really happened is that the only thing that matches the glob <code class="console">/etc/ev*</code> is the <code class="console">/etc/event.d</code> directory.  So, the <code>ls</code> command only displayed the files in that directory!</p>

<p>There is a simple solution to this problem: when you use glob arguments with the <code>ls</code> command, always use the <code>-d</code> option.  When you use the <code>-d</code> option, then the <code>ls</code> command won't display the contents of a directory, but rather the name of the directory:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -d /etc/e*                                      
/etc/encript.cfg /etc/environment /etc/ethers <strong><span class="ansi-blue">/etc/event.d</span></strong> /etc/exports   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>  

<h2><a name="16">1.3 Copying Files</a></h2>
<p>The <code>cp</code> command is used to copy files.  It requires that you specify a source and a destination.  The structure of the command is as follows:</p>

<pre class="config">cp [source] [destination]</pre>

<p>The <var>source</var> is the file you wish to copy.  The <var>destination</var> is where you want the copy to be located.  When successful, the <code>cp</code> command will not have any output (no news is good news).  The following command will copy the <code class="console">/etc/hosts</code> file to your home directory:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp /etc/hosts ~                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                                  
<strong><span class="ansi-blue">Desktop</span></strong>    <strong><span class="ansi-blue">Downloads</span></strong>  <strong><span class="ansi-blue">Pictures</span></strong>  <strong><span class="ansi-blue">Templates</span></strong>  hosts                          
<strong><span class="ansi-blue">Documents</span></strong>  <strong><span class="ansi-blue">Music</span></strong>      <strong><span class="ansi-blue">Public</span></strong>    <strong><span class="ansi-blue">Videos</span></strong>                                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>                                                           

<div class="alert alert-info">
<strong>Remember:</strong> The <code class="console">~</code> character represents your home directory.</div>


<h2><a name="17">1.3.1 Verbose Mode</a></h2>
<p>The <code>-v</code> option will cause the <code>cp</code> command to produce output if successful.  The <code>-v</code> option stands for <var>verbose</var>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp -v /etc/hosts ~                              
`/etc/hosts' -&gt; `/home/sysadmin/hosts'                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                          

<p>When the destination is a directory, the resulting new file will have the same name as the original file.  If you want the new file to have a different name, you must provide the new name as part of the destination:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp /etc/hosts ~/hosts.copy                      
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop</span></strong>    <strong><span class="ansi-blue">Downloads</span></strong>  <strong><span class="ansi-blue">Pictures</span></strong>  <strong><span class="ansi-blue">Templates</span></strong>  hosts                       
<strong><span class="ansi-blue">Documents</span></strong>  <strong><span class="ansi-blue">Music</span></strong>      <strong><span class="ansi-blue">Public</span></strong>    <strong><span class="ansi-blue">Videos</span></strong>     hosts.copy                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>

<h2><a name="18">1.3.2 Avoid Overwriting Data</a></h2>
<p>The <code>cp</code> command can be destructive to existing data if the destination file already exists.  In the case where the destination file exists , the <code>cp</code> command will overwrite the existing file's contents with the contents of the source file.  To illustrate this potential problem, first a new file is created in the <code class="console">sysadmin</code> home directory by copying an existing file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp /etc/skel/.bash_logout ~/example.txt 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>    


<p>View the output of the <code>ls</code> command to see the file and view the contents of the file using the <code>more</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp /etc/skel/.bash_logout ~/example.txt
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l example.txt
-rw-rw-r--. 1 sysadmin sysadmin 18 Sep 21 15:56 example.txt
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> more example.txt
# ~/.bash_logout: executed by bash(1) when login shell exits.

<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp -i /etc/hosts ~/example.txt
cp: overwrite `/home/sysadmin/example.txt'? n
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l example.txt
-rw-rw-r--. 1 sysadmin sysadmin 18 Sep 21 15:56 example.txt
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> more example.txt
# ~/.bash_logout: executed by bash(1) when login shell exits.

<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>In the next example, you will see that the <code>cp</code> command destroys the original contents of the example.txt file.  Notice that after the <code>cp</code> command is complete, the size of the file is different (158 bytes rather than 18) from the original and the contents are different as well:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp /etc/hosts ~/example.txt
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l example.txt
-rw-rw-r--. 1 sysadmin sysadmin 158 Sep 21 14:11 example.txt
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cat example.txt
127.0.0.1  localhost localhost.localdomain localhost4 localhost4.localdomain4
::1        localhost localhost.localdomain localhost6 localhost6.localdomain6
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                                              

<p>There are two options that can be used to safeguard against accidental overwrites.  With the <code>-i</code> (interactive) option, the <code>cp</code> will prompt before overwriting a file.  The following example will demonstrate this option, first restoring the content of the original file:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp /etc/skel/.bash_logout ~/example.txt          
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l example.txt                                
-rw-r--r-- 1 sysadmin sysadmin 18 Sep 21 15:56 example.txt           
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> more example.txt                                 
# ~/.bash_logout: executed by bash(1) when login shell exits.         

<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp -i /etc/hosts ~/example.txt                   
cp: overwrite `/home/sysadmin/example.txt'? n                          
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l example.txt                                
-rw-r--r-- 1 sysadmin sysadmin 18 Sep  21 15:56 example.txt            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> more example.txt                                
# ~/.bash_logout: executed by bash(1) when login shell exits.          

<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>



<p>Notice that since the value of <code class="console">n</code> (no) was given when prompted to overwrite the file, no changes were made to the file.  If a value of <code class="console">y</code> (yes) was given, then the copy process would have taken place.</p>

<p>The <code>-i</code> option requires you to answer <code class="console">y</code> or <code class="console">n</code> for every copy that could end up overwriting an existing file's contents.  This can be tedious when a bunch of overwrites could occur, such as the example demonstrated below:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp -i /etc/skel/.* ~                             
cp: omitting directory `/etc/skel/.'                                   
cp: omitting directory `/etc/skel/..'                                  
cp: overwrite `/home/sysadmin/.bash_logout'? n                         
cp: overwrite `/home/sysadmin/.bashrc'? n                              
cp: overwrite `/home/sysadmin/.profile'? n                            
cp: overwrite `/home/sysadmin/.selected_editor'? n                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>      

<p>As you can see from the example above, the <code>cp</code> command tried to overwrite four existing files, forcing the user to answer three prompts.  If this situation happened for 100 files, it could become very annoying, very quickly.</p>

<p>If you want to automatically answer <strong>n</strong> to each prompt, use the <code>-n</code> option.  It essentially stands for "no rewrite”.</p>

<h2><a name="19">1.3.3 Copying Directories</a></h2>
<p>In a previous example, error messages were given when the <code>cp</code> command attempted to copy directories:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cp -i /etc/skel/.* ~                             
cp: omitting directory `/etc/skel/.'                                   
cp: omitting directory `/etc/skel/..'                                  
cp: overwrite `/home/sysadmin/.bash_logout'? n                         
cp: overwrite `/home/sysadmin/.bashrc'? n                              
cp: overwrite `/home/sysadmin/.profile'? n                            
cp: overwrite `/home/sysadmin/.selected_editor'? n                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>      


<p>Where the output says <code class="console">...omitting directory...</code>, the <code>cp</code> command is saying that it cannot copy this item because the command does not copy directories by default.  However, the <code>-r</code> option to the <code>cp</code> command will have it copy both files and directories.</p>

<p>Be careful with this option: the entire directory structure will be copied.  This could result in copying a lot of files and directories!</p>

<h2><a name="20">1.4 Moving Files</a></h2>
<p>To move a file, use the <code>mv</code> command.  The syntax for the <code>mv</code> command is much like the <code>cp</code> command:</p>

<pre class="config">mv [source] [destination]</pre>

<p>In the following example, the <code class="console">hosts</code> file that was generated earlier is moved from the current directory to the <code class="console">Videos</code> directory:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates  example.txt  hosts.copy     
Documents  Music      Public    Videos</span></strong>     hosts                       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> mv hosts Videos                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates  example.txt                 
Documents  Music      Public    Videos</span></strong>     hosts.copy                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls Videos                                        
hosts                                                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           

<p>When a file is moved, the file is removed from the original location and placed in a new location.  This can be somewhat tricky in Linux because users need specific permissions to remove files from a directory.  If you don't have the right permissions, you will receive a "<code class="console">Permission denied</code>" error message:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> mv /etc/hosts .                                  
mv: cannot move `/etc/hosts' to `./hosts': Permission denied           
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>                                                        

<div class="alert alert-info">A detailed discussion of permissions is provided in a later chapter.</div>

<h2><a name="21">1.5 Moving Files While Renaming</a></h2>
<p>If the destination for the <code>mv</code> command is a directory, the file will be moved to the directory specified.  The file name will change only if a destination file name is also specified.</p>

<p>If a destination directory is not specified, the file will be renamed using the destination file name and remain in the source directory.</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  example.txt                 
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>                    
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> mv example.txt Videos/newexample.txt             
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates                  
Documents  Music      Public    Videos</span></strong>                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls Videos                                       
hosts  newexample.txt                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>

<h2><a name="22">1.5.1 Renaming Files</a></h2>
<p>The <code>mv</code> command is not just used to move a file, but also to rename a file.  For example, the following commands will rename the <code class="console">newexample.txt</code> file to <code class="console">myexample.txt</code>:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> cd Videos                                        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/Videos</span>$</strong> ls                                        
hosts  newexample.txt                                                  
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/Videos</span>$</strong> mv newexample.txt myexample.txt           
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/Videos</span>$</strong> ls                                        
hosts  myexample.txt                                                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~/Videos</span>$</strong></pre>                                                    

<p>Think of the previous <code>mv</code> example to mean "move the <code class="console">newexample.txt</code> file from the current directory back into the current directory and give the new file the name <code class="console">myexample.txt</code>”.</p>

<h2><a name="23">1.5.2 Additional mv Options</a></h2>
<p>Like the <code>cp</code> command, the <code>mv</code> command provides the following options:</p>

<table class="table ">
<thead><tr>
<th>Option</th>
<th>Meaning</th>
</tr></thead>
<tbody>
<tr>
<td><code>-i</code></td>
<td>Interactive move: ask if a file is to be overwritten.</td>
</tr>
<tr>
<td><code>-n</code></td>
<td>Do not overwrite a destination files' contents</td>
</tr>
<tr>
<td><code>-v</code></td>
<td>Verbose: show the resulting move</td>
</tr>
</tbody>
</table>

<div class="alert alert-danger">
<strong>Important:</strong> There is no <code>-r</code> option as the <code>mv</code> command will by default move directories.</div>

<h2><a name="24">1.6 Creating Files</a></h2>
<p>There are several ways of creating a new file, including using a program designed to edit a file (a text editor).  In a later chapter, text editors will be covered.</p>

<p>There is also a way to simply create a file that can be populated with data at a later time.  This is a useful feature since for some operating system features, the very existence of a file could alter how a command or service works.  It is also useful to create a file as a "placeholder" to remind you to create the file contents at a later time.</p>

<p>To create an empty file, use the <code>touch</code> command as demonstrated below:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                                
<strong><span class="ansi-blue">Desktop  Documents  Downloads  Music  Pictures  Public  Templates  
Videos</span></strong> 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> touch sample                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls -l sample                                     
-rw-rw-r-- 1 sysadmin sysadmin 0 Nov  9 16:48 sample                   
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>                                                           

<p>Notice the size of the new file is 0 bytes.  As previously mentioned, the <code>touch</code> command doesn't place any data within the new file.</p>

<h2><a name="25">1.7 Removing Files</a></h2>
<p>To delete a file, use the <code>rm</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  sample                      
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> rm sample                                        
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop  Documents  Downloads  Music  Pictures  Public  Templates  
Videos</span></strong>       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong>
</pre>                                                          

<p>Note that the file was deleted with no questions asked.  This could cause problems when deleting multiple files by using glob characters, for example: <code>rm *.txt</code>.  Because these files are deleted without question, a user could end up deleting files that were not intended to be deleted.</p>

<p>Additionally, the files are permanently deleted.  There is no command to undelete a file and no "trash can" from which to recover deleted files.  As a precaution, users should use the <code>-i</code> option when deleting multiple files:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> touch sample.txt example.txt test.txt            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  example.txt  test.txt       
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>     sample.txt                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> rm -i *.txt                                     
rm: remove regular empty file `example.txt'? y                         
rm: remove regular empty file `sample.txt'? n                          
rm: remove regular empty file `test.txt'? y                            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  sample.txt                  
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>  

<h2><a name="26">1.8 Removing Directories</a></h2>
<p>You can delete directories using the <code>rm</code> command.  However, the default usage (no options) of the <code>rm</code> command will fail to delete a directory:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> rm Videos                                        
rm: cannot remove `Videos': Is a directory                            
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>    

<p>If you want to delete a directory, use the <code>-r</code> option to the <code>rm</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates</span></strong>  sample.txt                  
<strong><span class="ansi-blue">Documents  Music      Public    Videos</span></strong>                                 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> rm -r Videos                                     
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop  Documents  Downloads  Music  Pictures  Public  Templates</span></strong> 
sample.txt 
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>                                                           
<div class="alert alert-danger">
<strong>Important:</strong> When a user deletes a directory, all of the files and subdirectories are deleted without any interactive question.  It is best to use the <code>-i</code> option with the <code>rm</code> command.</div>

<p>You can also delete a directory with the <code>rmdir</code> command, but only if the directory is empty.</p>

<h2><a name="27">1.9 Making Directories</a></h2>
<p>To create a directory, use the <code>mkdir</code> command:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop  Documents  Downloads  Music  Pictures  Public  Templates</span></strong>  
sample.txt
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> mkdir test                                       
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ls                                               
<strong><span class="ansi-blue">Desktop    Downloads  Pictures  Templates   test                       
Documents  Music      Public</span></strong>    sample.txt                             
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong></pre>           

*Все материалы взяты с официального курса <i class="fa fa-link"></i> [NDG Linux Essential](https://www.netacad.com/ru/courses/ndg-linux-essentials/)*
