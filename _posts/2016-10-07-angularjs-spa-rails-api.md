---
layout: post
title: AngularJS Single Page Application with Rails API backend
---

AngularJS is a JavaScript based front-end framework developed by Google for the purpose of addressing the many challenges that come with single page applications. It follows MVVM (Model-View-ViewModel) as opposed to the classic MVC (Model-View-Controller) architecture that I began learning early in my journey as a software developer.

As part of this project I was tasked with building out dynamic updating of a single field of a resource. Ex: Allow changing of quantity in a shopping cart. This blog post will cover a particular problem I came across while I built this feature out. 

<code>Angular-xeditable</code> is a bundle of angular directives that allows you to create editable elements. This technique is also known as 'edit-in-place'. You can view the docs <a href="https://vitalets.github.io/angular-xeditable/" target="_blank">here</a>. This bundle is a great example of why Angular is such a fun and familiar framework, it reminds me of injecting ruby gems into a Rails application. 

After spending some time in the docs I decided to implement the form.

![Alt text](/assets/ss15.png)

As you can see here we have a simple form that displays the healthcare providers' location OR if there is no location "empty" inside of a span tag. When the user clicks to edit the form, a text box will pop up with the "location" text inside of it, prompting the user to edit the text. 

![Alt text](/assets/ss16.png) ![Alt text](/assets/ss17.png)

After "save" is clicked, instead of utilizing <code>ng-submit</code> we are using the <code>onaftersave</code> directive which calls my <code>editProvider</code> function in my controller with the passed in provider ID as a parameter. The function then calls on my provider service to send a PATCH with the json data for that specific provider and updates the database. Now at this point you're probably thinking this is way too straightforward... there has to be a catch. You are correct! 

The main challenge here was looking up the correct provider object by id. Since our application is a single page, all of the providers are listed through an array, which we call <code>ng-repeat</code> on to iterate and display each provider's data. Throw in filters and different search results and the server has no idea what the correct object is without its specific id if a user wanted to edit a provider. 

![Alt text](/assets/ss18.png)

Here I created a lookup object. It sets a key id for each provider's id in the array to the provider object itself as the value. To grab the object, I then set a variable <code>provider</code> equal to accessing the <code>lookup</code> object by passing in the id we obtained from the view. Then simply pass the <code>provider</code> variable into our service and the correct provider is updated!

______________

<i>I learned so much about modern web application development from building this SPA. This was definitely the most challenging part of the curriculum for me. If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out the full source code for this project on github [here](https://github.com/jamesnvk/openhealth)</i>