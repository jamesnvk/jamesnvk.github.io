---
layout: post
title: Advanced JavaScript - this
---

The <code>this</code> keyword in JavaScript seems to be one of the most confusing mechanisms in the entire language. It is often compared to <code>self</code> in Ruby, which is a completely false comparison. In this blog post I am going to break down why that is, and how developers can effectively leverage the use of <code>this</code> instead of sit and wonder why things are breaking.

At its core, <code>this</code> is a run-time binding. In other words, it is a binding that is made when a function is invoked, and what it references is determined by the *callsite* of the function. The *callsite* is the place in code where a function gets executed. Every function, while executing, has a reference to its current execution context, called <code>this</code>.

There are 4 main rules to follow when we think about <code>this</code>.
> 1. Was the function called with <code>new</code>? If yes, <code>this</code> is that object.
> 2. Was the function called with <code>call()</code> or <code>apply()</code>? If yes, use the passed in <code>this</code> argument.
> 3. Was the function called with a containing object? If yes, use that object.
> 4. Default: fall back to global context, unless in <code>strict</code> mode.

That's it! These rules are in order of precedence, so the <code>new</code> keyword will always overwrite a containing object. The big take away here if you want to determine <code>this</code> is to focus on the callsite, then ask yourself those 4 rules.

______________
If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out my github <a href="https://github.com/jamesnvk/" target="_blank">here</a>.
