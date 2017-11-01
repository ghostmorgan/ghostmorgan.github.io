---
bg: "linux.jpg"
layout: post
comments: true
title:  "Basic Scripting"
crawlertitle: "Basic Scripting"
summary: "Базовые понятия написания скриптов"
date:   2017-11-01 16:15:00 +0300
categories: posts
tags: ['linux']
author: DenIvTea
---


<p>In this chapter, we will discuss how the tools you have learned so far can be turned into reusable scripts.</p>

Навигация по статье:

* <a href="#1">1.1 Shell Scripts in a Nutshell</a>
* <a href="#2">1.2 Editing Shell Scripts</a>
* <a href="#3">1.3 Scripting Basics</a>
* <a href="#4">1.3.1 Variables</a>
* <a href="#5">1.3.2 Conditionals</a>
* <a href="#6">1.3.3 Loops</a>


<h2><a name="1">1.1 Shell Scripts in a Nutshell</a></h2>
<p>A <var>shell script</var> is a file of executable commands that has been stored in a text file.  When the file is run, each command is executed.  Shell scripts have access to all the commands of the shell, including logic. A script can therefore test for the presence of a file or look for particular output and change its behavior accordingly. You can build scripts to automate repetitive parts of your work, which frees your time and ensures consistency each time you use the script.  For instance,  if you run the same five commands every day, you can turn them into a shell script that  reduces your work to one command.</p>

<p>A script can be as simple as one command:</p>

<pre class="config">echo “Hello, World!”</pre>

<p>The script, <code class="console">test.sh</code>, consists of just one line that prints the string <code class="console">Hello, World!</code> to the console.</p>

<p>Running a script can be done either by passing it as an argument to your shell or by running it directly:</p>

<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> sh test.sh
Hello, World!
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ./test.sh
-bash: ./test.sh: Permission denied
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> chmod +x ./test.sh
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> ./test.sh
Hello, World!
</pre>

<p>In the example above, first, the script is run as an argument to the shell. Next, the script is run directly from the shell. It is rare to have the current directory in the binary search path <code class="console">$PATH</code> so the name is prefixed with <code class="console">./</code> to indicate it should be run out of the current directory.</p>

<p>The error <code class="console">Permission denied</code> means that the script has not been marked as executable. A quick <code>chmod</code> later and the script works. <code>chmod</code> is used to change the permissions of a file, which will be explained in detail in a later chapter.</p>

<p>There are various shells with their own language syntax. Therefore, more complicated scripts will indicate a particular shell by specifying the absolute path to the interpreter as the first line, prefixed by <code class="console">#!</code> as shown:</p>

<pre class="config">#!/bin/sh
echo “Hello, World!”</pre>

<p>or</p>

<pre class="config">#!/bin/bash
echo “Hello, World!”</pre>

<p>The two characters, <code class="console">#!</code> are traditionally called the hash and the bang respectively, which leads to the shortened form of <var>“shebang”</var> when they’re used at the beginning of a script.</p>

<p>Incidentally, the shebang (or crunchbang) is used for traditional shell scripts and other text-based languages like Perl, Ruby, and Python.  Any text file marked as executable will be run under the interpreter specified in the first line as long as the script is run directly. If the script is invoked directly as an argument to an interpreter, such as <code class="console">sh script</code> or <code class="console">bash script</code>, the given shell will be used no matter what’s in the shebang line.</p>

<div class="alert alert-info">It helps to become comfortable using a text editor before writing shell scripts, since you will need to create files in plain text.  Traditional office tools like LibreOffice that output file formats containing formatting and other information are not appropriate for this task.</div>

<h2><a name="2">1.2 Editing Shell Scripts</a></h2>
<p>UNIX has many text editors, the merits of one over the other are often hotly debated. Two are specifically mentioned in the LPI Essentials syllabus: The GNU nano editor is a very simple editor well suited to editing small text files. The Visual Editor, <code>vi</code>, or its newer version, VI improved (<code>vim</code>), is a remarkably powerful editor but has a steep learning curve. We’ll focus on <code>nano</code>.</p>

