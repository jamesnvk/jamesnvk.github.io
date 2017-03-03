---
layout: post
title: ES6 Initial Impression
---

One of the main reasons I am so excited to continue learning to master Javascript is the constant evolution of the language. The popularity of the Angular and React frameworks have shown us that this language is here to stay. <a href="https://github.com/lukehoban/es6features" target="_blank">ES6</a> is the latest version of the language and has come with some significant updates.

The first thing that caught my attention and probably many others, was the <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions" target="_blank">arrow function</a>. My initial impression on this: not a fan. There seems to be many different syntax use cases for it that can get quite confusing if someone is not familiar. Yes, I could learn all the syntax cases but the trade off is another mental tax when reading code when I could've just simply typed <code>function</code>. What I do like about the arrow function, however, is the fact that you don't have to worry about the <code>this</code> binding. For example, instead of using a common lexical scoping hack such as <code>var self = this</code> to grab context for another function, the <code>this</code> binding is *implicitly* lexical with the arrow.

An ES6 update that I am a fan of are the new <code>let</code> and <code>const</code> <a href="https://github.com/lukehoban/es6features#let--const" target="_blank">declarations</a>. These are block-scoped binding constructs. The <code>let</code> keyword enforces what we have already been doing stylistically with var. For example, putting a <code>var</code> inside an <code>if</code> block - that <code>var</code> is still accessible to the entire scope, but it makes sense to put it there for another developer to see that that <code>var</code> is meant to be used for that <code>if</code> statement. The <code>const</code> keyword is simply a variable that cannot be changed (a getter). I don't think that just because <code>let</code> is now in the language that we should get rid of <code>var</code>. Both have their place in code and I prefer to write <code>let</code> when I know I want my variable blocked - such as in a *for loop*, or in that earlier example with the if statement.

Overall I think Javascript is moving in a great direction with these changes. As I learn and start incorporating more ES6 features in my code I will continue to update this blog with my thoughts. Stay tuned!

______________
If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out my github <a href="https://github.com/jamesnvk/" target="_blank">here</a>.