---
layout: post
title: Building a CLI Gem
---

<div class="message">
  My first Ruby CLI Gem: Train Hard
</div>

My idea for this gem is fairly straightforward. It is a command line interface that scrapes from a website that lists exercises by muscle groups. Each muscle group has exercises, and each exercise has a rating. Later in the process I would like to add functionality that displays only exercises based on a certain rating criteria.

The first order of business is to bust out the notepad and organize the project into small bite sized pieces. Here's what I got (shoutout to Avi ;))

1. Plan your gem, imagine your interface
2. Start with the project structure - google
3. Start with the entry point  - the file run
4. Stub out the interface
5. Start making things real. Discover objects. PROGRAM.

Alright! Lets get started shall we? 

## 1. Plan your gem, imagine your interface

A CLI seems like a fairly simple idea. The program asks a user a question, and the user responds to the question with the correct input. So when we first run our gem we want to ask our user an important question (one which they want to be asked since they installed the gem, and one that is concise and to the point.)

    Which muscle group are you training today?

Using <code>gets.strip</code> we can determine by number, which muscle group a user wants to see exercises for, then display that list to the user. We will of course list those muscle groups by number.

## 2. Start with the project structure

<code>bundle gem train_hard</code>

Magic! We now have a brand new directory with all of our necessary files to create a gem.

## 3. Start with the entry point

In our <code>bin</code> directory is where we want to encapsulate all of our code into a simple call to execute our program. It seems to be best practice not to place logic in this directory. I added <code>#!/usr/bin/env ruby</code> to tell the interpreter that this is a ruby file. I also added <code>require './lib/train_hard'</code> since we will be needing our <code>cli.rb</code> class to run the file.

In our <code>lib</code> directory is where the meat of the program lies. We have a file called <code>train_hard.rb</code> that is responsible for loading all the required files including our <code>nokogiri</code> gem and <code>open-uri</code>.

##4. Stub out the interface

Our program should start just by running <code>./bin/train_hard</code> command. Inside our bin/train_hard file we should only have code that looks like this to encapsulate our logic and run our program 
<div class = "message">
#!/usr/bin/env ruby<br />

require "bundler/setup"<br />
require "train_hard"<br />

TrainHard::CLI.new.start
</div>

Our first method that is going to be run in our CLI is our <code>display_menu</code> method which displays a menu for the user to choose which muscle group they would like exercises for. For now, we are going to hard-code our method just to be able to have a visualization of what the program will look like before it becomes real. For example
<code>puts "Which muscle group are you training today? (enter number):"</code><br/>
<code>
def display_menu<br />
  puts "Which muscle group are you training today?:"<br />
  puts <<-DOC<br />
  1. Chest<br />
  2. Back<br />
  3. Legs<br />
  4. Shoulders<br />
  5. Abs<br />
  6. Arms<br />
    DOC<br />
   end
 </code>

 Let's do the same for our <code>pick</code> method, which will <code>gets</code> from a user to enter the number which they would like to train, then based on that number display that muscle's exercises. Example:<br />
<code>
  def pick<br />
    input = nil<br />
    while input != "exit"<br />
    puts "Enter number of the muscle you would like to train or type menu to display menu:" <br />
    input = gets.strip <br />
      case input <br />
      when "1" <br />
      puts "Exercises for 1" <br />
      etc...
</code>

Now that we have our code stubbed lets start actually programming!

##5. Start making things real. Discover objects. PROGRAM.

The fun part! The first thing we have to do is figure out what exactly a "muscle" consists of, and what our <code>muscle class</code> is going to do for us. 
What is a “muscle” ?
What is an "exercise" ?
1. A muscle has a name 
2. A muscle has many exercises.
3. An exercise belongs to a muscle.
These can be represented here in <code>class Muscle</code>: <code>attr_accessor :name, :exercises</code>.<br/>
<code> class Exercise </code> <br/>
<code> attr_accessor :name, :muscle </code>

Next we want to be able to build a muscle object by scraping it off of a website. Our goal is to find all the muscles we want to include and for each muscle, create a muscle instance. To do this we are going to need a separate <code>Scaper</code> class, since a muscle class's responsibility is to create instances of muscles, not scrape information. In our scraper class we are going to define a <code>get_page</code> method and setup our <code>Nokogiri</code> with our index url. Read more about Nokogiri and open-uri [here](http://ruby.bastardsbook.com/chapters/html-parsing/)

Our scraper is going to be split into 2 parts. First we will want to scrape the index page for all the muscles that are available. Then we will want to dive deeper and scrape the exercises within those muscle pages. So our first method will just scrape the index page for all the muscle titles, get just the text from those titles and push those strings into an array. Here is the code to accomplish this: <code>self.get_page.css('.muscle-pagination li')[0].text,</code>

Here we can see that we are calling the get_page method within <code>scrape_muscles_index</code> to parse the HTML page, then retrieve the specific text from the HTML and push that string into an array. We will be doing the same thing for the exercises, but since there are a lot of exercises we need to add another process.<br/>

<code>self.get_page.css('.exerciseName h3 a').collect {|exercise| exercise.text.strip!}</code> Here we are collecting all of the exercises listed on the page (just the text), then using the <code>strip!</code> method to remove any trailing and leading whitespace, then push that array of strings into a separate array.

Next after we gather our raw data we are going to need to create objects out of them. Let's start with muscles. Our muscles are an array of strings. We need to take each muscle from that array and instantiate it into an object, then push that new muscle instance into a class constant called <code>@@all</code>. this is where all of our muscles will reside so we can reference them later. Going back to instantiating objects, like we learned earlier, A muscle has many exercises, so in our <code>initialtize</code> method we are going to set an instance variable <code>@exercises</code> set to equal an empty array. In other words every new muscle object that gets born will have an empty "pocket" for exercises to be added to it. Then we will push <code>self</code> into <code>@@all</code>.

After our muscle objects are instantiated and pushed into that <code>@@all</code> we are going to create make and add the exercises as objects using our scrape exercises scraper method. Let's do this by reference each index in <code>@@all</code> like so: <code>@@all[0].exercises = SCRAPED_EXERCISES[0].collect {|exercise| TrainHard::Exercise.new(exercise, @@all[0])}</code></br>
Let's break this code down. First we are referencing the first muscle that has been instantiated in <code>@@all[0]</code> which happens to be Abs. Then we are calling the <code>.exercise =</code> method created by our <code>attr_accessor :exercise</code> and setting it equal to <code>SCRAPED_EXERCISES[0]</code> which is reference our first array of arrays which contains a bunch of our exercises as strings. For each of those exercises we are instantiating a new exercise object and setting its name equal to the exercise and its muscle as the second argument equal to its corresponding muscle <code>#@@all[0]</code>

And that's it! The bulk of our design structure is done. We now have muscle objects that have many exercises, and exercise objects that belong to muscles. We can implement this structure within the CLI and have the user obtain real object data if we wanted to add more features down the line.






