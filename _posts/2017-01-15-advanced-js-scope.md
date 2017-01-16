---
layout: post
title: Advanced JavaScript - Scope
---

I have an obsession with learning, especially when it is something I want to master. I am currently reading *You Don't Know JS* by Kyle Simpson. So far this book has really helped me solidify my understanding of what is *really* going on under the hood in the JavaScript engine. It's been so helpful that I actually decided to put down the money for a monthly subscription to his Frontend Masters curriculum. Today I'm going to be covering the basics of scope in JS. If you would like to read more, I highly recommend checking out his book (it's free on <a href="https://github.com/getify/You-Dont-Know-JS" target="_blank">github</a>!)

What is scope? I like to think of scope as a bubble. There can be objects, functions, and even other bubbles inside this bubble, but bubbles never overlap - meaning each bubble has its own "environment". You can create a bubble by declaring a function, which in technical terms means authoring a *function declaration*. Contrast this with authoring a *function expression*, which is treated differently by the JavaScript compiler.

![Alt text](/assets/ss19.png)

Since JavaScript treats its functions as first class citizens, any function that is *declared* will get precedence over other variables that are declared with the same name. It also means that if I decided to call foo() at the top of the file, it would behave as expected, unlike a call to bar, which I will explain below.

![Alt text](/assets/ss21.png)

Contrary to popular belief, JavaScript is actually a compiled language.<br>
<code>var a = 2;</code> 
How does this code work? It may seem simple, and most people that are coming from different languages (including myself, I started out learning Ruby) will look at that code and think it is executed as a single statement. That is actually incorrect in JavaScript. When the compiler first encounters <code>var a</code> it asks our current scope or bubble if variable a already exists - if it does, our compiler ignores the statement, if it doesn't it creates a new variable in the current bubble. **Remember that when a new variable is created initially its value is set to undefined.** Once our compiler is done compiling code, our engine then handles the <code> a = 2 </code> assignment during run time. The engine comes across a = 2 and asks our current bubble, do you have a variable a? The bubble responds yes, hands the variable a off to engine and engine assigns it to the value 2.

What happens when our bubble doesn't have the variable the engine is asking for? It looks for it outside of its current bubble (if its not in global, of course). The process repeats until it finally reaches the global scope and if it does not find the variable, the result is an error. However, there is a gotcha. If a variable is being *assigned*: for example there's this following code: 

![Alt text](/assets/ss20.png)

during run time and it reaches global scope, global scope will **create a new variable** for us to use. As you can imagine, this will most likely lead to a whole bunch of nightmare situations. This is why a lot of developers advocate the use of "use strict"; on top of the source file to prevent this situation from ever happening.


I thought it seemed like a lot to take in at first, coming from a dynamic language like Ruby. There is also a whole set of details that I did not cover here that includes compiler terminology like "LHS" and "RHS" when our engine handles the code. But as I'm learning more and more about how JavaScript really works, the language is starting to grow on me. Even though I develop primarily in Angular, I'm confident that I have the necessary foundational skillset that will allow me pickup any future JS framework and hit the ground running.

______________
If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out the full source code for my latest project on github [here](https://github.com/jamesnvk/openhealth).



