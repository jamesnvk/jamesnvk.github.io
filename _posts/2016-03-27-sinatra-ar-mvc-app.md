---
layout: post
title: Sinatra ActiveRecord MVC Application
---

I've learned a ton since I built my first CLI gem in my last project. Flatiron School's Full Stack Dev curriculum really knows how to keep us just on the edge of our knowledge - Always challenging and I'm absolutely addicted. This project's requirements are as follows:

## REQUIREMENTS
+ Build an MVC Sinatra Application.
+ Use ActiveRecord with Sinatra.
+ Use Multiple Models.
+ Use at least one has_many relationship
+ Must have user accounts. The user that created the content should be the only person who can modify that content
+ Models must have validations to ensure that bad data isn't created
+ Any validation failures must be shown to user with an error message

I decided I wanted to build a game collection app that keeps track of a users games. When I was younger (the days before Steam was a thing) I had a ton of games on PC/DVD, SNES, N64 and no where to keep track of them! My first task is to determine file structure, more importantly.. which gems I will be needing to create this app. ![Alt text](/assets/ss1.png)

Next let's build out the models. A User <code>has many</code> games and a Game <code>belongs to</code> a user. We're being taught that starting out with the models first is a great pattern for building web apps from scratch. This way we can directly interact with our data first before committing to building out the larger portion of the framework like the controllers and routing. We can always come back to add attributes or functionality to the models in the future as well.

Now let's setup our database. We have to create 2 tables, one for users and one for games. We're going to run <code>rake db:create_migration NAME=create_users</code> and do the same for games. Our code in our migration file will look like this: ![Alt text](/assets/ss2.png)

We're creating 3 columns for our 3 attributes: Games have a name, year, and a foreign key: <code>user_id</code> since games <code>belong_to</code> a User. We'll do the same for Users then run <code>rake db:migrate</code> to execute the changes. After our tables are setup we'll need to add our 2 models to our app. ![Alt text](/assets/ss3.png)

With our tables and models setup and migrated our Users and Games are now associated. Remember that the model that has belongs_to will always have the foreign key. In this case, our Game model has the foreign key <code>user_id</code>.

Let's start with the User class. We're <code>include</code>ing instance method <code>slug</code> that will take a user's username, downcase it, and replace all spaces with dashes. That's the beauty of ruby.. we can just look at the method and know exactly what it does. The purpose of this method is to have our URLs remain RESTful. Next we're <code>extend</code>ing our class method <code>find_by_slug</code> that will give us the ability to find a user by their slugified name.

<code>has_secure_password</code> is a macro given to us by ActiveRecord. However in order to use this we will need to have <code>sessions</code> enabled and also our gem <code>bcrypt</code> that we installed earlier. <code>Bcrypt</code> gives us the ability to store a salted and hashed version of a user's password in a database column called <code>password_digest</code>. Let's add that now.  ![Alt text](/assets/ss4.png)

To wrap up user auth we are given a method <code>authenticate</code> that is provided to us by the Bcrypt gem, which takes a string as an argument. If the string password matches the string password in the password digest, it will return the user object, otherwise it will return false. ![Alt text](/assets/ss5.png)

We ensure that bad data isn't being passed with our helper methods <code>logged_in?</code> which evaluates the truthiness of a session[:id] and <code>empty_field?</code> which ensures that a user fills out all form fields when logging in or signing up. Since the our session hash persists across our URLs, it is a very useful tool allowing a web app to persist a user across the entire scope of the application. In other words, the user does not have to log in every time they request a new page. This introduces "state" in an otherwise stateless web. Check out all of my controller routes and actions on my full [github repo](https://github.com/jamesnvk/game-collection-sinatra-app).

For our last requirement I decided to use the flash gem found [here](https://github.com/SFEley/sinatra-flash). This cool little gem adds an error message for the user when they fail a validation.

##Conclusion

I learned a ton about how the web operates doing this project. It was a lot of work and I'm glad that I'm learning a basically smaller version of Rails before moving onto the behemoth. Feel free to send me an email jamesnovak90@gmail.com I'd love to hear from you!

