---
layout: post
author: Joshua Owoyemi
title: Python Essentials - Variables and Types
comments: true
tag: Python Programming
excerpt: In this video post I talk about the first essential elements in python programming - the variable types. This will help to understand the basics of python variables and how to use them.
---

## Python Programming Essentials - Variables and Types

In this video post I talk about the first essential elements in python programming - the variable types. This will help to understand the basics of python variables and how to use them.

<iframe width="355" height="210" src="https://www.youtube.com/embed/videoseries?list=PLNEw_VEWvAEplEA3FWLbaLAMmwjj2K1ph" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### [Python Interactive Environment](https://docs.microsoft.com/en-us/visualstudio/python/python-interactive-repl-in-visual-studio?view=vs-2019)

In this tutorial, we are going to be using the python interactive environment, through the command line. The Interactive environment lets you enter arbitrary Python code and see immediate results. This way of coding helps you learn and experiment with APIs and libraries, and to interactively develop working code to include in your projects. This is a very great feature of the python programming language. In VScode, we will access this by typing `python` in the terminal at the bottom of the window.

### Printing

To print to the terminal in python is as simple as;

```python
print("whatever you want")
```

It is necessary at this point to introduce a variable type called `strings`. This is a kind of variable that stores alphanumeric values such as `"Names"` and `"Places"`. So if we would like to print out a message with a string variable, it is a simple as;

```python
full_name = "Joshua Owoyemi"
# print out the message with the name
print("Full Name: ", full_name)
```

You will notice that a line was started with `#`. This is to tell python program to ignore that line. Therefore anything written on that line is ignored and will not be `compiled`. It is called a `comment`. So if we do something like;

```python
full_name = "Joshua Owoyemi"
#print("Full Name: ", full_name)
```

Nothing will be printed to the terminal because the line has been commented out. `Comments` are useful to add human readable information to our code so we can easily remember or understand what we are trying to do in that part of the code. Please use comments as much as possible.

In python, other variables can also be printed in the already introduced manner. For example a variable storing a number can be printed as such;

```python
number = 7800000000
print("World Population = ", number)

# this is also possible
number = 7.8
print("There are, ", 7.8, "billion people in the world right now")
```

The print statement can be used in more various ways. More of this will be introduced in future sections.

### Strings

One class of variable that deserves to be treated separately is `strings`. This section will focus on `string` manipulation as it has been introduced earlier. Two major manipulation for python strings are `concatenation` and `slicing`. `Concatenation` allows two or more string sequences to be combined into one, such as;

```python
first_name = "Joshua"
last_name = "Owoyemi"
full_name = first_name + " " + last_name
```

Notice that a space (`" "`) is added in the middle as will be expected in a full name.

On the other hand, `slicing` allows us to split a single string variable to smaller pieces as such;

```python
full_name = "Joshua Owoyemi"
first_name = full_name[:6]
last_name = full_name[7:]
```

What happened here is that we give an `index` of the point where we want the string variable to be split. This idea can be applied to some other variable types. We will talk about them in later sections. We can also specify the starting and the ending index, sucha as;

```python
full_name = "Joshua Owoyemi"
first_name = full_name[0:6] # same output as previous example
last_name = full_name[7:13] # same output as previous example
```

### Numbers

Generally, in python, a variable type is whatever you assign to it. In other programming languages like `c++` and `java` this is not the case as you have to explicitly specify or declare the variable type. Even though there is still a differentiation between types such as `integers` (whole numbers) and `floats` (numbers with decimal places), this is only done implicitly.

```python
# assign a value of 2 to the variable x
x = 2

# assign a value of 10.5 to the variable y
y = 10.5
```

We can find out the type of a variable by using the keyword `type`.

```python
>>> type(x)
int

>>> type(y)
float
```

### Arithmetic Operations

The following are the arithmetic operations on numbers in python.

| Operation | Description                                             |
| --------- | ------------------------------------------------------- |
| x + y     | Sum of two numbers                                      |
| x - y     | Difference of two numbers                               |
| x * y     | Product of two numbers                                  |
| x / y     | Quotient of two numbers                                 |
| x // y    | Quotient of two numbers, returned as an integer         |
| x % y     | x “modulo”: y: The remainder of x / y for positive x, y |
| x ** y    | x raised to the power y                                 |
| -x        | A negated number                                        |
| abs(x)    | The absolute value of a number                          |

Arithmetic operations can also be combined;

```python
>>> 5 + 2 * 5
15

# opetations can be grouped using the parenthesis
>>> (5 + 2) * 5
35
```

### Boolean

Another important class of variable types is the boolean or simply `bool`. This has only two values; `True` or `False`, which can also be `numbers` or `0` respectively. this is very useful in making comparisons, which happens a lot in programming.

```python
# assign the boolean value True to the variable check
check = True

# assign the boolean value False to the variable present
present = False
```

### Boolean Operations

The following are operations for comparing variables. Results are either `True` or `False`.

| Operation | Description                                |
| --------- | ------------------------------------------ |
| x == y    | Check if two numbers have the same value   |
| x != y    | Check if two numbers have different values |
| x > y     | Check if x is greater than y               |
| x >= y    | Check if x is greater than or equal to y   |
| x < y     | Check if x is less than y                  |
| x <= y    | Check if x is less than or equal to y      |