<p>Type <code>nano test.sh</code> and you’ll see a screen similar to this:</p>

<pre class="content_terminal"><code class="input">GNU nano 2.2.6</code>              <code class="input">File: test.sh</code>                         <code class="input">modified</code>

#!/bin/sh

echo "Hello, World!"
echo -n "the time is "
date
                                    
                                                                                
                                                                                
                                                                                
                                                                                
                                                                                
                                                                                
<code class="input">^G</code> Get Help  <code class="input">^O</code> WriteOut  <code class="input">^R</code> Read File <code class="input">^Y</code> Prev Page <code class="input">^K</code> Cut Text  <code class="input">^C</code> Cur Po 
<code class="input">^X</code> Exit      <code class="input">^J</code> Justify   <code class="input">^W</code> Where Is  <code class="input">^V</code> Next Page <code class="input">^U</code> UnCut Text<code class="input">^T</code> To Spell</pre>    

<p>The <code>nano</code> editor has few features to get you on your way.  You simply type with your keyboard, using the arrow keys to move around and the <strong>delete</strong>/<strong>backspace</strong> button to delete text. Along the bottom of the screen you can see some commands available to you, which are context sensitive and change depending on what you’re doing. If you’re directly on the Linux machine itself, as opposed to connecting over the network, you can also use the mouse to move the cursor and highlight text.</p>

<p>To get familiar with the editor, start typing out a simple shell script while inside <code>nano</code>:</p>

<pre class="content_terminal"><code class="input">GNU nano 2.2.6</code>              <code class="input">File: test.sh</code>                         <code class="input">modified</code>

#!/bin/sh

echo "Hello, World!"
echo -n "the time is "
date
                                    
                                                                                
                                                                                                                                                                
                                                                                                                                                            
                                                                                
<code class="input">^G</code> Get Help  <code class="input">^O</code> WriteOut  <code class="input">^R</code> Read File <code class="input">^Y</code> Prev Page <code class="input">^K</code> Cut Text  <code class="input">^C</code> Cur Po 
<code class="input">^X</code> Exit      <code class="input">^J</code> Justify   <code class="input">^W</code> Where Is  <code class="input">^V</code> Next Page <code class="input">^U</code> UnCut Text<code class="input">^T</code> To Spell</pre>    

<p>Note that the bottom-left option is <code class="console">^X Exit</code> which means “press <strong>control</strong> and <strong>X</strong> to exit”.  Press <strong>Ctrl</strong> and <strong>X</strong> together and the bottom will change:</p>

<pre class="content_terminal"><code class="input">Save modified buffer (ANSWERING "No" WILL DESTROY CHANGES) ?</code>                 
 <code class="input">Y</code> Yes                                                                       
 <code class="input">N</code> No           <code class="input">^C</code> Cancel</pre>             

<p>At this point, you can exit the program without saving by pressing the <strong>N</strong> key, or save first by pressing <strong>Y</strong> to save. The default is to save the file with the current file name.  You can press the <strong>Enter</strong> key to save and exit.</p>

<p>You will be back at the shell prompt after saving.  Return to the editor.  This time press <strong>Ctrl</strong>  and <strong>O</strong> together to save your work without exiting the editor. The prompts are largely the same, except that you’re back in the editor.</p>

<p>This time use the arrow keys to move your cursor to the line that has <code class="console">"The time is”</code>. Press <strong>Control</strong> and <strong>K</strong> twice to cut the last two lines to the copy buffer. Move your cursor to the remaining line and press <strong>Control</strong> and <strong>U</strong> once to paste the copy buffer to the current position. This makes the script echo the current time before greeting you and saved you needing to re-type the lines.</p>

<p>Other helpful commands you might need are:</p>

