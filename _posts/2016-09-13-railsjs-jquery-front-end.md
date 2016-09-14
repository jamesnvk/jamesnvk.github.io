---
layout: post
title: RailsJS jQuery Front End - Handlebars
---

It's been a while since my last blog post but I'm back at it again with another new app! This time I built a Pinterest style app utilizing javascript/jQuery and HandlebarsJS to handle the front end while Rails took care of the back end. If you're unfamiliar with Handlebars I recommend you take a quick look at the <a href="http://handlebarsjs.com/" target="_blank">documentation</a> before proceeding.

A high level overview of how Handlebars works is that it basically gives us templates that we insert into our HTML pages that we want to use our API with. Then we can use javascript to call and insert objects from the database directly into the DOM without a page refresh. Lets start by taking a look at our template in our HTML:

![Alt text](/assets/ss12.png)

We can see here that this looks almost like an ERB file. In fact, this is basically ERB for javascript. Since we are still in an actual ERB file we can still use ruby `<%= current_user.name %>` and javascript `[[content]]`* at the same time. Pretty cool. 

*<i>Markdown doesnt like the curly braces so we have to use brackets</i>

Next lets create a constructor in javascript.

![Alt text](/assets/ss11.png)

Here our Comment belongs_to a user and has the attributes id, content, and user_id. After we set this up, next we need to build a function on this prototype that will return the HTML for the page we have our script in.

![Alt text](/assets/ss13.png)

You're probably wondering what the `.template` method is on our Comment. First, we need to grab the template (an HTML string). Then, if you recall from the documentation we need to *compile* our HTML string into an actual handlebars template.

![Alt text](/assets/ss14.png)

What this now allows us to do is inject our object's properties using that mustache syntax into our DOM via our compiled template!


