---
layout: post
title: Advanced JavaScript - new
---

Since I just wrote up a [blog post on the this keyword](https://jamesnvk.github.io/2017/02/16/advanced-js-this/), I figured I would round up some knowledge on <code>new</code>. The <code>new</code> keyword does have some built in ties to <code>this</code> that I want to illuminate, but I also want to clarify some misconceptions about <code>new</code> in the world of JavaScript.

One common misconception in JavaScript is that when we are calling <code>new</code> we are instantiating a new object from some sort of class. Instead, what we are really doing here is *constructing* a brand new object, then attaching whatever properties our *function constructor* has. For example:

![Alt text](/assets/ss22.png)

Notice that the <code>f</code> in <code>foo</code> is lowercase. This is to illustrate the point that even though we typically see function constructors start with a capital letter, that is simply just a convention to let other developers know that the function is meant to be used as a constructor.

So what exactly happened when we called <code>new foo()</code>? Just like the [4 rules of this](https://jamesnvk.github.io/2017/02/16/advanced-js-this/), <code>new</code> has some rules as well. Can you guess how many rules there are for <code>new</code>? If you said 4, you are correct! Let us run through what happens when we invoke a function with <code>new</code> in front of it.

> 1. A brand new object is created (or constructed) out of thin air.
> 2. That object is attached to the function's *prototype*.
> 3. That object is set as the <code>this</code> binding for the function call.
> 4. Unless the function has a return value of an alternate object, it implicitly returns <code>this</code> (the newly constructed object)

Just like <code>this</code>, <code>new</code> isn't some magical class oriented keyword. Understanding the core functions and principles of JavaScript can really open up the language in many ways.

______________
If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out my github <a href="https://github.com/jamesnvk/" target="_blank">here</a>.