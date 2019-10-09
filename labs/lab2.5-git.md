# Lab 2.5: git Basics

### Goals

This lab will show you how to use `git`, a professional version control system to submit your work
on the Raspberry Pi.  
Along the way, you'll get some more practice with the Linux command line environment.

### Pre-lab prep
Before you start the lab, watch this video:
* [git Basics](https://www.youtube.com/watch?v=uR6G2v_WsRA) (only the first 6:35)


### Lab Activities
All the following steps assume you've already created your accounts and the connection as specified in the software setup discussed on the first day of class.  If you haven't done this, you need to follow the instructions on the software setup page before beginning.  See the link on the class calendar.

Since we're now working on the Raspberry Pi, developing code is a bit more primitive.  You no longer have access to an online IDE like Mimir or Codio.  This means that you'll be working entirely in a command line environment.

Review the following Linux commands, and make sure you understand them:
  a. `ls` (to see what files are in your current working directory)
  b. `cd` (to change directories and navigate the directory heirarchy)
  c. `pwd` (to see where you are in the directory heirarchy)
  d. `touch` (to create empty files)
  e. `nano` (to edit files)
  f. `mv` (to both move and rename files)

At this point, you'll do a very short exercise using git.  This exercise is designed to be like homework assignments in miniature using the Raspberry Pi.  This is the procedure you'll follow for all the assembly language homework assignments this semester.  Because these must be completed on the Raspberry Pi, you don't have the option to use other IDE's or environments.  This exercise will show you how to: 

   - accept an assignment which will create a repo on GitHub.com with some starter code
   - clone that repo to your Raspberry Pi
   - edit a file on the Raspberry Pi
   - compile and run your program on the Raspberry Pi
   - run testcases to check your work
   - stage your changes and commit them to your local repo
   - push your changes back to github (and thus submit your work)

To begin, make sure you're logged into github.com and your Raspberry Pi.  Also make sure your Raspberry Pi is connected to the internet.


git Exercise

1. Begin by creating a cms230 directory on your Raspberry Pi:
   ```
   cd
   mkdir cms230
   ```
2. Open a web browser on your laptop, visit Canvas, and find the Lab2.5 assignment.  This assignment has a link to GitHub in it.  Click on it.  You may have to grant the Rollins-CMS organization permissions as this is the first time you've accepted the assignment.  You'll get a message that GitHub is setting up your repo.  Once that message is finished, your repo full of "starter code" for this lab has been created on GitHub.  You can look at the code on GitHub, but you can't compile it or test it.  So we've got to get that code over to your Raspberry Pi!
3. In your GitHub window, find the big green button which says "Clone or download".  Click it and copy the link.
4. Now go to your Putty/Terminal window on your laptop.  Make sure you're in the `cms230` directory you just created.  In this directory type the command ```git clone link-to-repo-you-just-copied-in-the-previous-step```  Note: Typing Ctl-V to paste **will probably not work**.  You will need to right-click. This command tells your Raspberry Pi to make a connection to a specific repo on GitHub and copy that code.  It will prompt you to enter your github user id and password. As you enter your password, *you will not see the password being typed*.  
5. You will see a confirmation message as the repo is successfully cloned.  Type ```ls``` at the prompt, and you will see a directory that is a combination of the assignment name and your GitHub userid.  Move into that directory (```cd directory-name```) and type ```ls``` again.  You should see a file named ```lab.s``` which is the starter assembly code I've provided for this lab. 
6.  At this point you may want to open another Putty/Terminal and establish a 2nd connection to your Raspberry Pi.  I find it easiest to have two windows open when working in a non-graphical environmrnt.  I open `nano` in one window and leave it open, remembering to save after I make changes to my source code, of course!  Then I compile and analyze the errors in the other window.  To me, this is easier than constantly closing and re-opening `nano`, but you do you.  
7. Open the file in nano: `nano lab.s`.  The code will look strange because we haven't done any work with assembly programming yet.  However, the mechanics of compiling assembly on a Raspberry Pi are very similar to C.  Close nano (by typing Ctl-o).  At a prompt, compile the code by typing ```gcc -Wall -Werror lab.s```
7. You will see an error.  (Actually, it's a warning, but we're forcing gcc to treat warnings like errors.)  Fix the error by XXXX.  Save your work and recompile (use the up arrow to repeat the previous command!). 
8. Remember that an absence of errors means success!  At the prompt, test the output of your program by typing: XXXX.

9.  Yay!  You've completed your assignment.  Now you need to get your changes back to GitHub so that I can grade your work.  You will need to do 3 things to make this happen: add the (changed) file to your local repo, commit the changes to your local repo, push your local repo to your remote repo (on GitHub) so they are in sync.  From your assignment directory:
      - Type the command ```git add .```  This stages all the changed files in the current directory/repo.
      - Type the command ```git commit -m "message here"```.  You should change the message between the quotes to indicate how your code has changed since your last commit.  For this assignment, an appropriate message might be: "Fixed error in previous version".
      -  ```git push origin master```.  This command pushes (copies/syncs) your local repo to GitHub.  Your work is **NOT** submitted until this step successfully finishes.
   
   That's all you need to do to submit your work.  I will have access to your repo and can check/download your work to grade it if I need to.  GitHub automatically timestamps files, and I use this timestamp to verify deadlines.

   ### A Few Notes About Good git Practices
   - In general, you should have many commits for a homework.  A rule of thumb is to commit once you have a small "logical chunk" working.  In practice, this might mean committing whenever you finish a problem or other "chunk" of code.  Remember that by committing and pushing your work, you're creating a backup of your code.  If your Raspberry Pi were to disappear tomorrow (please, no), your code would still be on GitHub and you could be up and working on it again as soon as you found a computer with git and other software installed.
   - In this class, we will not be working in teams.  In the real world working in teams requires the use of git branching.  We won't be covering branching in this course, but you will continue to use git/GitHub in future courses.
   - While you can change files at GitHub.com via a web browser, I don't recommend this.  It is easy to create conflicts (code versions which cannot be combined) between your local repo and the repo on GitHub.  This takes some effort to sort out and can become ugly.  It's easier not to do it in the first place.
