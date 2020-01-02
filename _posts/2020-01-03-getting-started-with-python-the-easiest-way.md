---
layout: post
author: Joshua Owoyemi
title: Getting Started with Python the Easiest Way
comments: true
---
About 4 years ago when I wanted to start learning Python Programming, the top question on my mind was, "How do I get started quickly?". Over the years, many things have changed about Python programming itself. It has become more useful and popular for general programming and most especially for Data Science, Machine Learning and Deep Learning. As the interest in the programming language have been increasing over the years, the question is still relevant - "How do I get started with Python Programming in the easiest way?". I will try my best to answer that question in this post.

<!-- <center>
</center> -->
![banner](/media/python_post_banner.jpeg)


In the beginning, I set out to write a short and straight-to-the-point article but I quickly found out there are so many explanation to do. If you just want the action, you can skip to the "Procedures" section. However, I encourage you to keep reading as this will give the needed foundation for the reason I am giving the recommended steps.
For a programming language like Python, new learners soon realize that there are many concepts and hurdles they need to overcome in order to begin to appreciate the language (as with other programming languages). One of such is Packages, or Libraries. This becomes more difficult when the learner has no programming experience. It is therefore necessary to have a little understanding of how the programming language environment works in order to get the best out of it with little 'head-banging'.
Packages
A programming language is simply a set of vocabularies arranged in a special way called Syntax, used in instructing the computer to perform specific tasks. Programming languages build on several layers of complexity, hence a simple code like print("Hello World!") has several lines of codes (or vocabularies) that someone has written behind it so that it can do what you expect it to do. And you, or another programmer can take this code and add more of yours and use it for some other purpose. You can then 'Package' the code you have written and make it available for other people who also use it for their own purpose. This is the concept of Packages.
Truth is, you won't need to write all your codes from scratch, you will need bits and pieces from what other people have written. This is made possible through Packaging also referred to as Libraries.

![concept_of_packages](/media/concept_of_packages.png)
*Concept of Packages*

Concept of PackagesYou will therefore have different libraries that do specific tasks, such as arithmetic operations, or files processing, or image processing, etc. This makes the life of a programmer much easier as you only need to 'import' these libraries into your code and use them to achieve your own aim.
It is possible to work with the official Python software provided by the Python Software Foundation , which I call Vanilla Python. It comes with pre-provided Libraries. However, you will soon realize that it is pretty limited and that you need more packages than this has to offer. The Python software also come with a Package installer called pip which is intended to help in installing extra packages. However for a beginner, things begin to get complicated when you realize you need to install multiple of Packages with several dependencies (more on this later). This is actually the path that most beginners will be introduced to, but there is a better way, and easier too.
So imagine all these Libraries floating around on the internet (or in space, or wherever) because everyone is writing their own and for specialized and specific purposes. There is therefore a need for a management system for these Libraries, to help in organizing them and distributing them easily for programmers who need them. Hence, there a number of such package management systems built on top of the Vanilla Python software to do just that. Examples of such are Anaconda, Enthought Canopy and WinPython.
Dependencies
The easiest way to explain is this is to say that a package needs another package to run successfully, hence it depends on that package. This is because the writer of the later package used codes from the former package to build his own package. It is therefore possible to have a package that depend on multiple other packages to run, and trying to install all the needed dependencies with the right versions can be a pain for a new python programmer. I know because I struggled with this a lot as a beginner. This is where package distribution platforms like excel. They help to provide not just a package but also the right dependencies for each installed package.
Now that you know about packages and dependencies, you will agree that it is better to have all the pieces together and figure out the details as you go along.
Procedure
Finally, here are the steps to the path I recommend for getting started with python the easiest way. It is actually only one step.
Install Anaconda: Anaconda is the single easiest package manager and distribution platform that will make you get started easily. It is cross-platform (that is, available on Windows, Mac OS and Linux), easy to install and comes with handy tools (mostly GUI) such as the python Integrated Development Environment (IDE) - Spyder, Jupyter Notebook - for interactive coding environment, and others. Even for experienced programmers, Anaconda offers great tools for data science, database and project management for easier and painless workflow. See the image below for a cross-section of tools offered by Anaconda.

![anaconda_navigator](/media/anaconda_navigator.jpeg)
*Anaconda Navigator*

Anaconda NavigatorThat is pretty much all you need as beginner. There are other considerations such as the IDEs and environments, which you will have to deal with sooner or later but with this down, those are more of a choice for convenience and efficiency. For me, the image below gives an overview of the Python programming "getting started" map.

![getting_started_map](/media/getting_started_map.png)
*The "Getting Started" map*

The "Getting Started" mapAnd in case you are wondering, environments are a collection of packages accessible to a python compiler. Imagine you are working on multiple projects. Usually, each project will need a set of different packages. Therefore, it is possible to have several collection of packages bundled together for specific purposes or projects which do not affect or interact with each other. As you may have seen in the map above, Anaconda also provide tools for achieving this.
I hope I have been able to answer the question from the beginning of this post. There may have been some concepts that are still yet unclear, please ask about them in the comments below. I hope to post more about Python programming in the future. Let me know what you would like to read about. If you find any mistakes, be sure to point them out.
Thanks for reading through.

...

Originally published on [Medium](https://medium.com/@tjosh.owoyemi/getting-started-with-python-the-easiest-way-5f52c6187ad8) on May 4, 2019.