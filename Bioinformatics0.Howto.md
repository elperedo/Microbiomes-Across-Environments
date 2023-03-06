# Bioinformatics I. Basic commands
June 2021

 ###### tags: `MAE`, `basic commands` ---UPDATED June 2021
 
 [TOC]
 
You will find all you need in the MAE-specific tutorial: https://jbpc.mbl.edu//unix-tutorial/MAE2020.html

In this webpage, we will just cover very simple commands and screen. Screen is a program that allows you to continue to run programs even if you close your terminal. Because many of the steps you will compute take hours, it is very handy!


## basic unix commands
[cheatsheet!](https://drive.google.com/file/d/10Jvm8IyezDfp0PWnGIXVZTNhpNevToRc/view?usp=sharing)
https://drive.google.com/file/d/10Jvm8IyezDfp0PWnGIXVZTNhpNevToRc/view?usp=sharing

mv, cp, ls, cd, rm... not familiar?
Still not familiar? 

In the [MAE tutorial](https://jbpc.mbl.edu/unix-tutorial/MAE2020.html#Step_4:_Intro-to-Unix_tutorial) you will find many commands that will be useful in this course. 
https://jbpc.mbl.edu/unix-tutorial/MAE2020.html#Step_4:_Intro-to-Unix_tutorial

Also, you can consult the bioinformatic lab I presentation [here](https://docs.google.com/presentation/d/14LhrA5ODxiwHsLnXhaL9AXO_G5t96mWLHeRwal56t24/edit?usp=sharing)
https://docs.google.com/presentation/d/14LhrA5ODxiwHsLnXhaL9AXO_G5t96mWLHeRwal56t24/edit?usp=sharing

## Very brief recap
Let's open the terminal and type 

```
pwd

```
pwd -> print working directory

you can use this command to check where you are!

```
ls

```
what happened?
This list all the objects in a folder
ls -> list

Now type

```
mkdir newfolder

```

and type

```
ls

```
mkdir -> make a directory 

Now let's navigate to the new directory

```
cd newfolder

```
cd -> change directory

did it work?

let's check it

what would you use to know where are you?


.....

**tip** use the tab on your keyboard!

this will fill up info for you so you don't have to type us much. if two files share a name, it will stop. type a little more and use the tab again. 

:)

**more tips!**
select and use `crt+shift c` to copy the text in the terminal
use `crt+shift v` to paste it into the terminal

## how to make a text file in terminal
type in terminal 

```
cat > fileName.txt

```
now write (or paste) in the terminal

```
 There are microbes everywhere. 
 yes, on your keyboard too! 
 
 :)
 
```
 Press enter and crt +Z
 
 Did it work?
 
 use `ls` 
 is the file there?
 
 Now, is the text in the file?
 
 Let's use head to check it. 
 
 ``` 
 head fileName.txt
 
 ```
 
 :)
 
 
 ## now, let's remove the file
 
 We use `rm`  -> remove to delete files and folder
 
 ```
 rm fileName.txt
 
 ```
 did it work?
 
 how would you check it?
 
 yes, let's use `ls`
  
 now, let's remove the folder
 to navigate back to the previous folder use
  
 `cd ..`

 use `ls` to check the folder objects. Can you see the `newfolder`?

 to remove a folder we will use 

 ```
 rm -fr newfolder

 ```
 The flag `-fr` forces recurrent removal of objects within a folder ( so no need to eliminate all the files inside beforehand)

### listing files before removing (rm)

A very useful thing is to use wildcards. 

For example `*_test.txt will` identify any file finished in `_test.txt`

If you want to remove multiple files you can use the wild card

`rm *_test.txt`

BUT!!
 
Remember that `rm` will remove files **forever**. To check if you have the right list of files replace `rm` with `echo`. It will show you the list of files without removing them.
```
echo *_pass_1.fastq.gz
echo *_pass_2.fastq.gz
echo *_unpaired_*
```

### some tutorials

This is the MAE-specific Unix tutorial. 
Always consult here if you have any doubts. 
https://jbpc.mbl.edu//unix-tutorial/

Others:
http://www.ee.surrey.ac.uk/Teaching/Unix/ 

https://www.doc.ic.ac.uk/~wjk/UnixIntro/ **#this one has exercises**

For the project part of the course, you should be familiar with 

mkdir (creates a directory)
cd navigates to a directory
ls list the folders or files in a directory
rm removes a file
rm -rf removes a directory
mv moves a file

for all these commands,  if you have any doubts about how to use them, type the command + -h or --help . This will list the options for usage. 
You don't need to remember the commands. There are many many tutorials and cheat sheets. 

I like this [one](https://files.fosswire.com/2007/08/fwunixref.pdf) 
https://files.fosswire.com/2007/08/fwunixref.pdf

## screen

This is probably the most important command you will learn today. Read all about the program [here ](https://kb.iu.edu/d/acuy)
https://kb.iu.edu/d/acuy

#### Creating and naming a screen session
```
screen -S sessionID
```
Screen opens a protected window. This is important because many steps you will be running will run for a **really** long type. Using `screen` the processes won't die if you close the terminal or your computer. 
You can give any name to a session (the sessionID would be any name you give e.g. qualitycheck) that is meaningful for identifying the screen session. So, if you open several, you can navigate to the desired one because they can be easily identified. 

#### Deattaching from a screen session

Use `crt+a` followed by `d` to detach the terminal, which means to close the terminal screen window and return to the regular terminal **without** ending the process that is running in the screened session. 

#### Returning to a screen session 

```
screen -r 

```
If there is just one screen session open, this command will reconnect you to it. If several screen windows are open, there will be a list of select the ones of interest 

> [eperedo@minnie taxonomy_databases]$ screen -r
> There are several suitable screens on:
> 	59479.tax	(Detached)
> 	65328.database	(Attached)
> 	45734.testscreen.FRot	(Detached)
> 
to return to a specific session, use the sessionID listed by `screen -r`

```
screen -r sessionID

```

#### Returning to an attached screen session 
If a session appears as Attached when the sessions are listed, use `screen -x sessionID`

```
screen -x 65328.database

```


#### Keeping a log of a screen session
Most times it is useful to record what you type

there are two options. 
1. when you create the session use the flag -L (log)
```
screen -L -S test

```
This is a very easy system that will log #ALL# from beginning to end. It will create a log file "output.0" in the folder where you first launched the screen session. **Only one big caveat: If you open another screen in the same folder it will overwrite your file**

2. generate a file to log in to specific parts of the session
Once in a screened session type `crt+a` release and press `:` a line of text will appear on the bottom of the terminal
Type `logfile NAMEforlog.txt` and press enter (twice)


 If you want to log something, press 
 `crt+a` followed by `H`  in the bottom of the terminal a line saying creating file NAMEforlog.txt will appear, press enter
 
all you type now will be recorded. 
to stop recording type again 
`crt+a` followed by `H`
Recording will stop

**supercool!**
if you use `crt+a` followed by `H` it will append (instead of overwrite!) to the log file. 
To stop, once again  `crt+a` followed by `H`

#### Finishing a screen session
type **exit** to close the screen session. 


#### How to kill a screen session 

Sometimes, it happens. Things go wrong. 
From inside the screen: typing `ctrl+a` followed by `k`
```
screen -X -S sessionID kill
```

kill all screen sessions: 

```
screen -ls | grep '(Detached)' | awk 'sys {screen -S $1 -X quit}'
```




