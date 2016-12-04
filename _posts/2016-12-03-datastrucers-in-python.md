---
layout: post
title: Data Structres in Python!
---

# Data Structures in Python

##### Welcome New Comer!  Come Come!  Learn one of the most importantant concepts of Computer Science in the wonderful language that is Python!

### Table of Contents
* Arrays
* Linked Lists
* Stacks
* Queues
* Hash Tables
* Trees
  * Binary Trees
  * Binary Search Trees
  * AVL Trees
 * Graphs
  * Directed and Undirected
  * Breath First Search (DFS)
  * Depth First Search (DFS)
  * Dijkstra's Algorithm


###### Skip if this does not portray to you
(quick run down of python syntax, "hell yeah")

* Ints
 * These are your generic numbers.  No decimal places, it basically cuts that straight off.
 * Let's see what this looks like in action!

``` python
# Declaring an Int
 num = 1
```
As you can tell above, what is this syntax?  What's going on here?  Where the hell did I declare this variable?  Welp here comes the magic of Python!  In python you do not need to explicitly declare then.

* Floats/Doubles
  * These are the numbers with a bit more precision.  yeah that's right! DECIMAL POINTS!
  *  Floats be the small numbers, and if you need more precision, doubles are it!

``` python
# Declaring a Float/Double
num = 1.1
```

There we are!  Yup implicitly declared and well..yeah you know the rest.

* Strings
 * Now how do you actually keep you know, "WORDS"
 * Welp do not worry! Python has got you there!

``` python
# Declaring a String
name = "Qasim"
```

There are also obviously a ton of operations that can be done on a String but I'll probably explain them through a different tutorial

(Alrighty done with the run down)

## Arrays

So let's start out with Arrays.  Imagine having a box of space.  Let's bring that down to a cardboard UPS box.  There is no way that box is getting any bigger.  It's made that way.  If you need more space you'll need a bigger box man unless you pull some Package Engineering magic and make extra space with the same box out of your wonderful equations.

What do we use boxes for initially?  To store things silly!  I'm assuming you all know the basic primitives and common use objects such as Ints, Doubles, Floats, Strings.

See here now, Python's Arrays aren't exactly arrays.  they do much much more, such as implement some really insane functions and do so many Data Structures on they're own.  We'll get into that as we go along.


### Lists

Their arrays are actually denoted as a structure called List.  Here is the syntax for a list.

```python
# Declare a List
myList = [0,1,2,3]
```

We declare a list as any other variable name but add brackets and commons in between to contain elements within in the list.

We are going to need to access elements within the list so that would be done with this syntax.

With the one element we could easily access one element and then edit it.  Be sure to watch out for the type that you are setting the variable to.  Types of the variables cannot be changed after declaring into one specific type.


```python
# Declare a List
myList = [0,1,2,3]

# Accessing element in List
myList[2] = 234

# Incorrect Syntax
myList[2] = "Penguin"

```
