---
layout: presentation
title: Algorithms Design Techniques
theme: sky
published: true
categories: talks
date: 2015-09-26 00:25:00
---
{{site.startvertical}}
{{site.startslide}}
### Algorithm Design Techniques

> Presented by : Enes Kemal Ergin

{{site.nextslide}}
1. How are the different approaches solves the same problems?
2. How are the different problems solved by the same approaches?

{{site.nextslide}}

Over the centuries, people who solve their problems with algorithms realized that problems were vary but the approaches/ideas were similar. Then they saw the pattern and they came up with some techniques to design algorithms and put them in types.

When I introduce these techniques, I will stick with one example, which will be finding a person who you don't know in a library.

{{site.endslide}}
{{site.endvertical}}

{{site.startslide}}
### 1. Brute Force

- Brute force or Exhaustive Search, examines every possible alternative.
- It is like you are asking every person in the library
- You will find it eventualy but it may be too late.
- Easiest type to design and understand.
- In some cases they work well, in bioinformatics
- Mostly too slow.
- Even for the small sets, try to avoid this type

{{site.endslide}}

{{site.startslide}}
### 2. Branch-and-Bound

- Branch-and-Bound or Pruning
- Technique when you omit large number of alternatives in Brute Force Algorithm
- It is like you know the gender of the person you automatically

{{site.endslide}}

{{site.startslide}}
### 3. Greedy Algorithms

- Most algorithms use iterative procedure, and greedy,
- Chooses the “most attractive” alternative at each iteration
- It is like you are blind and you are walking through the sound of that person in library (I am not even sure if talking in library is appropriate) ;)
- This type is very direct if there is something like a wall in between you and your person, that may prevent you to reach him/her
- When problem gets more realistic, the chance of failure using greedy will increase.

{{site.endslide}}

{{site.startslide}}
### 4. Dynamic Programming

- Organizes the computations to avoid re-computing the same values that you already know
- This type is not applicable to our example
- This type is worth having a presentation for itself.

{{site.endslide}}

{{site.startslide}}
### 5. Divide-and-Conquer

- Divide big problem into smaller sub-problems
- Solve sub-problems individualy and unite the results the get a bigger picture
- Critical step is to combine results to make one for big problem

{{site.endslide}}

{{site.startslide}}

### 6. Machine Learning

- This approach is all about statistics and data
- Often base their strategies on the computational analysis of previously collected data.
- In our example we get the information of where usually our target sit and stick around then we might find him/her
- Machine Learning methods are getting very popular

{{site.endslide}}

{{site.startslide}}
### 7. Randomized

- Randomize the starting point

{{site.endslide}}