<table class="table ">
<thead><tr>
<th>Command</th>
<th>Description</th>
</tr></thead>
<tbody>
<tr>
<td>
<strong>Ctrl</strong> + <strong>W</strong>
</td>
<td>search the document</td>
</tr>
<tr>
<td>
<strong>Ctrl</strong> + <strong>W</strong>, then <strong>Control</strong> + <strong>R</strong>
</td>
<td>search and replace</td>
</tr>
<tr>
<td>
<strong>Ctrl</strong> + <strong>G</strong>
</td>
<td>show all the commands possible</td>
</tr>
<tr>
<td>
<strong>Ctrl</strong> + <strong>Y</strong>/<strong>V</strong>
</td>
<td>page up / down</td>
</tr>
<tr>
<td>
<strong>Ctrl</strong> + <strong>C</strong>
</td>
<td>show the current position in the file and the file’s size</td>
</tr>
</tbody>
</table>

<h2><a name="3">1.3 Scripting Basics</a></h2>
<p>You got your first taste of scripting earlier in this chapter where we introduced a very basic script that ran a single command. The script started with the shebang line, telling Linux that /bin/bash (which is Bash) is to be used to execute the script. </p>

<p>Other than running commands, there are 3 topics you must become familiar with:</p>

<ol type="disc" class="">
<li>Variables, which hold temporary information in the script</li>
<li>Conditionals, which let you do different things based on tests you write</li>
<li>Loops, which let you do the same thing over and over</li>
</ol>
<h2><a name="4">1.3.1 Variables</a></h2>
<p>Variables are a key part of any programming language. A very simple use of variables is shown here:</p>

<pre class="config">#!/bin/bash

ANIMAL="penguin"
echo "My favorite animal is a $ANIMAL"
</pre>

<p>After the shebang line is a directive to assign some text to a variable.  The variable name is <code class="console">ANIMAL</code> and the equals sign assigns the string <code class="console">penguin</code>. Think of a variable like a box in which you can store things.  After executing this line, the box called <code class="console">ANIMAL</code> contains the word <code class="console">penguin</code>.</p>

<p>It is important that there are no spaces between the name of the variable, the equals sign, and the item to be assigned to the variable. If you have a space there, you will get an odd error such as “<code class="console">command not found</code>”. Capitalizing the name of the variable is not necessary but it is a useful convention to separate variables from commands to be executed.</p>

<p>Next, the script echos a string to the console. The string contains the name of the variable preceded by a dollar sign. When the interpreter sees that dollar sign it recognizes that it will be substituting the contents of the variable, which is called <var>interpolation</var>. The output of the script is then <code class="console">My favorite animal is a penguin</code>.</p>

<p>So remember this: To assign to a variable, just use the name of the variable. To access the contents of the variable, prefix it with a dollar sign. Here, we show a variable being assigned the contents of another variable!</p>

<pre class="config">#!/bin/bash

ANIMAL=penguin
SOMETHING=$ANIMAL
echo "My favorite animal is a $SOMETHING"
</pre>

<p><code class="console">ANIMAL</code> contains the string <code class="console">penguin</code> (as there are no spaces, the alternative syntax without using quotes is shown). <code class="console">SOMETHING</code> is then assigned the contents of <code class="console">ANIMAL</code> (because <code class="console">ANIMAL</code> has the dollar sign in front of it).</p>

<p>If you wanted, you could assign an interpolated string to a variable. This is quite common in larger scripts, as you can build up a larger command and execute it!</p>

<p>Another way to assign to a variable is to use the output of another command as the contents of the variable by enclosing the command in back ticks:</p>

<pre class="config">#!/bin/bash
CURRENT_DIRECTORY=`pwd`
echo "You are in $CURRENT_DIRECTORY"
</pre>

<p>This pattern is often used to process text. You might take text from one variable or an input file and pass it through another command like <code>sed</code> or <code>awk</code> to extract certain parts and keep the result in a variable.</p>

<p>It is possible to get input from the user of your script and assign it to a variable through the <code>read</code> command:</p>
<pre class="config">#!/bin/bash

echo -n "What is your name? "
read NAME
echo "Hello $NAME!"
</pre>

