
# Bioinformatics 0: How to get your computer ready
UPDATED February 2023.

 ###### tags: `MAE`, `terminal`, `filezilla`, `basic commands` ---
[TOC]
## MBL Wireless Network
Find more about how to connect [here](https://jbpc.mbl.edu/unix-tutorial/MAE2020.html#WiFi_Login)
https://jbpc.mbl.edu/unix-tutorial/MAE2020.html#WiFi_Login


There are two wireless networks at the MBL, "MBL-GUEST" and "MBL-REGISTERED."  Life will be easier if you are on the registered network.  
To register your computer choose MBL-REGISTERED from the wireless list and follow the instructions. Your username is your initials followed by the 5-digit number on the side of your MBL ID card. Your password is the same. E.g. if your name is Norman Pace and your card has the number 12345 on the side then your login details are:

username: np12345
password: np12345

You will probably need to restart your computer to complete the process.  If you run into any problems please let us know.

## Software
We will use the software on MBL bioinformatic servers for most of our data processing and analyses.  To interact with the servers you will need:
1. A terminal to connect to the servers
2. A program to transfer files from and to your computer

What is a terminal? Find out [here](https://cs.colby.edu/maxwell/courses/tutorials/terminal/)
https://cs.colby.edu/maxwell/courses/tutorials/terminal/
![](https://i.imgur.com/drx87Fy.png)


What is a file transfer program? Find out [here](https://en.wikipedia.org/wiki/FileZilla) 
https://en.wikipedia.org/wiki/FileZilla

![](https://i.imgur.com/IreN1qr.png)

:::success
How to connect in FileZilla

* Open the new site icon (just under File)
* Select ssh connection
* Port 22
* Fill in the MBL connection data. 
:::

## Install/Activate a terminal
### mac

A full terminal, compatible with unix system is pre-installed. 
You can find detailed instructions for Mac users [here](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac). 
https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac

Useful shortcuts: to **copy and paste inside the terminal** use crt+shift+ c and crt+shift+ v

:::warning
thanks to Liuhao Wu, MAE 2020

As we realized in the class, most Mac users have default zsh terminal shells where * (asterisk) does not work, which causes issues when doing secure copying. The solution here is to switch from zsh shell to the bash shell and we might want to add this note to the tutorials for the future class.

I am attaching the command lines I used to help them figure out below:
* Type chsh -s /bin/bash on your LOCAL machine terminal
* Then the terminal will prompt you to enter your Mac password
* Quit the terminal and reopen that should make it work
* We can also double-check if we're on bash shell now by typing echo $SHELL. If we get /bin/bash​, that means we are on bash shell and we can use * now!
:::

### windows

Windows does not have a native terminal. You need to activate or install it. You can find detailed instructions on how to install an ubuntu terminal in win 10 [here](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/).
https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/

In brief, go here and activate the Windows Subsystems for Linux
![](https://i.imgur.com/oiB3Dq1.png)

Now go to the store and download Linux, I recommend Ubuntu (e.g. 20.04 or 22.04)

Useful shortcuts:

how to find your files (your computer files)

`cd /mnt/c`
That is your C drive. Your files would be under Users, your username. 

How to **copy & paste** in the terminal in ubuntu in windows OS. 
By default, it might be set to use the right button of the mouse to paste after copying. I would recommend setting the terminal to use the same shortcuts the other students would be using.
To do this in an open Ubuntu window click on the upper left corner,  in the terminal app go to Defaults -> Check on Ctrl+Shift+C/V as Copy/Paste -> Click Ok. 


### Linux
If you are running Linux, you are probably pretty familiar with the terminal. If not, check [here](https://askubuntu.com/questions/38162/what-is-a-terminal-and-how-do-i-open-and-use-it).
https://askubuntu.com/questions/38162/what-is-a-terminal-and-how-do-i-open-and-use-it

To **copy and paste inside the terminal** use crt+shift+ c and crt+shift+ v

## secure file transfer 
You can use the scp command in the terminal to transfer files to and from your computer.  This can be fast and efficient, or slow and confusing depending on what you're doing.  
You can find detailed info about transferring in the [MAE unix tutorial](https://jbpc.mbl.edu/unix-tutorial/MAE2020.html#Copying_files_between_your_computer_and_the_server) 
https://jbpc.mbl.edu/unix-tutorial/MAE2020.html#Copying_files_between_your_computer_and_the_server

It's worth installing a graphical interface that will let you move files around the way you're probably used to.  We recommend FileZilla. 

### FileZilla client
Download the appropriate version of the program (**client version**) 

[Win64bit](https://filezilla-project.org/download.php?platform=win64)
[Win32bit](https://filezilla-project.org/download.php?platform=win32)

[MAC OSX](https://filezilla-project.org/download.php?platform=osx)

[linux64](https://filezilla-project.org/download.php?platform=linux64)
[linux32](https://filezilla-project.org/download.php?platform=linux32)

webpage: https://filezilla-project.org/

## text editor (ATOM)
Copying commands from Word or other sophisticated word processors to the terminal leads to all sorts of problems.  You'll want to use a simple text editor.
One nice text editor is Atom, which combines a folder-based interface and text edition capabilities. 


[Windows here](https://flight-manual.atom.io/getting-started/sections/installing-atom/#platform-windows) 

[IOS here](https://flight-manual.atom.io/getting-started/sections/installing-atom/#platform-mac)

[linux here](https://flight-manual.atom.io/getting-started/sections/installing-atom/#platform-linux)


Atom can be seamlessly integrated with the desktop version of [github](https://desktop.github.com/). Scripts and comments from this class can also be found on Github, https://github.com/elperedo/Microbiomes-Across-Environments


## Additional text editors.

### windows 
Windows has [Notepad](https://en.wikipedia.org/wiki/Microsoft_Notepad) 

### mac 
Mac has [text edit](https://support.apple.com/guide/textedit/welcome/mac). Just follow the instructions [here](https://www.techjunkie.com/textedit-plain-text-mode/#:~:text=TextEdit%20opens%20a%20new%20document,in%20the%20TextEdit%20menu%20bar.) to make it plain text so that copying to the terminal goes smoothly.

### Linux
you can use [text edit](www.gedit.org) from gedit. It is a small and lightweight text editor for the GNOME Desktop.


## Documenting your project

It is important to store your code, so that
1. You (or anyone else) can repeat your analysis. 
2. We can help you to troubleshoot any problem that you might encounter.

This is part of your grading for this course. We will guide you through each analysis step, but we want you to document all the steps you took to arrive at your conclusions. 

We **strongly encourage you not to use** Word (.docx) or other sophisticated word processing programs to save your code. These programs embed many additional lines of code that will be misinterpreted by the terminal and the programs you will be using. Even "saving as" a text file may not remove all these symbols.
:::success
We recommend you use a text editor or even websites such as this one, [HackMD](https://hackmd.io/) or [Github](https://github.com/)

:::

# Important. Class server
You will find all you need in the MAE-specific tutorial: https://jbpc.mbl.edu//unix-tutorial/MAE2020.html


### Connect to the MBL BPC computing server

You will be connected to the class server. Each of you will be assigned a host [class.XX] and a password. The main purpose of each of you running in a different host is to prevent competing for computing power. 

Open the terminal and type 

```

ssh [username]@class.mbl.edu

ssh [username]@class.[XX]
password: type here

```
![](https://i.imgur.com/Fw6eXJE.png)


There are other ways of connecting, see here for more detail: https://jbpc.mbl.edu/unix-tutorial/MAE2020.html#Step_2:_Getting_Connected_Using_SSH





