---
layout: post
title: Managing Authorization - and Usability - in Rails/AngularJS Part 1
---

I am currently helping build an employee training application for a busy restaurant with two other developers on a Rails backend with an AngularJS front end. So far this project has allowed me to leverage my experience in management to help offer insight on effective and efficient ways to help train the staff of a company with high turnover. It has also got me thinking more deeply about authorization and how managers will be interacting with the application. 

An easy UI allows both management and their employees to focus on what's important, instead of being bogged down by tasks or questions that are repeatedly asked about. I intend to read the book *Don't Make Me Think: A Common Sense Approach to Web Usability* by Steve Krug as it seems to be highly recommended. The title makes sense for the project. A restaurant is a fast paced environment where employees simply *do not have the time* to think. They simply just *do*. Making the application as simple and easy to use is our primary goal. On to authorization.

I decided to go with CanCan for authorization. CanCan is a Ruby library that restricts what resources and their actions a given user is allowed to access. These permissions are defined in a single location - the <code>Ability</code> class. CanCan also requires some type of current_user. We have implemented Devise to handle all of our authentication.

______________
Part 2 coming soon!
If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out the full source code for my latest project on github [here](https://github.com/jamesnvk/openhealth).

