# Lab 1: Linux and Mimir Basics

### Goals

This lab will let you working in Linux and using Command Line Interfaces (CLIs). 
Along the way, you'll get some practice with several important Linux sysadmin concepts, including

  - experience with the fundamental Linux commands
  - understanding of directory hierarchies and file system organization
  - understanding of relative and absolute paths

In the second part of the lab, you'll work with Mimir, the software platform we're using this semester.  You'll also write your first C program.

### Pre-lab prep
Let's get the boring lecture out of the way before lab, so you can spend this entire lab period 
playing around with the basics of the Linux CLI.  To begin, watch these videos (in order or they won't make sense).  All of them are on YouTube and range from 7-10 minutes each and total about 1 hour and 15 minutes.

1. [Command Line Interfaces](https://www.youtube.com/watch?v=3WddgzyhHk8)
2. [Directory Hierarchies](https://www.youtube.com/watch?v=MdMCWKpWbjc)
3. [Basic Linux Commands](https://www.youtube.com/watch?v=wNB72BaH6rA)
4. [Paths and Special Directories](https://www.youtube.com/watch?v=RPviGYRAdgU)
5. [Relative and Absolute Paths](https://www.youtube.com/watch?v=sqX6hu7oEew)
6. [Command Flags](https://www.youtube.com/watch?v=fU6BDYVE2og)
7. [Creating and Deleting Directories](https://www.youtube.com/watch?v=AVzqquRi_-g)
8. [Copying Files](https://www.youtube.com/watch?v=MYe58LbbfVU)
9. [Moving/renaming Files and Directories](https://www.youtube.com/watch?v=GKEGNdNIQrw)

You may also want to refer to [Notes on Linux and the Terminal Environment](../c-programming/c-chap02.md) which you already read during the first week of class.

### Getting Started
All the following steps assume you've already created your accounts and the connection as specified in the software setup discussed on the first day of class.  If you haven't done this, you need to follow the instructions on the software setup page before beginning.  See the link on the class calendar.

Log into mimir.  You should see a project named Lab1; click on it. Open this project in the Mimir IDE (button on the right hand side). You will probably see two windows.  One of these is for writing your source code and one of them will be a terminal as you've seen me use during class.  You can close the source code window for now.  You won't need it until part 2 of the lab.

### Part I

Work through the following commands, one at a time, at the prompt. After each command (first column), the observations (second column) specify things to look for or notice. Observing these things will help you cement your understanding of the directory hierarchy and command line environment. 

Go slow and pay attention to the details.  Spaces and capitalization are important!  If you get lost, ask for help.

Command <img width="600px"> | Observations
--------|--------------
``` LS ``` | case sensitivity is extremely important in CLIs.  If you get a "command not found" errors, check your capitalization and spacing
```pwd``` | print working (current) directory.  Notice the output: ```/home/cabox/workspace```.  This is your current location in the hierarchy.  codeanywhere has automatically created a directory called ```workspace```.  Sub-directories that you create will show in the graphical hierarchy in the left hand sidebar.
```ls``` | list the contents of the directory.  Notice the lack of output.  There are no files/directories in this directory.
```ls /``` | list the contents of the root directory.  Notice the output.
-----------------|------------------------------------------------
```mkdir mydir``` | create a subdirectory for this activity
```cd mydir``` | change into your mydir directory (or, make cms230 the current (working) directory).  Notice how the prompt changed too!
```ls``` | directory should be empty so nothing is printed to the display
```pwd``` | notice the output: ```/home/userID/cms230/lab1/mydir```
-----------------|------------------------------------------------
```touch one.txt``` | this command creates an empty data file named ```one.txt``` in the current directory
```ls``` | Can you see the file you just created?
```touch two.txt``` | same but a file named ```two.txt``` 
```ls -l``` | Notice the different format. The ```-l``` flag makes the ```ls``` command give us more information (ie, the "long format").  Can you figure out which field gives information about the file size?
-----------------|------------------------------------------------
```cd``` | Can you guess the current directory after this command executes?
```pwd``` |Check your guess. Did you guess correctly?
-----------------|------------------------------------------------
```cd /home``` | How did the prompt change? What is the prompt showing you at all times?
```ls /home``` | contains all the home directories for the users of the machine. So what you see depends on machine and authorized users.
```touch myfile.txt``` | This should fail for you. What error did you get? You will not have the proper permissions to write to this directory.
-----------------|------------------------------------------------
```cd``` | Where are you in the directory heirarchy? Check if you need to.
```cd ..``` | Now where are you? Check if you need to. What did the ```..``` do?
```cd ~/cms230/lab1``` | Where are you? What directory does the ```~``` represent?
```cd ~/cms230``` | What happened?  Why?
```cd ../..``` | Where are you? What happened when you used ```..``` twice?



Now let's kick it up a notch.  We're going to add in lots of small details that really make a difference.  Pay close attention to each command (left column) and the observations (right column).  If you get confused, ask me or someone sitting near you.  It's important to not gloss over things you don't understand now as we'll be using these commands all semester.

Command | Observations
--------|--------------
``` cd ~/cms230/ ``` | move into your ```cms230``` for this exercise
``` touch mydir/file1.txt ``` | make an empty file in the ```mydir``` directory
``` ls ``` | list the contents of your ```cms230``` directory
``` ls -l ``` | list, long format.  Notice the output and how it differs from the previous command.  What do you think it means if a line of output starts with a 'd'?
``` ls -L ``` | did you get the same result?
------------------------------------------------------|------------------------------------------------
```mkdir mydir2``` | create another subdirectory for this exercise
```ls``` | you should now see the ```mydir``` and ```mydir2``` directories and files you created earlier during exercise 1
```touch mydir/file3.txt``` | make another file in the `mydir` directory
```touch mydir2/file1.txt``` |
```touch mydir2/file2.txt``` | make some files in the ```mydir2``` directory
```ls -l mydir2``` | what happens when you list a directory?
--------------------------------------------------------------------------------|------------------------------------------------
```mv mydir2/file1.txt mydir2/file3.txt``` |
```ls mydir2``` | Where did ```file1.txt```?
```mv mydir2/file2.txt``` | What happened? What does this error mean?
```mv mydir2/file2.txt .``` | What is the meaning of the ```.``` at the end of the command?
```ls```|
```ls mydir2 ``` | What happened to ```file2.txt```? Why?
```ls . ``` | What is . a shortcut for?
------------------------------------------------------|---------HERE---------------------------------------
```touch temp/file2.txt``` | make another file in the temporary directory.
```ls -l temp``` | What order are the files in?
```ls -lt temp``` | What order are the files in now? What does the -t flag do?
```ls -lrt temp``` | What order are the files in now? What does the -r flag do?
------------------------------------------------------|------------------------------------------------
```cp temp/file1.txt boo.txt```|
```ls``` | Where did you copy the file to? Why?
```cp temp/file1.txt exercise2``` |
```ls temp``` |
```ls exercise2``` | What happened? Why?
```cp temp/file1.txt exercise2/file4.txt```|
```ls -l exercise2``` | What file(s) are in the directory ```exercise2```?
------------------------------------------------------|------------------------------------------------
```rm temp/File1.txt``` | What does the error tell you?
```rm temp/file1.txt``` |
```rm temp/file2.txt``` |
```rm temp/file3.txt``` |
```ls temp```| What is in the temp directory now?
```rmdir temp``` |
```ls temp``` | directory should be gone
```rm file2.txt``` | remove the file from this (current) directory
```rm boo.txt``` | remove file from this (current) directory
------------------------------------------------------|------------------------------------------------
```rmdir exercise2``` | What happened? What can you infer about the rmdir command?
```mv exercise2 exer2``` |
```ls``` | What is the effect of ```mv``` when invoked on a directory?
```ls exer2``` |  Note the files still in ```exer2```
```rm exer2/*.txt``` | cleanup ```exer2``` directory
```ls exer2``` | What happened in the previous step?  What was the effect of using ```*.txt```?
```rmdir exer2``` | finish cleanup

### Part II - Mimir

At this point, you'll do a short exercise using Mimir.  This exercise is designed to be like C homework assignments in miniature.  This is the procedure you'll follow for all the C homework assignments this semester.  This exercise will show you how to: 

   - create and edit a source code file on Mimir
   - compile and run your program on Mimir
   - submit your work which triggers a set of testcases on Mimir
   - interpret the output of the testcases
   - locate and interpret instructor feedback in Mimir (after the lab is completed)


1. Begin by opening the IDE in Mimir if you haven't already.  At the prompt, use `cd`, `pwd`, and/or `ls` to determine your location and navigate to the `lab1` directory.
2. Create a new file: `touch lab1.c`  If you open the appropriate folders on the left-hand file browser tree, you should see `lab1.c` in your `~/cms230f19/lab1` folder.  (You may have to right click and choose refresh on the file viewer tree before it appears.)  You can then click on this file to open it in a pane for editing.  You should now have two tabs open: one with your empty `lab1.c` file and one with your terminal.
3. Your goal is to write a function named `sumTo` which takes an `int` as an argument and returns an `int`.  This code should sum up all the even numbers between 0 and the argument (not including the value of the argument itself).  So a call to `sumTo(10)` would add up 2, 4, 6, and 8 and return the value 20.  `sumTo(9)` would return the same value of 20 using the same logic.  Add the following code to your `lab1.c` file.  (If you're reading the code you're pasting, you might realize this code is logically incorrect.  Leave it alone for now.)

```
#include <stdio.h>

int sumTo(int n) {
    int sum = 0;
    for(int i = 0; i < n; i++) {
        sum += i
    }
    return sum;
}


int main(void) {
    printf("%d\n", sumTo(9));
}

```

3. Save your source code and change to your terminal window. Compile your source code by typing: 

`gcc -Wall -Werror -o lab1 lab1.c`

You should see an error which looks something like:

   ```
user@mimir: ~/cms230f19/lab1 > gcc -Wall -Werror -o lab1 lab1.c
lab1.c: In function ‘sumTo’:
lab1.c:6:17: error: expected ‘;’ before ‘}’ token
         sum += i
                 ^
                 ;
     }
     ~            
user@mimir: ~/cms230f19/lab1 > 
   ```

This syntax error is easy to diagnose, but note that the C compiler tells you what line the error occurs on:

   `lab1.c:6:17: error: expected ‘;’ before ‘}’ token`.  

The first number in that output line, 6, is the line you need to fix in `lab1.c`.  The second number, 17, relates to something else.  Go ahead and fix the error and recompile.  *Protip: You can easily recall your previous compiler command by pushing the up arrow.  This will scroll through your previous commands.  When you find the one you want to execute, simply press [Enter] to execute the command again.*

4. When all the syntax errors are gone (leave the logical errors alone for now!), run your program using the command: `./lab1`  "Great," you think, "My program runs and is obviously correct. I think I'm ready to turn in my work."

5. When you submit your code, Mimir will run your code against some testcases that I write.  This is a hallmark of *test driven development* which is common in industry.  You (as a developer) write code, but that code must pass testcases written by other departments (often QA or Testing) before it can be incorporated into the larger code base.

Click the green Submit button at the top your Mimir window.  Choose the assignment you wish to submit your work to (in this case "Lab1").  Then select the `lab1.c` file to submit.  You should see a popup which says "Submission Successful" and an option to view your submission.  Click View.  You'll then be taken to a window which shows your submission and the results of the testcase run. In this case, your file should **FAIL** the testcases (shown in red on the right hand side of the window).  Click on the name of a failing testcase (say, `sumTo(10)`) to receive more information.

When you look at the output of a failing testcase, there are two crucial pieces of information.  

In the "testcase input" box, you should see:

```
int num = sumTo(10);
munit_assert_int(num, ==, 20);
```

This is the actual code I wrote for the testcase.  You can see that I call the function you wrote (`sumTo`), store the returned value in a variable (`num`) and then feed that value into the `munit_assert_int` function.  This function tests to see if a comparison holds true or not.  In this case, it checks whether the result of your function (stored in `num`) is equal to (the operator that is the middle argument) to the value 20 (the correct answer).  A one-line way to write this testcase would be:

```
munit_assert_int(sumTo(10), ==, 20);
```

Further down in the testcase window, you'll see the "Your code's output" box.  You should see something like:
```
Running test suite with seed 0x6c01edcb...
mimir/test                           
-----------
[ ERROR ]
Error: c_unit_test:2: assertion failed: num == 20 (55 == 20)
Error: child killed by signal 6 (Aborted)
0 of 1 (0%) tests successful, 0 (0%) test skipped.
```

This set of output shows what your code returned instead of the correct answer.  In particular, the line `Error: c_unit_test:2: assertion failed: num == 20 (55 == 20)` is very useful.  This says that your code returned 55 instead of 20.
 
Close the submission tab and head back to the IDE and fix the logical error.  You can change the code in `main` to help you debug and make sure your code is working correctly.  These testcases don't test the output of your program; they test what your function returns.  Once you have compiled and tested your code in the IDE, resubmit to Mimir and check the testcases.  Continue this cycle until all the `sumTo` testcases pass.

6.  So what's this "Code formatting" testcase about?  You should currently have 3/4 testcases passing.  These are the ones that test the logic you've implemented; Based on the specifications, does your code spit out the correct answer?  However, there's more to writing good code than just logic. The code formatting checks on Mimir help you check if your code is well formatted.  What does "well formatted" mean and who says so?  Well, in this case, Google says so.  We're using a tool called `cpplint` which Google developed to make sure their developers adhered their prefered [style guidelines](https://google.github.io/styleguide/cppguide.html) - certain standards when writing code.  The tool isn't perfect, but let's look at a few things that industry considers to be "well formatted" code:
   * Lines no longer than 80 characters.  The reasons for this go back to the days of teletype machines as output devices but the principle still holds: long lines are hard to read.
   * Spacing is important.  This means indentation is standardized, there aren't lots of blank lines in your code, and so forth.  There are other rules you may not have seen before, such as "use spaces instead of tabs".  These most often get violated when you copy and paste code from something such as a lab writeup.  Rules such as these ensure your code looks the same regardless of which editor a programmer uses to view it.  Spacing around things like parentheses and braces also enhances overall readability.
   * camelCase vs. snake_case for function and variable names.  This is left to the programmer's discretion.  Most C programmers today use snake_case - that is, an underscore between words when they name variables and functions.  However, it's not as rigorous as the Java community which has settled exclusively on camelCase - that is, lowercase first word with subsequent words capitalized.  For this class, I don't care which style you use as long as you are consistent.  Don't mix and match styles in a single project.  You can either:
      - Use snake_case for everything: file_names, function_names, and variable_names.
      - Use Java conventions: initial letter of all words capitalized in FileNames.  Then camelCase for function and variableNames.
   * While not enforced by the tool, you are also expected to comment your code.  Remember that comments are at a high level and **DO NOT** restate the code.  They should explain the purpose of the function or chunk of code.  At a minimum, you should comment every function, just before the function signature and state 1) what inputs (arguments) are needed and what they represent; 2) what output or return value is generated by the function and 3) the overall purpose of a function.  Below is an example of an acceptable comment for this lab's function:
   ```
   //function returns an int derived by adding all numbers between 0 and the int argument supplied.  Returns 0 if arg is <= 0.
   ```
Copy this comment into your `lab1.c` file above the function `sumTo`.  Go ahead and submit.  What have you learned about the style guidelines for comments?

Modify the style of your code until it is passing all the testcases.  Then you're finished with this lab!


A few notes about grading:
* The Mimir testcases are NOT guaranteed to cover all possible scenarios.  In some cases, they deliberately won't.  It is always your job to read the specifications contained in an assignment and make sure your code meets those specifications.  The testcases are there to help point you in the correct way, but you should never abdicate the responsibility of writing correct code.
* It is always my intention to allow you to make unlimited submissions to Mimir.  If a project isn't setup that way and you get cut off after only a few submissions, let me know so I can fix that problem.
* I always grade the last thing you submit.  Therefore, make sure your last submission has comments, is indented correctly, and generally follows good coding conventions even if it doesn't pass all the testcases.
