---
layout: post
title:      "Metaprogramming - What is it? "
date:       2017-12-28 02:36:47 +0000
permalink:  metaprogramming_-_what_is_it
---


I have heard about Metaprogramming before starting the section, and when my cousin tried to explain it to me it sounded like it was something that ruby ninjas use. But the truth is that it isnt very difficult or scary at all!

Metaprogramming is a technique by which you can write code that *writes* code by itself. What this means is that you can define and change methods and classes depending on the state at which your program exists during runtime. in other words, you can reopen and modify classes and catch methods that dont exist and create them as you run your program. 

Why might we want to use metaprogramming? for one - your code looks cleaner, which is the ultimate goal of a ruby expert. another goal is that it allows your code to run faster by configuring data from runtime to compile-time. 

By cutting down the amount of lines of code your program has, metaprogramming saves time when writing, debugging and running your program, which makes it a vital tool for OO programming. 
