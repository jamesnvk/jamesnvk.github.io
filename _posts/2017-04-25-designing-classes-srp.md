---
layout: post
title: Designing Classes with a Single Responsibility
---

### Classes
The goal of modeling classes is to keep it simple enough to do what it is supposed to right now, and is also easy to change later. Design is more of the art of preserving changeability than it is the act of achieving perfection.

### Single Responsibility
Applications that are easy to change consist of classes that are easy to reuse. A class that has more than one responsibility is difficult to reuse. A class should do the smallest possible useful thing. Try to describe what the class does in one sentence. 
SRP doesnt require that a class only do one very narrow thing - it requires a class be cohesive - that everything the class does be highly related to its purpose.

Same things apply to not only classes but methods - Ask them questions about what they do and try to describe their responsibilites in a single sentence.

### Design decisions
When the future cost of doing nothing is the same as the current cost, postpone the decision. Applications are never perfectly designed, every choice has a price. “Improve it now” vs “improve it later” tension always exists.
Depending on behavior and not data - behavior is captured in methods and invoked by sending messages.
Use attr_accessors to encapsulate methods for only that class. Implementing these changes that data (which is referenced all over) to behavior (which is defined once).

### Direct references into complicated data structures are a maintenance nightmare, because every reference will need to be changed when the structure of the data structure changes.
Example: ​
<pre><code>@data -> [[622,20], [622,23], [559,30], [559,40]] 
def diameters
  data.collect{|cell| cell[0] + (cell[1] *2)}
end</code></pre>

​Creating a struct can solve this problem by defining a method that understands the structure of the incoming data structure, so that we only have to change the code in that one place if the data structure happens to change. (if its externally owned data etc.)

The path to changeable and maintable objected oriented software begins with classes that have a single responsibility. Classes that do one thing isolate that thing from the rest of your application. This isolation allows change without consequence and reuse without duplication.

______________
If you like what you read you can check out my previous posts listed in my [archive](https://jamesnvk.github.io/archives/). Or you can check out my github <a href="https://github.com/jamesnvk/" target="_blank">here</a>.