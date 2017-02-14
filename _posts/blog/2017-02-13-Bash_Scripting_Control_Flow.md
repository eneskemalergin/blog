---
layout: post
title: Bash Scripting: Control Flow
excerpt:
categories: blog
tags: ["Bash", "Terminal"]
published: true
comments: true
share: true
---

Hello all, this is the second part of my bash shell scripting tutorial. In this part we will go from where we left of and work on control flow statements on BASH scripting.

Control statements are one of the most fundamental concepts in computer science, since they allow us to select from different options and make more accurate decisions by given them true/false resulting statements. In this blog post we will see the exit statuses, logical expressions, File test, string tests, arithmetic test, if-else statements, and case statements in bash scripting.

![](http://1.bp.blogspot.com/-QE9dDUpFECc/UAyAWZx1p7I/AAAAAAAAAE8/OXBntps8LAA/s1600/blank_computer_screen.png)

## 1. Exit Statuses
Integer that returns after the execution of a program is called an *exit status or exit code*.

Depending on its value, we can see if the program terminated successfully or not. If returns 0 that means program run without any error, however any value above 1 is it terminated unsuccessfully.

---

To find the last exit status, simply use the ```$?``` variable. Be cautious in that if you run echo ```$?``` twice in a row, the second command will always return a 0.



```BASH
$ rm /; echo $?
```

    rm: /: is a directory
    1



```BASH
$ ls -l; echo $?
```

    total 7128
    -rw-r--r--  1 eneskemalergin  staff    25297 Feb 13 12:40 Bash_Shell_Scripting_Tutorial_1.ipynb
    -rw-r--r--  1 eneskemalergin  staff     1945 Feb 13 14:47 Bash_Shell_Scripting_Tutorial_2.ipynb
    -rw-r--r--  1 eneskemalergin  staff     7627 Feb 13 12:40 Basic_NeuralNets.ipynb
    -rw-r--r--  1 eneskemalergin  staff    51397 Feb 13 12:40 Basic_Sequence_Analysis.ipynb
    -rw-r--r--  1 eneskemalergin  staff    81298 Feb 13 12:40 Biology_with_Python.ipynb
    -rw-r--r--  1 eneskemalergin  staff   153869 Feb 13 12:40 GenerativeAdversarialNetworks.ipynb
    -rw-r--r--  1 eneskemalergin  staff   145740 Feb 13 12:40 Inferential_Statistics.ipynb
    0



```BASH
# Running 'echo $?' twice always produces a succes
$ echo $?
```

    0


We can see the list of POSIX exit statuses here:

- __0__: Success
- __> 0__: Failure due to redirection or word wxpression
- __1-125__: Unsuccessful (for the most part, depends on the command)
- __126__: File not executable
- __127__: Command not found
- __128__: Unspecified, but failure.
- __>128__: Command failed due to receiving a signal.


To terminate your script with a specific exit code, use the ```exit``` code, followed by an integer.


```BASH
    if [ ! -e $SAMP_FILE ]; then
        exit 32
    fi
```

We'll learn ```if``` statements real soon, but this snippet simply checks if the file does not exist.

In some cases, a program can exit with a value other than ```0```, and still be considered a successful run.

For example, the ```grep``` command returns a ```0``` if a matching pattern is found, and a ```1``` if no matching pattern is found. A value of ```2``` or greater is reported for real errors.


## 2. Logical Expressions

We use the ```[]``` brackets to evaluate logical expressiong. They are not syntax but a shortcut for the ```test``` command.

The ```test``` command takes in some evaluation and (depending on the result of the statement) returns some exit code.

### Unary and Boolean Operators
Let's first look at the unary and boolean operators before we learn about specific tests.

#### Inverting a test
To invert a test, place an exclamation mark as the first argument of the ```[``` command (remember it's not syntax!). For example, the -e operator checks for a file's existence.

```BASH
# Test if file 1 does not exist
[ ! -e file1 ]
```

#### Boolean Operators
The boolean operators AND and OR can be modeled with the ```-a``` and ```-o``` flags.

```BASH
# Test if both file1 and file2 exists
[ -e file1 -a file2 ]
```

Let's look at some examples to see what some logical expressions evaluate to.

Since ```test``` call does not explicitly return what it's exit code is, we need to use the ```$?``` command to retrieve the last exit code.

Remember that using the ```test``` command is the same as using brackets.

```BASH
$ test 'hi' = 'hello'; echo $?
1
$ [ 'hi' = 'hello' ]; echo $?
1
$ test 'hi' != 'hello'; echo $?
0
$ [ 'hi' != 'hello' ]; echo $?
0
$ [ 'hi' === 'hello' ]; echo $?
# === is not a real option, so returns an exit code of 2
-bash: test: ===: binary operator expected
2
```

Notice that if an evaluation is true, it returns a 0, but if false, it returns a 1. Any errors result in an error code of 2.

You can see a list of all test options with the ```man test``` command, but we'll go through them step by step over the following lessons.


> **CAREFUL!!**

> **Spacing is important in bash scripting**

> Be sure to space out your operators properly - the Command Line is particular picky about this! Joining arguments together (```1=3``` instead of ```1 = 3```) can mean errors all over the place, so be cautious!

### Handling more than one test with ```&&``` and ```||```

If we have more than one command, we can bring them together logically with the && operator or || operators. The evaluation of these boolean operators depend on the exit statuses of the commands.

The shell is designed to be efficient, and so wastes no time running needless commands. For example, if two commands - ```command1``` and ```command2``` are joined with an && operator, and ```command1``` returns an exit status other than 0, ```command2``` is not run.

```BASH
command1 && command2
```

Similarly, in the case two commands are joined by a || operator, ```command2``` won't be run if ```command1``` already has an exit status of 0.

```BASH
command1 || command2  
```

We can use these two properties above to create a simple but efficient if/else-like statement.

```BASH
command1 && command2 || command3
```

the ```command1``` is first executed, then ```command2``` is also executed if ```command1``` has an exit status of 0. Otherwise, ```command3``` is run.

Hopefully these evaluations make sense - let's now move onto the different types of tests (file, string and arithemetic) which give much more flexibility to control flow.

## 3. File Tests
With file tests, we can check simple properties of file attributes. The file tests that require just one argument are called unary operators.

### Existence
There are two simple tests to see if a file exists and if it's empty.

- **```-e```**:  File exists
- **```-s```**:  File is not empty

```BASH
$ [ -e testFile.txt ]; echo $?
1
$ touch testFile.txt
$ [ -e testFile.txt ]; echo $?
0
$ [ -s testFile.txt ]; echo $?
1 # File is empty
$ echo "Hello world" > testFile.txt
$ [ -s testFile.txt ]; echo $?
0
```

### Type
The following checks for the file's type. If any of the options below are used on a file that doesn't exist, the exit code returns a nonzero value.

- **```-b```**: Block device
- **```-c```**: Character device
- **```-d```**: Directory
- **```-f```**: Regular file
- **```-L```**: Symbolic link
- **```-O```**: Group matches the effective group id of this process
- **```-p```**: Named pipe
- **```-s```**: Socket

```BASH
$ [ -d Downloads ]; echo $?
0
$ touch testFile.txt
$ [ -f testFile.txt ]; echo $?
0
```

### Permissions
We may also check the permissions settings of a file.

- **```-r```**: Readable
- **```-w```**: Writable
- **```-x```**: Executable
- **```-u```**: uid has been set
- **```-g```**: gid has been set
- **```-k```**: Sticky bit is set

```BASH
$ touch testFile.txt
$ ls -l testFile.txt
-rw-r--r--  1 johnPC  staff  0 Jul  3 11:02 testFile.txt
$ [ -r testFile.txt ]; echo $?
0
$ [ -w testFile.txt ]; echo $?
0
$ [ -x testFile.txt ]; echo $?
1
$ chmod a+x testFile.txt
$ [ -x testFile.txt ]; echo $?
0
```

### Comparisons
Lastly, we have comparison operators, which looks at two files.

```BASH
[ file1 -nt file2 ]
```

- **```-nt```**: file1 is newer than file2
- **```-ot```**: file1 is older than file2
- **```-ef```**: file1 and file2 share inode numbers

```BASH
$ touch oldFile.txt
$ touch newFile.txt
$ [ oldFile.txt -nt newFile.txt ]; echo $?
1
$ [ oldFile.txt -ot newFile.txt ]; echo $?
0
```

## 4. String Tests (=, !=)
String tests can be useful for checking user's input.

### Checking for string equality
To check if two strings are equal or not, simply use the ```=``` or ```!=``` operators.

```BASH
$ [ 'hi' = 'hi' ]; echo $?
0
$ [ 'hello' = 'hi' ]; echo $?
1
```

### Checking if argument is empty or not
Two unary operators are used to check if a string is empty or not.

- **```-z```**: Argument is empty
- **```-n```**: Argument is not empty

```BASH
$ [ -z "" ]; echo $?
0
$ [ -n "" ]; echo $?
1
```

Here's a simple script that reads an input, and depending on the string put in, returns a specific response.

```BASH
#!/bin/bash

printf 'Please enter a word: '

read input

if [ $input = 'hi' ]; then
  printf 'Hi to you too!'
else
  printf 'You input %s.\n' $input
fi
```

We'll go over if-then-else statements soon, but notice how we can use tests and expressions such as these to control logic in our scripts.


## 5. Arithmetic Expansions and Tests

### Arithmetic Expressions
There are two ways we can have the shell evaluate an expression. Either using ```$((expression))``` syntax or the ```expr``` command.

The former does not require proper spacing, while the latter does.

```BASH
$ echo $((2+3))
5
$ expr 2 + 3
5
```
Arithmetic expasion only supports integer values and no decimals.

```
$ expr 2.3 + 2
expr: not a decimal number: '2.3'
```


### Operators
Here are a list of arithmetic operators.

- **```++ --```**:  Increment, Decrement
- **```+ -```**: Unary plus and minus
- **```* / %```**: Multiplication, division and remainder
- **```== !=```**: Equal and not equal
- **```! && ||```**: Logical negation, AND, and OR
- **```<< >>```**: Bit-shift left and right
- **```~ & ^ |```**: Bitwise negation, AND, exclusive OR, and OR
- **```\= += -= *= /= %=```**:  Assignment operators
- **```&= ^- <<= >>= |=```**:  Bitwise assignment operators

### Arithmetic Test
It's important to avoid using the ```=``` symbol when comparing numerals. The ```=``` looks for string equality, not numeric equality. Thus, when working with arithmetic equations, be sure to use ```-eq``` instead.

```BASH
$ [ 1 = 1 ]; echo $?
0
$ [ 092 = 92 ]; echo $?
1
$ [ 092 -eq 92 ]; echo $?
0
```
Here is a list of more comparison tests we can use to compare two numbers. Be sure to not use canonical notations such as > or <!

- **```-eq```**: Equal to
- **```-ne```**: Not equal to
- **```-lt```**: Less than
- **```-gt```**: Greater than
- **```-le```**: Less than or equal to
- **```-ge```**: Greater than or equal to

```BASH
$ [ 92 > 32 ]; echo $?
0      # Looks good...(but wrong)
$ [ 92 < 32 ]; echo $?
0      # Wrong
$ [ 92 -gt 32 ]; echo $?
0      # There we go!
```

## 6. If-else Statements
Just like any other language, the shell provides if-else statements to handle logic flow. However, the syntax is quite different - let's see how.

### No curly braces
Instead of curly braces or indentations to enclose logical constructs, the shell encloses if-statements within its keywords ```if, then, else```, and ```fi```. There is also the ```elif``` keyword that is the shorthand for else-if.

```BASH
if command; then
  # If test condition returns exit status of 0 (success)
elif another command; then
  # Another command is true
else
  # Both commands have exit status not 0
fi
```

Notice anything different from other programming languages? Instead of using some logical expression bound by parentheses, the shell runs commands and checks their exit statuses! This concept may seem foreign and strange at first, but it'll grow on you with practice.

Be sure to get this concept down since it's used in loops as well! It can be confusing since many ```if``` statements use bracket notations ```[]```, which look like syntax.

### Boolean Constructs

When stringing together a group of test commands, use the following syntax:

```BASH
if [ $value -lt 2 ] && [ $value -gt 0 ]; then
  # value is between 0 and 2
fi
```

Let's implement a simple coin tossing game. We'll have the user pick heads or tails, and the shell toss a coin. If the user is correct, then he/she wins; if not, he/she loses.

```BASH
#!/bin/sh

printf "Choose (h)eads or (t)ails: "
read user_choice

# Make sure user chooses between heads or tails
if [ $user_choice != h ] && [ $user_choice != t ]; then
  echo "Invalid choice. Defaulting to (h)eads."
  user_choice=h
fi

# Value of 1 is heads, 2 is tails
computer_choice=$((RANDOM % 2 + 1))

if [ $computer_choice -eq 1 ]; then
  echo "Computer chose heads."
else
  echo "Computer chose tails."
fi

if [ $computer_choice -eq 1 ] && [ $user_choice = h ]; then
  # Correct
  echo "You win!"
elif [ $computer_choice -eq 1 ] && [ $user_choice = t     | ]; then
  # Incorrect
  echo "You lose!"
elif [ $computer_choice -eq 2 ] && [ $user_choice = t ]; then
  # Correct
  echo "You win!"
else
  # Incorrect
  echo "You lose!"
fi
```

## 7. Case Statements
In some cases, a ```case``` statement can be more appropriate. For example, when you have a variable and need to execute lines of code depending on its value, the ```case``` statement makes for clean code.

Case statements do not execute any test commands and therefore do not use exit codes.

Here's a script that outputs a greetings depending on which country a user is from.

```BASH
#!/bin/sh

echo "Please select which country you are from: "

printf "1: Canada
2: Croatia
3: Czech Republic
4: France
5: Germany
6: Greece
7: Italy
8: Netherlands
9: Poland
10: Sweden
11: United States
"

read -p "Country number code: " input

case $input in
  1|11)
    echo 'Hello!'
    ;;
  2)
    echo 'Bog!'
    ;;
  3)
    echo 'Ahoj!'
    ;;
  4)
    echo 'Salut!'
    ;;
  5|8)
    echo 'Hallo!'
    ;;
  6)
    echo 'YAH sahs!'
    ;;
  7)
    echo 'Ciao!'
    ;;
  9)
    echo 'Czesc!'
    ;;
  10)
    echo 'Hej!'
    ;;
  *)
    echo 'Please enter a valid number.'
    ;;
esac
```

Notice the use of the ```|``` operand. We may also use regular expressions if we are trying to match a string!

We may simplify this script with the ```select``` command, which we'll see next.

We can also use case-statements and match input strings with regular expressions!

Let's try to build a script where the user inputs his/her name, and the response changes depending on whether the input starts with a vowel or consonant.

```BASH
#!/bin/sh

printf "What is your first name? "
read first_name

case $first_name in
    [aeiouAEIOU]*)
        echo 'Your name starts with a vowel!'
        ;;
    [0-9]*)
        echo 'Strange that your name would start with a number...'
        ;;
    [a-zA-Z]*)
        echo 'Your name starts with a consonant!'
        ;;
    *)
        echo 'Your name starts with some funky punctuation.'
        ;;
esac
```


```python

```