<p>The <code>read</code> command can accept a string right from the keyboard or as part of command redirection like you learned in the last chapter.</p>

<p>There are some special variables in addition to the ones you set. You can pass arguments to your script:</p>

<pre class="config">#!/bin/bash
echo "Hello $1"
</pre>

<p>A dollar sign followed by a number <var>N</var> corresponds to the <var>Nth</var> argument passed to the script. If you call the example above with <code>./test.sh</code> the output will be <code class="console">Hello Linux</code>. The <code class="console">$0</code> variable contains the name of the script itself.</p>

<p>After a program runs, be it a binary or a script, it returns an <var>exit code </var>which is an integer between 0 and 255. You can test this through the <code class="console">$?</code> variable to see if the previous command completed successfully. </p>


<pre class="content_terminal"><strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep -q root /etc/passwd
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo $?
0
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> grep -q slartibartfast /etc/passwd
<strong><span class="ansi-green">sysadmin@localhost</span>:<span class="ansi-blue">~</span>$</strong> echo $?
1
</pre>

<p>The <code>grep</code> command was used to look for a string within a file with the <code>–q</code> flag, which means “quiet”. The <code>grep</code>, while running in quiet mode, returns <code class="console">0</code> if the string was found and <code class="console">1</code> otherwise. This information can be used in a conditional to perform an action based on the output of another command.</p>

<p>Likewise you can set the exit code of your own script with the <code>exit</code> command:</p>

<pre class="config">#!/bin/bash
# Something bad happened!
exit 1
</pre>

<p>The example above shows a comment <code class="console">#</code>. Anything after the hash mark is ignored which can be used to help the programmer leave notes. The <code class="console">exit 1</code> returns exit code <code class="console">1</code> to the caller. This even works in the shell, if you run this script from the command line and then type <code>echo $?</code> you will see it returns <code class="console">1</code>.</p>

<p>By convention, an exit code of <code>0</code> means “everything is OK”. Any exit codes greater than <code class="console">0</code> mean some kind of error happened, which is specific to the program. Above you saw that <code>grep</code> uses <code class="console">1</code> to mean the string was not found.</p>

<h2><a name="5">1.3.2 Conditionals</a></h2>
<p>Now that you can look at and set variables, it is time to make your script do different functions based on tests, called <var>branching</var>. The if statement is the basic operator to implement branching.</p>

<p>A basic <code class="console">if</code> statement looks like this:</p>

<pre class="config">if somecommand; then
  # do this if somecommand has an exit code of 0
fi
</pre>

<p>The next example will run “somecommand” (actually, everything up to the semicolon) and if the exit code is <code class="console">0</code> then the contents up until the closing <code class="console">fi</code> will be run. Using what you know about <code>grep</code>, you can now write a script that does different things based on the presence of a string in the password file:</p>

<pre class="config">#!/bin/bash

if grep -q root /etc/passwd; then
  echo root is in the password file
else
  echo root is missing from the password file
fi
</pre>

<p>From previous examples, you might remember that the exit code of <code>grep</code> is <code class="console">0</code> if the string is found.  The example above uses this in one line to print a message if <code class="console">root</code> is in the password file or a different message if it isn’t.  The difference here is that instead of an <code class="console">fi</code> to close off the <code class="console">if</code> block, there’s an <code class="console">else</code>. This lets you do one action if the condition is true, and another if the condition is false. The <code class="console">else</code> block must still be closed with the <code class="console">fi</code> keyword.</p>

<p>Other common tasks are to look for the presence of a file or directory and to compare strings and numbers. You might initialize a log file if it doesn’t exist, or compare the number of lines in a file to the last time you ran it. The <code class="console">if</code> command is clearly the one to help here, but what command do you use to make the comparison?</p>

<p>The <code>test</code> command gives you easy access to comparison and file test operators. For example:</p>

