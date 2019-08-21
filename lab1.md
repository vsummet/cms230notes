# Lab 1: Linux and git Basics

### Goals

This lab will let you working in Linux and using Command Line Interfaces (CLIs). 
Along the way, you'll get some practice with several important Linux sysadmin concepts, including

  - experience with the fundamental Linux commands
  - understanding of directory hierarchies and file system organization
  - understanding of relative and absolute paths
  - understanding of git repos and organization
  - experience with basic git commands


### Pre-lab prep
Let's get the boring lecture out of the way before lab, so you can spend this entire lab period 
playing around with the basics of the Linux CLI and git.  To begin, watch these videos (in order or they won't make sense).  All of them are on YouTube and range from 7-10 minutes each and total about 1 hour and 15 minutes.

1. [Command Line Interfaces](https://www.youtube.com/watch?v=3WddgzyhHk8)
2. [Directory Hierarchies](https://www.youtube.com/watch?v=MdMCWKpWbjc)
3. [Basic Linux Commands](https://www.youtube.com/watch?v=wNB72BaH6rA)
4. [Paths and Special Directories](https://www.youtube.com/watch?v=RPviGYRAdgU)
5. [Relative and Absolute Paths](https://www.youtube.com/watch?v=sqX6hu7oEew)
6. [Command Flags](https://www.youtube.com/watch?v=fU6BDYVE2og)
7. [Creating and Deleting Directories](https://www.youtube.com/watch?v=AVzqquRi_-g)
8. [Copying Files](https://www.youtube.com/watch?v=MYe58LbbfVU)
9. [Moving/renaming Files and Directories](https://www.youtube.com/watch?v=GKEGNdNIQrw)
10. [git Basics](https://www.youtube.com/watch?v=uR6G2v_WsRA) (only the first 6:35)

You may also want to refer to [Notes on Linux and the Terminal Environment](https://github.com/vsummet/IntroductionToComputerSystems/blob/master/Notes/01b-Linux_and_the_Shell.md) which you already read during the first week of class.

### Lab Activities
0. All the following steps assume you've already created your accounts and the connection as specified in the software setup discussed on the first day of class.  If you haven't done this, you need to follow the instructions on the software setup page before beginning.  See the link on the class calendar.
1. Log into mimir.  You should see a project named Lab1; click on it. Open this project in the Mimir IDE (button on the right hand side). You will probably see two windows.  One of these is for writing your source code and one of them will be a terminal as you've seen me use during class.  You can close the source code window for now.  You won't need it until part 2 of the lab.
2.  Now work through the following commands, one at a time, at the prompt. After each command (first column), the observations (second column) specify things to look for or notice. Observing these things will help you cement your understanding of the directory hierarchy and command line environment. 

Command | Observations
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



3. Now let's kick it up a notch.  We're going to add in lots of small details that really make a difference.  Pay close attention to each command (left column) and the observations (right column).  If you get confused, ask me or someone sitting near you.  It's important to not gloss over things you don't understand now as we'll be using these commands all semester.

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

4. Switching Gears - At this point, you'll do a very short exercise using git.  This exercise is designed to be like homework assignments in miniature.  This is the procedure you'll follow for all (most?) homework assignments this semester.  This exercise will show you how to: 

   - accept an assignment which will create a repo on GitHub.com with some starter code
   - clone that repo to Mimir
   - edit a file on Mimir
   - compile and run your program on Mimir
   - run testcases on Mimir to check your work
   - stage your changes and commit them to your local repo
   - push your changes back to github and submit your work

5. git Exercise

   0. Begin by navigating to your ```cms230``` directory on Mimir. 
   1. Open a web browser, visit Canvas, and find the Lab1 announcement.  This announcement has a link in it.  Click on it.  You may have to grant the CMS230 organization permissions as this is the first time you've accepted the assignment.  You'll get a message that GitHub is setting up your repo.  Once that message is finished, your repo full of "starter code" for this lab has been created on GitHub.  But we've got to get that code over to codeanywhere!
   2. In your GitHub window, find the big green button which says "Clone or download".  Click it and copy the link.
   3. Switch tabs in your web browser to codeanywhere.  Make sure you're in your ```/workspace/cms230``` directory.  In this directory type the command ```git clone link-to-repo-you-just-copied-in-the-previous-step```  Note: Typing Ctl-V to paste **will not work**.  You will need to right-click and select Paste or use Shift-Ctl-V. You may have to enter your GitHub user name and password, depending on how you set up your codeanywhere account.  If you need to enter your password, *you will not see the password being typed*.  
   4. You will see a confirmation message as the repo is successfully cloned.  Type ```ls``` at the prompt, and you will see a directory that is a combination of the assignment name and your GitHub userid.  Move into that directory (```cd directory-name```) and type ```ls``` again.  You should see a file named ```Lab0.c``` which is the starter code I've provided for this lab. 
   5. There is a small bug (feature?) in codeanywhere.  In order to be able to see your newly created directories and files in the graphical file browser (left hand sidebar), you'll need to refresh by right clicking on the Fall2018 connection and selecting Refresh.
   6.  In the graphical file browser, navigate (by using your mouse and clicking, isn't that easy?!) to the Lab0.c file.  Click on it.  It will open in a tab.  You should now have two tabs open: "Fall2018" (the command line interface connection to the Linux computer) and "Lab0.c" (your C program ready for editing).
   5.  Switch to the CLI tab and make sure you're in the directory for your repo.  At a prompt, compile the code by typing ```gcc -Wall -Werror Lab0.c```
   6. You will see an error.  (Actually, it's a warning, but we're forcing gcc to treat warnings like errors.)  See if you can figure out how to fix the error.  Save your work and recompile (use the up arrow to repeat the previous command!). 
   6. Remember that an absence of errors means success!  At the prompt, list the contents of the directory.  You should see a file named ```a.out```.  This is the compiled executable.  Execute it by typing ```./a.out```.  You should see the output ```Hello CMS230```.  
   7.  Switch to your editor tab containing Lab0.c.  Modify the .c file to print out your name on a new line after the "Hello" greeting.  Save your changes. Switch back to the CLI tab, compile, and execute your program.  If you get any errors at the compilation stage, fix them!
   8.  Yay!  You've completed your assignment.  Now you need to get your changes back to GitHub so that I can grade your work.  You will need to do 3 things to make this happen: add the (changed) file to your local repo, commit the changes to your local repo, push your local repo to your remote repo (on GitHub) so they are in sync.

      - Type the command ```git add .```  This stages all the changed files in the current directory/repo.
      - Type the command ```git commit -m "message here"```.  You should change the message between the quotes to indicate how your code has changed since your last commit.  For this assignment, an appropriate message might be: "Added code to print my name".
      -  ```git push origin master```.  This command pushes (copies/syncs) your local repo to GitHub.  Your work is **NOT** submitted until this step successfully finishes.
   
   That's all you need to do to submit your work.  I will have access to your repo and can check/download your work to grade it if I need to.  GitHub automatically timestamps files, and I use this timestamp to verify deadlines.

   ### A Few Notes About Good git Practices
   - In general, you should have many commits for a homework.  A rule of thumb is to commit once you have a small "logical chunk" working.  In practice, this might mean committing whenever you finish a function or other "chunk" of code.  Remember that by committing and pushing your work, you're creating a backup of your code.  If codeanywhere were to disappear tomorrow (please, no), your code would still be on GitHub and you could be up and working on it again as soon as you found a computer with git and other software installed.
   - In this class, we will not be working in teams.  In the real world working in teams requires the use of git branching.  We won't be covering branching in this course.
   - While you can change files at GitHub.com via a web browser, I don't recommend this.  It is easy to create conflicts (code versions which cannot be combined) between your local repo and the repo on GitHub.  This takes some effort to sort out and can become ugly.  It's easier not to do it in the first place.
