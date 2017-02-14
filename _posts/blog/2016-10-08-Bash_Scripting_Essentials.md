---
layout: post
title: Bash Scripting - Essentials
excerpt:
categories: blog
tags: ["Bash", "Bioinformatics", "Terminal"]
published: true
comments: true
share: true
---

Hello everyone, today I am sharing some notes about shell scripting. In this part of the shell/bash scripting I am covering the essentials before getting into more serious topics like conditional statements, loops, and awk/sed tools. I will make a series of blogposts which will cover whole shell scripting so stay tuned...

![imperial.ac.uk](http://www.imperial.ac.uk/ImageCropToolT4/imageTool/uploaded-images/unix--tojpeg_1440498641820_x2.jpg)

Bash scripting, in my opinion is essential tool that bioinformatics scientist must have, because it is a perfect tool to automate other processes like your other scripts on Python or R.

Imagine you are submitting multiple jobs on your server/cluster, however only thing changes in manual submission is the chromosome names, you would simply lose time. Although doing the following will give you more time to spare on other jobs and will give you amazing feeling to see they are going to be submitted, while you are just watching it (It's my personal delight :) )

```Bash
FILES=/n/scratch2/eke2/ENCODE_data/positionIndexes/*

for f in $FILES
do
	FILE_PATH=${f::45}
	FILE_NAME=${f:45}
        #echo $FILE_NAME
	size=${#FILE_NAME}

	if [ "$size" == "23" ]
	then
		NAME=${FILE_NAME::19}
		CHNAME=${NAME:14}
		echo $CHNAME
	else
		NAME=${FILE_NAME::18}
		CHNAME=${NAME:14}
		echo $CHNAME
	fi

	bsub -q short -W 12:00 -R "rusage[mem=20000]" -u eneskemalergin@gmail.com -J "hdf5_$CHNAME Index" -N "python hdf5maker.py hg_19/ full_dnase_genomedata.enes positionIndexes/$FILE_NAME  CHIP_TRAIN/ comp_data_$CHNAME.h5"
	sleep .5
	bsub -q short -W 12:00 -R "rusage[mem=20000]" -u eneskemalergin@gmail.com -J "hdf5_$CHNAME WithoutIndex" -N "python hdf5maker_withoutIndex.py hg_19/ full_dnase_genomedata.enes positionIndexes/$FILE_NAME  CHIP_TRAIN/ comp_data_withoutIndex_$CHNAME.h5"
done
```

PS: (This small script help me to submit all the chromosomes in parallel and using 2 slightly different scripts, producing approx. 600 GB data.)

If you convinced to follow this small tutorial like post, go ahead and catch up with me...

A shell script is a file containing lines of code for the shell to execute.  We can write these scripts in either terminal's editors such as ```vim```, ```nano```, or text editors with syntax highlighters such as atom and sublime text.

But before even we start I would like to mention that we are not going to write huge scripts like typical bioinformatician does with Python/Perl/R. We just need small scripts to increase our speed.

Here is small intro to bash we are printing stuff with ```echo``` command and ```""``` quotation marks:


```python
%%bash
echo "This is what I want to print"
var=2
echo $var
```

    This is what I want to print
    2


Comments in bash are starts with ```#``` symbol like in Python:


```python
%%bash
# This is comment it will not have any effect on output
echo "But this will have effect"
```

    But this will have effect


The first line of a shell script may look like a comment since it starts with a pound symbol ```(#)```, but it's actually a __shebang__. The shebang symbol indicates where to find the program that will be used to execute the script. Thus, the following line of code would indicate that the sh program (default shell executor) should be used to run the shell script, which is found in the ```/bin``` folder.


```python
%%bash
#!bin/sh
# It seems no effect
```

To indicate the running the line is done use ```;``` at the end, however when you directly go to the new line it bash will understand that you went to new line...

How are we going to run the script that we created and named it with ```.sh``` extension? (Not necessarily have to have this extension.)
#### 1. We need to change the permissions to make it executable:

> Assuming that we have small script called printhello.sh


```python
%%bash
# We are setting the permission to executable for specific user
chmod u+x printhello.sh
```

    chmod: cannot access 'printhello.sh': No such file or directory



```python
%%bash
# Checking if changed or not
ls -l printhello.sh
```

    ls: cannot access 'printhello.sh': No such file or directory


#### 2. Executing with ```source``` command

The ```source``` command is used to execute in this example however there are other ways to execute it __with__ a following commands:

- ```source```
- ```./```
- ```bash```
- ```sh```


```python
%%bash
source printhello.sh
```

    bash: line 1: printhello.sh: No such file or directory



```python
%%bash
./printhello.sh
```

    bash: line 1: ./printhello.sh: No such file or directory



```python
%%bash
bash printhello.sh
```

    bash: printhello.sh: No such file or directory



```python
%%bash
sh printhello.sh
```

    sh: 0: Can't open printhello.sh


Executing your scripts __with__ commands are look convenient, I agree! However in the long run when you write bigger scripts which depends on another scripts and having relationship with same packages on your system it is note really going to do the job anymore. I am not just saying that it will not work but most likely it will take a lot more time than executing your scripts __as__ a command.

To be able to make your script command you have to define ```path```s in your system. We can set up paths in 2 ways:

1. Place the script in a directory that's in our ```$PATH``` variable.
2. Add the folder containing our script in the ```$PATH``` variable.

> Recall that the __```$PATH```__ variable contains all the folders the shell looks through when executing a command.

### 1. Adding script to a ```$PATH``` directory

What I want to do is to print my path first which will show me the already added paths to my root:


```python
%%bash
echo $PATH
```

    /home/eneskemal/anaconda2/bin:/usr/local/cuda/bin:/home/eneskemal/bin:/home/eneskemal/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin


In theory we can add our desired scripts to any path that printed with our path, but most used and less error prone folder would be ```/usr/local/path``` default path. Just move your script to the path, then voila!


```python
%%bash
mv printhello.sh /usr/local/bin/
```

    mv: cannot stat 'printhello.sh': No such file or directory



```python
%%bash
# Just run it as a command...
printhello.sh
```

    bash: line 2: printhello.sh: command not found


### 2. Adding containing folder to ```$PATH```

Another way is to add your scripts containing folder and reference folders path into ```~/.bash_profile``` or ```~/.bashrc``` depending on your operating system.

You can add them like this:

```Bash
PATH=$PATH:/path/to/our/scripts
export PATH
```

After you modify the scripts you need to execute the file to actually see the changes.

```Bash
source ~/.bash_profile
```

This was a small part that you hopefully get some beneficial information about how to execute your files.

__Believe me, you will need this writing path for executing scripts, a lot...__

__Variables__ in shell scripting can be tricky sometimes. There are some rules that you need to obey.

Naming conventions:

- Variables must start with a letter ```(a-zA-Z)``` or underscore ```(_)```.
- Variables may then contain any number of letters ```(a-zA-Z)```, digits ```(0-9)``` or underscores ```(_)```.
- There is no limit in characters, but a sensible programmer will make it long enough to be descriptive, and short enough to type out.

Utilization conventions: _(This could be tricky, since it's not very similar to Python or other scripting languages)_

- Use quotes if your variable value contains a space.
When you want the shell to expand your variable, include a ```$``` in front.
Wrap a variable around in quotes unles you have a good reason not to. ```echo "$VAR"```
Wrap variable names around braces ```({})``` to avoid confusion. ```${VAR}```a is certainly different from ```$VARa.```


```python
%%bash
$Test = "Hello World!"
```

    bash: line 1: =: command not found


This will give you syntax error since there are spaces around ```=```. Shell does not like this...


```python
%%bash
test='hello world!'
echo $test
```

    hello world!



```python
%%bash
length=50
echo $length
```

    50


> Remember that when assigning values to variables, a ```$``` sign in unnecessary, but once you want the shell to expand a variable's value, it is.

So now how are we going to manipulate variables:

There are some useful tricks that be must known, such as finding the length of the string. ```${#var_name}``` will do the job


```python
%%bash
string_='eneskemalergin'
echo ${#string_}
```

    14


Making a variable constant, final, or read-only is another useful small trick on manipulating variables. We use ```readonly``` command to achive this constant variable.


```python
%%bash
hello='Hello World!'
echo $hello

readonly hello
hello="Another string"
```

    Hello World!


    bash: line 5: hello: readonly variable


As you can see from the error line it will not overwrite the ```hello``` variable that we define.

Variable that you create, in default will only be useable for the current shell, if you want to inherit the variable to another sub-shell, you should use ```export``` command.



```python
%%bash
keep='This message will be kept'
not_keep='This message will not be kept'
export keep

echo $keep
```

    This message will be kept


When we open up a s sub-shell it will not keep the not_keep, since it is not inheritable...


```python
%%bash
echo $not_keep
```




Another one is to emptying the variables using ```unset``` command. When you ```unset``` a variable you will lose the value.


```python
%%bash
test=45
unset test
echo $test
```




_Positional Parameters_ are used to access the command-line arguments

```Bash
shell_script posParam1 posParam2 posParam3
```

- ```$1``` is posParam1
- ```$0``` is command itself
- ```${10}``` can be used.

Know this will help us to print error messages.

---

### Input Output in Shell Scripting

The ```echo``` command is the easiest way of outputting to a user.


```python
%%bash
echo "easy way to output!"
```

    easy way to output!


Using ```echo``` with option ```-e``` will let us use escape sequences such as; ```\n``` new line, ```\a``` alert.

We can also use ```printf``` to do more fancy stuff. However ```printf``` is forces user to be more specific. As an example of forcing user is that ```printf``` does not include ```\n``` new line as default so you have to include it everytime if you want to go to new line.


```python
%%bash
printf "printing with printf"
printf " don't forget to put new line\n"
```

    printing with printf don't forget to put new line



```python
%%bash
# Like in C, formatting is cool with shell too
printf "Hello my name is %s %s.\n" Enes Kemal
```

    Hello my name is Enes Kemal.



```python
%%bash
printf "I am %d years old" 23
```

    I am 23 years old


```python
%%bash
# When dealing with float numbers decimal precision is 0.6f adds 6 digit to decimal part
printf "The temperature now is %0.1f celcius degre \n" 17.6
```

    The temperature now is 17.6 celcius degre



```python
%%bash
# Also possible to add 0s in front of an integers
printf "I am %04d years old.\n" 13
```

    I am 0013 years old.


If there are fewer stand-ins than variables supplied, then the shell repeats the line until done.



```python
%%bash
printf "I ate some %s.\n" eggs chicken bacon
```

    I ate some eggs.
    I ate some chicken.
    I ate some bacon.


On the other hand, if there are more stand-ins than variables, then the shell simply omits them.


```python
%%bash
printf "I ate some %s, %s and %s.\n" eggs chicken
```

    I ate some eggs, chicken and .


Quoatation marks are not really similar to Python, so it's important to talk about them even a little.

__Single quotes ```''```__:

- Literal values.
- Guarantee shell won't try substitutions.

__Double quotes ```""```__:

- Before running the command, shell looks for variables, globs and other substitutions to perform.
- More flexibility with the shell.
- Executes everything literally except for ```$, \, ! or `.```

__Back quotes ``__:

- Key found on top of left tab key.
- Used to execute commands.


#### Standart I/O redirection

__Standard Input__:

- Used to input data.
- Denoted with a ```<``` symbol.

__Standard Output__:

- Where the normal output goes.
- Denoted with a ```>``` symbol.

__Standard Error__:

- Where all error messages are reported
- Use ```2>```.

__Appending__:

- Attaches second file to bottom of first file.
- Denoted with a ```<<``` symbol.


There are also pipelines, which are used to take the standard output of one command to be used as the standard input of another command. These commands are joined together by a ```|```. (I personally love pipelining)


```python
%%bash
ls | grep .ipynb | wc -w
# This small one-liner gives how many files with .ipynb extension are in current folder
```

    9


To read user input into your shell program using standard in, simply use the ```read``` command.


```python
%%bash
printf 'How are you doing today? '
read user_input
```

    How are you doing today?


- You may use the ```read``` command to read in multiple values at once, separated by a space.
- We may hint at what info the user has to give by using the ```-p``` option.


```python
%%bash
printf 'What are your first and last names? '
read -p "First name: " first_name
read -p "Last name: " last_name
```

```
What are your first and last names?
First name:
Last name:
```

I hope you enjoyed my first part of Bash scripting tutorial.

> Hey do you know there is a comment section below that you can share your ideas with me?

> Until next time, be safe...