<table class="table ">
<thead><tr>
<th>Command</th>
<th>Description</th>
</tr></thead>
<tbody>
<tr>
<td><code>test –f /dev/ttyS0</code></td>
<td>
<code class="console">0</code> if the file exists</td>
</tr>
<tr>
<td><code>test ! –f /dev/ttyS0</code></td>
<td>
<code class="console">0</code> if the file doesn’t exist</td>
</tr>
<tr>
<td><code>test –d /tmp</code></td>
<td>
<code class="console">0</code> if the directory exists</td>
</tr>
<tr>
<td><code>test –x `which ls`</code></td>
<td>substitute the location of <code>ls</code> then <code>test</code> if the user can execute</td>
</tr>
<tr>
<td><code>test 1 –eq 1</code></td>
<td>
<code class="console">0</code> if numeric comparison succeeds</td>
</tr>
<tr>
<td><code>test ! 1 –eq 1</code></td>
<td>
<code class="console">NOT – 0</code> if the comparison fails</td>
</tr>
<tr>
<td><code>test 1 –ne 1</code></td>
<td>Easier, <code>test</code> for numeric inequality</td>
</tr>
<tr>
<td><code>test “a” = “a”</code></td>
<td>
<code class="console">0</code> if the string comparison succeeds</td>
</tr>
<tr>
<td><code>test “a” != “a”</code></td>
<td>
<code class="console">0</code> if the strings are different</td>
</tr>
<tr>
<td><code>test 1 –eq 1 –o 2 –eq 2</code></td>
<td>
<code>-o</code> is OR: either can be the same</td>
</tr>
<tr>
<td><code>test 1 –eq 1 –a 2 –eq 2</code></td>
<td>
<code>-a</code> is AND: both must be the same </td>
</tr>
</tbody>
</table>

<p>It is important to note that <code>test</code> looks at integer and string comparisons differently. <code class="console">01</code> and <code class="console">1</code> are the same by numeric comparison, but not by string comparison. You must always be careful to remember what kind of input you expect.</p>

<p>There are many more tests, such as <code>–gt</code> for greater than, ways to test if one file is newer than the other, and many more. Consult the <code>test</code> <code>man</code> page for more.</p>

<p><code>test</code> is fairly verbose for a command that gets used so frequently, so there is an alias for it called <code class="console">[</code> (left square bracket). If you enclose your conditions in square brackets, it’s the same as running <code>test</code>.  So, these statements are identical.</p>

<pre class="config">if test –f /tmp/foo; then
if [ -f /tmp/foo]; then
</pre>

<p>While the latter form is most often used, it is important to understand that the square bracket is a command on its own that operates similarly to <code>test</code> except that it requires the closing square bracket.</p>

<p>The <code class="console">if</code> statement has a final form that lets you do multiple comparisons at one time using <code class="console">elif</code> (short for <code class="console">else</code> <code class="console">if</code>).</p>

<pre class="config">#!/bin/bash

if [ "$1" = "hello" ]; then
  echo "hello yourself"
elif [ "$1" = "goodbye" ]; then
  echo "nice to have met you"
  echo "I hope to see you again"
else
  echo "I didn't understand that"
fi
</pre>

<p>The code above compares the first argument passed to the script. If it is <code class="console">hello</code>, the first block is executed. If not, the script checks to see if it is <code class="console">goodbye</code> and <var>echos</var> a different message if so. Otherwise, a third message is sent. Note that the <code class="console">$1</code> variable is quoted and the string comparison operator is used instead of the numeric version (<code>-eq</code>).</p>

<p>The <code class="console">if</code>/<code class="console">elif</code>/<code class="console">else</code> tests can become quite verbose and complicated. The <code class="console">case</code> statement provides a different way of making multiple tests easier.</p>

<pre class="config">#!/bin/bash

case "$1" in
hello|hi)
  echo "hello yourself"
  ;;
goodbye)
  echo "nice to have met you"
  echo "I hope to see you again"
  ;;
*)
  echo "I didn't understand that"
esac
</pre>

