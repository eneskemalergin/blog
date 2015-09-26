---
title: Projects
layout: contentbase
gh: <span class="fa fa-github fa-lg"></span>
bb: <span class="fa fa-bitbucket fa-lg"></span>
web: <span class="fa fa-globe fa-lg"></span>
pdf: <span class="fa fa-file-pdf-o fa-lg"></span>
tw: <span class="fa fa-twitter fa-lg"></span>
---
# Projects

Currently in Construction <Change name into projects.md>

## Current

### Using Prior Biological Information to Select Features for Predicting Cancer Phenotypes

This is a 10-week bioinformatics research project scheduled for the summer
of 2015.  I will be working in conjunction with Dr. Mehmet Koyuturk to develop
an algorithm for selecting combinations of somatic mutations which are
correlated with cancer phenotypes.

[{{page.pdf}} View the Proposal](https://dl.dropboxusercontent.com/u/24472738/proposal.pdf)

## Works in Progress

I may never decide these projects are *done,* since I'm always improving them.

### `libstephen` -- A C Library

This humbly-named library is the foundation for much of my C programming.  It
extends the standard C library with support for a few important data structures,
regular expressions, command line argument parsing, lightweight unit testing,
and memory leak detection.  I continue to rethink and improve its architecture,
so it is not yet at a place where other people should use it in their own
programs.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/libstephen)

[{{page.web}} Visit the webpage!](/libstephen/)

### `cky` -- A Parser

This project is actively under construction.  It's intended to become an
impementation of the [CKY](http://en.wikipedia.org/wiki/CYK_algorithm) algorithm
for parsing [CFGs](//en.wikipedia.org/wiki/Context-free_grammar).  In the end, I
intend for it to be similar to, but not necessarily compatible with,
[Lex](http://en.wikipedia.org/wiki/Lex_(software)) and
[Yacc](http://en.wikipedia.org/wiki/Yacc).

`cky` is based on the `libstephen` library.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/cky)

- - -

## Past

### Twitter Bot

[Hacker's Society](http://hacsoc.org) hosted an event called "Python and Pie"
for incoming freshmen during Fall 2015 orientation.  I gave an intermediate
Python tutorial, which was all about writing a Twitter bot using Python.  As a
result, this bot and the accompanying tutorial are now on GitHub for others to
learn from.  The bot responds to any @mention with a randomly chosen Taylor
Swift lyric.

[{{page.gh}} Code and Tutorial at GitHub](https://github.com/brenns10/pypie15int)

[{{page.web}} Blog Post]({% post_url 2015-08-22-python-and-py %})

[{{page.tw}} Tweet at the Bot](https://twitter.com/pypie15bot)

### `tswift` - A Python MetroLyrics API

Get your Taylor Swift lyric fix with this quick'n'dirty tool for downloading
song lyrics from MetroLyrics.  Or, you know, any other artist's lyrics.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/tswift)

[{{page.web}} It's on PyPI!](https://pypi.python.org/pypi/tswift)

### CBot

A fun little challenge - write a functioning IRC bot in C!  This little guy was
a great excuse to use Libstephen's regular expressions in the real world, as
well as learn all about dynamic loading of modules and the IRC protocol.  CBot
currently has the basic functions necessary for a chatbot, and I'm sure I'll
return every now and then to expand on his available plugins.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/cbot)

### Tetris in C!

A 24 hour Tetris implementation written in C, using the `ncurses` library.  I
wrote an accompanying blog post about it, which also touched on how important I
find my personal projects, even if some are reimplementations.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/tetris)

[{{page.web}} Read the blog post]({% post_url 2015-06-12-tetris-reimplementation %})

### `PyWall` -- A Python Firewall

My EECS 444 project group (Jeff Copeland, Andrew Mason, Yigit Kucuk) implemented
a firewall in Python.  While obviously not practical for normal use, this
firewall illustrates the basics of packet filtering (including TCP connection
tracking) in a high-level lanugage, which is much easier to understand and
extend than C.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/pywall)

### `yams` -- YAMS: Awesome MIPS Server

My EECS 314 project group (Jeff Copeland, Andrew Mason, Thomas Murphy, Katherine
Cass, Aaron Neyer, and myself) created a HTTP 1.0 web server, written entirely
in MIPS assembly.  In addition to serving static pages, it also comes with
"dynamic content" courtesy of a
[Brainf***](https://en.wikipedia.org/wiki/Brainfuck) interpreter also written in
assembly.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/yams)

[{{page.web}} Read the blog post]({% post_url 2015-05-17-yams %})

### Minesweeper

A minesweeper game written entirely in C, with both a command line and graphical
interface.  This was a fun and short project to apply my C knowledge, as opposed
to my more ambitious, long running projects above.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/minesweeper)

### `caseid` -- Python module for Case IDs

This Python module aims to provide a plain and simple way for a programmer to
retrieve information about the owner of a Case ID.  It supports scraping CWRU
web services, as well as accessing the public LDAP server in order to find
people by their Case ID, and vice versa.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/caseid)

[{{page.gh}} Visit its Ruby cousin by Andrew Mason](https://github.com/ajm188/cwru_directory)

### `lsh` -- A Simple Shell in C

I wrote this to illustrate the system calls and basic mechanics behind a Unix
shell.  The accompanying blog post had a modest positive audience response.

[{{page.gh}} Visit it at GitHub](https://github.com/brenns10/lsh)

[{{page.web}} Read the blog post]({% post_url 2015-01-16-write-a-shell-in-c%})

### `wepa-linux` -- A CUPS Printer Driver

[WEPA](https://www.wepanow.com/) is a printing system used at my campus.  Users
'print' documents to their service, which stores them online to be printed at a
kiosk.  Drivers are available for Windows and Mac, but not Linux.

This driver, created at [HackCWRU](//www.hackcwru.com/) 2014, is a solution to
that problem.  It is a CUPS printer driver that allows rudimentary printing to
WEPA.  While the solution is not elegant (the security model of CUPS seriously
limits what a driver can do), it is effective.

[{{page.bb}} Visit it at Bitbucket](//bitbucket.org/brenns10/wepa-linux)

### `chat` -- A Quick and Dirty Chat System

This is a quick chat client/server implementation in Python (and a little C).
It served as my introduction to socket programming in both languages.  It is
intended to be used as a local chat server over SSH, instead of constantly
sending `wall` messages to other logged in users.

[{{page.bb}} Visit it at Bitbucket](//bitbucket.org/brenns10/chat)
