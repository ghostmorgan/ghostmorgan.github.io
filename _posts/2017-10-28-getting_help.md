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
<h2>5.1 man Pages</h2>
<p>As previously mentioned, UNIX was the operating system from which the Linux foundation was built.  The developers of UNIX created help documents called <var>man pages</var> (man stands for manual).</p>

<p>Man pages are used to describe the features of commands.  They will provide you with a basic description of the purpose of the command, as well as provide details regarding the options of the command.</p>

<h2>5.1.1 Viewing man pages</h2>
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