<p>The <code class="console">case</code> statement starts off with a description of the expression being tested: <code class="console">case <var>EXPRESSION</var> in</code>. The expression here is the quoted <code class="console">$1</code>.</p>

<p>Next, each set of tests are executed as a pattern match terminated by a closing parenthesis. The previous example first looks for <code class="console">hello</code> or <code class="console">hi</code>; multiple options are separated by the vertical bar <code class="console">|</code> which is an OR operator in many programming languages.  Following that are the commands to be executed if the pattern returns true, which are terminated by two semicolons. The pattern repeats.</p>

<p>The <code class="console">*</code> pattern is the same as an <code class="console">else</code> because it matches anything. The behavior of the <code class="console">case</code> statement is similar to the <code class="console">if</code>/<code class="console">elif</code>/<code class="console">else</code> statement in that processing stops after the first match. If none of the other options matched the <code class="console">*</code> ensures that the last one will match.</p>

<p>With a solid understanding of conditionals you can have your scripts take actions only if necessary.</p>

<h2><a name="6">1.3.3 Loops</a></h2>
<p>Loops allow code to be executed repeatedly.  They can be useful in numerous situations,  such as when you want to run the same commands over each file in a directory, or repeat some action 100 times. There are two main loops in shell scripts: the <code class="console">for</code> loop and the <code class="console">while</code> loop.</p>

<p><code class="console">for</code> loops are used when you have a finite collection over which you want to iterate, such as a list of files, or a list of server names:</p>

<pre class="config">#!/bin/bash

SERVERS="servera serverb serverc"
for S in $SERVERS; do
  echo "Doing something to $S"
done
</pre>

<p>The script first sets a variable containing a space separated list of server names. The <code class="console">for</code> statement then loops over the list of servers, each time it sets the <code class="console">S</code> variable to the current server name. The choice of <code class="console">S</code> was arbitrary, but note that the <code class="console">S</code> has no dollar sign but the <code class="console">$SERVERS</code> does, showing that <code class="console">$SERVERS</code> will be expanded to the list of servers. The list does not have to be a variable. This example shows two more ways to pass a list.</p>

<pre class="config">#!/bin/bash

for NAME in Sean Jon Isaac David; do
  echo "Hello $NAME"
done

for S in *; do
  echo "Doing something to $S"
done
</pre>

<p>The first loop is functionally the same as the previous example, except that the list is passed to the <code class="console">for</code> loop directly instead of using a variable. Using a variable helps the clarity of the script as someone can easily make changes to the variable rather than looking at a loop.</p>

<p>The second loop uses a <code class="console">*</code> which is a <var>file glob</var>. This gets expanded by the shell to all the files in the current directory.</p>

<p>The other type of loop, a <code class="console">while</code> loop, operates on a list of unknown size. Its job is to keep running and on each iteration perform a <code>test</code> to see if it should run another time. You can think of it as “while some condition is true, do stuff.”</p>

<pre class="config">#!/bin/bash

i=0
while [ $i -lt 10 ]; do
  echo $i
  i=$(( $i + 1))
done
echo “Done counting”
</pre>

<p>The example above shows a <code class="console">while</code> loop that counts from 0 to 9. A counter variable, <code class="console">i</code>, is initialized to <code class="console">0</code>. Then a <code class="console">while</code> loop is run with the <code>test</code> being “is <code class="console">$i</code> less than <code class="console">10</code>?” Note that the <code class="console">while</code> loop uses the same notation as an <code class="console">if</code> statement!</p>

<p>Within the <code class="console">while</code> loop the current value of <code class="console">i</code> is <var>echoed</var> and then <code class="console">1</code> is added to it through the <code class="console">$(( <var>arithmetic</var> ))</code> command and assigned back into <code class="console">i</code>. Once <code class="console">i</code> becomes 10 the <code class="console">while</code> statement returns false and processing continues after the loop.</p>

*Все материалы взяты с официального курса <i class="fa fa-link"></i> [NDG Linux Essential](https://www.netacad.com/ru/courses/ndg-linux-essentials/)*
