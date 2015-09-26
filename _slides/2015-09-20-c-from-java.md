---
title: C from Java
description: >
  C's syntax is dangerously similar to Java's, making it difficult to work with
  if you haven't spent much time learning about their differences.  This talk
  aims to bridge the gap for students taking CWRU's EECS 338.
layout: presentation
theme: night
---

{{site.startslide}}

# C from Java

Openhacks 9/20/2015

Stephen Brennan

{{site.endslide}}
{{site.startvertical}}
{{site.startslide}}

## First things first

{{site.nextslide}}

It's not safe to compile C without a Makefile!

Take [this](https://github.com/brenns10/last-makefile)!

It's Tekin-approved!  You can safely use it on your homework.

{{site.nextslide}}

## Why?

It automagically detects dependencies, so you don't have to edit your makefile
each time you add a `.c` file.

It sets the compiler to issue more warnings, so you catch more errors at compile
time, instead of runtime!  This has saved me hours of debugging, easily.

It has debug and release configurations, so you can (more) easily debug when you
have problems.

Many more things you may not need in EECS 338.

{{site.nextslide}}

## How?

1. Put it in your project root.
2. Fill out the variables at the top.
3. Put all your source files in the `src/` directory.
4. Run `make`.
5. Your program is at `bin/release/[name]`

{{site.nextslide}}

## For future reference

- Debugging:
    - `make CFG=debug`
    - `bin/debug/[name]`
- Variables...
  - `PROJECT_TYPE=executable`
  - You can leave `TEST_TARGET`, `STATIC_LIBS`, and `EXTRA_INCLUDES` alone.
- You should never need to `make clean`!

{{site.nextvertical}}

## Fundamental Differences

{{site.nextslide}}

## C only looks like Java

- But C isn't anything like Java
- Java runs on a virtual machine that manages objects
- C compiles to assembly code that runs directly on your processor
- C is more like slightly higher level, portable assembly
- C gives you direct access to your process's memory

{{site.nextslide}}

## Types of Memory in C

- **Static:** memory that is known and set aside when you compile your code.
    - EG: global variables
- **Heap:** memory that will be allocated and used when your program is run.
    - EG: `malloc()` and `free()`
- **Stack:** memory that is known at compile time, and is alloted when a
  function is called.
    - EG: local variables

(See diagram of memory model on board.)

{{site.nextslide}}

## Garbage Collection in Java

- When you use `new` in Java, it allocates space in memory for the instance
- Once the instance is done being used, the memory space is "freed", so other
  objects could be put there.
- C doesn't do this!
    - You allocate and free memory manually
    - If you forget to free, you get a "memory leak"

{{site.nextslide}}

## C Strings

- In Java, Strings are immutable, and fairly easy to use.
- In C, strings are just arrays of `char`s, terminated by a NUL character.
- Doing things like concatenating strings usually requires memory allocation to
  create a new string.
- `strlen()`, `strncpy()`, `strncat()`, `strncmp()`.

{{site.nextvertical}}

## Compiling

Practical consquences of how C compiles.

{{site.nextslide}}

## Java

1. `javac` translates Java into JVM bytecode
2. You end up with a bunch of `.class` files
3. `java ClassName`:
   1. JVM searches for `ClassName.class` in your "classpath"
   2. JVM loads the first one it finds
   3. JVM calls `main()`
4. JVM "interprets" the bytecode.
5. JVM may even convert the bytecode to machine code to run faster.  This is
   called "Just In Time compilation," or JIT.

{{site.nextslide}}

## C

1. Your C compiler converts each source file into an object file.
   - Object file: mostly compiled code, except for references to outside names.
2. Your compiler then combines each object file into an executable.
   - This is called "linking"
   - It hooks up all the unknown names from the object files with the code from
     other object files that defines them.
3. You run the code.  Your OS loads the program into memory and starts executing
   at the `main()` function.

{{site.nextslide}}

## How Linking Works

Say you have two code files:  `main.c`:

```c
#include <stdio.h>
#include "stuff.h"
int main(int argc, char *argv[]) {
  int a;
  printf("Doing stuff.\n");
  a = do_stuff(5);
  printf("Finished doing stuff.\n");
}
```

And `stuff.c`:

```c
int do_stuff(int x) {
  return x + 1;
}
```

{{site.nextslide}}

<img style="max-width: 100%;" src="{{site.baseurl}}/images/main.o.png"></img>

{{site.nextslide}}

<img style="max-height: 600px; max-width: 100%;" src="{{site.baseurl}}/images/stuff.o.png"></img>

{{site.nextslide}}

<img style="max-width: 100%;" src="{{site.baseurl}}/images/linked.png"></img>

{{site.nextslide}}

## Header Files

Missing functions are resolved when you link objects together.

But, the compiler still needs to know what the function returns, what arguments
it takes, etc.

So, you put the function declaration in a header file.

{{site.nextslide}}

## Declarations vs Definitions

A declaration for `do_stuff()`:

```c
int do_stuff(int);
```

A definition for `do_stuff()`:

```c
int do_stuff(int x) {
    return x + 1;
}
```

For variables:

```c
int x;     // declaration of x
x = 5;     // later, a definition
// OR...
int x = 5; // do both at once
```

{{site.nextslide}}

## Only put declarations in headers!

Never put definitions in headers!

Example time!

{{site.nextslide}}

## Always use include guards in headers

```c
#ifndef NAME_OF_HEADER
#define NAME_OF_HEADER
// header file contents.
#endif
```

Otherwise, the header may be included multiple times in a file, and end up
redeclaring everything in the header.  Which is an error :(

{{site.nextvertical}}

## Syntax

(just the differences)

{{site.nextslide}}

## Functions Don't Go In Classes

Since there are no classes in C, it's pretty difficult to have functions inside
of classes.

{{site.nextslide}}

## Declaring Structs

```c
struct customer {
  char *name;
  int id;
  unsigned int age;
  struct customer *child;
};
```

**Don't forget the semicolon at the end!**

Use it like this:

```c
struct customer mycustomer;
mycustomer.name = "Stephen";
// ...
```

{{site.nextslide}}

## Typedef

`typedef` allows you to create a new *name* for an *existing* type.  EG:

```c
typedef struct customer customer_t;
typedef unsigned int id_t;
typedef struct {
  char *destination;
  int id;
} bus_t;
```

- That last one allows you to use your structs without the `struct` keyword.
- It's common practice to end type names with `_t` so readers can tell they are
  types, and not any other identifier.

{{site.nextslide}}

## Static

*Forget what you know about it in Java.*

* `static` variables are stored in static memory.
    * I'll explain more about this in a bit.
* `static` functions can only be used in the file where they're defined.
    * Good for helper functions!

{{site.nextvertical}}

## Pointers

{{site.nextslide}}

Create a pointer to an int:

```c
int *pointer_to_int;
```

Get the address of a variable:

```c
int blah = 5;
pointer_to_int = &blah;
```

Dereference a pointer:

```c
printf("value pointed by pointer_to_int is: %d\n", *pointer_to_int);
// value pointed by pointer_to_int is: 5
```

{{site.nextslide}}

## Arrays

- Arrays behave *like* pointers.

```c
int indices[] = {0, 1, 2, 3, 4, 5, 6, 7};
printf("indices[0]: %d\n", *indices);
// indices[0]: 0
printf("indices[1]: %d\n", *(indices + 1));
// indices[1]: 1

// etc.
```

This is why arrays are zero-indexed!

{{site.nextvertical}}

## Debugging C

{{site.nextslide}}

## printf debugging

A classic, but not very good way to debug your code.

Scattered `printf` statements make your code hard to read, and your output less
concise.

However, in a pinch, `printf` debugging is an *ok* way to do it.

Thankfully, you have some better options.

{{site.nextslide}}

## Debug Symbols

In order to use a debugger, you need to enable "debug symbols" when you compile.

My makefile's `debug` configuration does this for you.  Just `make CFG=debug`,
and then debug the program `bin/debug/main`.

Or, use the `-g` flag when you compile.

{{site.nextslide}}

## GDB

Live demo time (rough transcript below)

```bash
$ gdb bin/debug/main
GNU gdb (GDB) 7.10
Copyright (C) 2015 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-unknown-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from bin/debug/main...done.
(gdb) break ex_debug
Breakpoint 1 at 0x40087c: file src/debug.c, line 19.
(gdb) run debug
Starting program: /home/stephen/repos/c-from-java/bin/debug/main debug

Breakpoint 1, ex_debug () at src/debug.c:19
19        a = 5;
(gdb) print a
$1 = 32767
(gdb) next
20        b = 3;
(gdb) print a
$2 = 5
(gdb) print b
$3 = -134225616
(gdb) step
21        *c = a + b;
(gdb) print b
$4 = 3
(gdb) continue
Continuing.

Program received signal SIGSEGV, Segmentation fault.
0x0000000000400896 in ex_debug () at src/debug.c:21
21        *c = a + b;
(gdb) backtrace
#0  0x0000000000400896 in ex_debug () at src/debug.c:21
#1  0x000000000040083f in main (argc=2, argv=0x7fffffffe598) at src/main.c:35
(gdb) quit
A debugging session is active.

        Inferior 1 [process 3618] will be killed.

Quit anyway? (y or n) y
```

{{site.nextslide}}

## GDB Main Points

- break: set breakpoints on functions or file:line
- Put command line arguments after `run`.
- next: "step over", step: "step into", continue: "continue"
- **backtrace** is probably the most useful for debugging segfaults.
- Pros of GDB
    - Can use it over SSH.
- Cons
    - Rather difficult to use.

{{site.nextslide}}

## GUI Debuggers

- GDB-TUI: do the key sequence "Control-x a" in GDB to get a crappy GUI.
- Emacs GDB Mode: if you already use Emacs, this may work for you.
- Recommended: [Nemiver](https://wiki.gnome.org/Apps/Nemiver/)
    - Have to use this on your own Linux machine or VM.
- Others:
    - Eclipse CDT has a debugger
    - A list: https://sourceware.org/gdb/wiki/GDB%20Front%20Ends

{{site.nextslide}}

And now, a demo of Nemiver!

{{site.nextslide}}

## Valgrind

- Valgrind is a tool that you can use to check for all sorts of memory errors.
- Especially, it can find memory leaks.
- `valgrind bin/release/main`

{{site.nextvertical}}

## Getting help

{{site.nextslide}}

## Man Pages

- C library is extremely well documented in manpages.
- `man function_name` usually gets you documentation
    - If that doesn't work, try `man 3p function_name`.
- Not sure what man page you want?
- `apropos [search term]` will give back a list of man pages to check.

{{site.nextslide}}

## Online Specification

- I find the Unix specification to be quite good for answering questions about
  header files.
- http://pubs.opengroup.org/onlinepubs/9699919799/
- Use the search function, or go to Section 13, headers!

{{site.nextslide}}

## Hacker Society!

- Many of us have taken EECS 338, or know C.
- Glennan student lounge may have people who can help.
- Check IRC
- Facebook group

{{site.nextslide}}

## Damage Control

- Use Git!
- Don't do anything stupid!  Collaboration is only OK if explicitly stated.
- Given the choice between turning in:
    - Something that compiles, but doesn't fully complete the assignment, or
    - Something that doesn't compile, but has more assignment code,

... **ALWAYS** turn in code that compiles (test it on the EECS 338 VM).

Your TA's don't want to try to fix code that you didn't bother to get to
compile.  Code that compiles and mostly runs gets more points!

{{site.nextvertical}}

# Questions!

{{site.endslide}}
{{site.endvertical}}
