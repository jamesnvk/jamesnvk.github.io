---
layout: post
title: RESTful Rails Blog with OAuth
---

I decided to build a fully functional blog application from the ground up for my Rails assessment project at Flatiron School. It was the biggest challenge I've faced since starting my journey into programming. I feel like I have come so far in the world of programming, yet at the same time barely scratching the surface. That is awesome. Steep learning curves excite me.

One of the most challenging sprints of this project was building out the comments system. My User model looks like this: 

![Alt text](/assets/ss6.png)

Post model: 

![Alt text](/assets/ss8.png)

and my comment model acting as a join:

![Alt text](/assets/ss7.png)

My problem was that I needed to be able to add a comment - from a user - to a particular post. I spent a lot of time trying to create a comment through the posts controller until I realized that even though my comments model was a join table, I still needed to build the comments controller to separate concerns. Even though a comment belongs to a post, a post controller should not have the responsibility of creating a comment. A comment is still a valid object in my program that deserves attention just as much as a User or Post.

Here's how my comments controller turned out: 

![Alt text](/assets/ss9.png)


My next challenging sprint was the implementation of Oauth using facebook as a provider. [This guide](https://github.com/plataformatec/devise/wiki/OmniAuth:-Overview) is an excellent step by step walkthrough on how to implement Oauth via facebook. One important thing to note about this was that I had trouble with my APP ID consumer key and secret key. A bug prevented me from being able to set my keys through my environment, so I had to add both keys to my project. It is extremely important that these keys, especially the secret key, is not in public view, ie. in the git source code.

To take care of this problem I added a file in my <code>config/initializers</code> folder that contained both keys as constants, then added that file to my .gitignore file so it would not get uploaded as public source code on github. I realize that this may not be an optimal solution as all code is still uploaded to a server.

My last sprint that I wanted to discuss was building a REST infrastructure. A design decision I made early on was to rename the <code>PostsController</code> to <code>InjuriesController</code> because I wanted my routes to be <code>/injuries</code>, <code>/injuries/new</code> etc.. but quickly realized that that design decision may be confusing as the app gets larger. I've learned that it is usually better to err on the side of convention when it comes to Rails development. So instead, I kept <code>PostsController</code> and passed an option to <code>resources</code> in my routes file:

![Alt text](/assets/ss10.png)

______________

<i>I had an awesome time and learned so much while building this app. If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out the full source code for this project on github [here](https://github.com/jamesnvk/injury-door)</i>

