---
layout: post
title:  "Java Abstract Class vs. Inheritance"
date:   2016-03-29 20:03:49
categories: jekyll update
---
The other day I was asked by a colleague if I knew the difference between and abstract class and an interface. I paused for a minute. Come to think of it, there
was a time and place when I knew such a difference but these days, I work primarily in languages like javascript and ruby and don't see such concepts utilized.
With that said, it's time for a refresher. This article published on wideskills.com reminds of what abstract classes and interfaces are and when you would use each.
The tutorial is written in Java as an fyi. When talking about abstract classes, I love the example of a Shape as the base abstract class. You can think of it as, "I don't think I
would ever need to instantiate a shape but, I would need to instantiate a triangle that has defined characterists of a shape". An abstract class allows you to layout a blue print for shapes and defining a triangle class allows us to implement the more definitive characteristcs of that particular shape. 

Interfaces are nice because they solve the problem of multiple inhertiance in Java. A class can easily implement multiple interfaces but can only extend a single abstract class. 

Tying it together, here is a great Stack Overflow example of using an abstract class and interface together:
  
  "How about an analogy: when I was in the Air Force, I went to pilot training and became a USAF (US Air Force) pilot. At that point I wasn't qualified to fly anything, and had to attend aircraft type training. Once I qualified, I was a pilot (Abstract class) and a C-141 pilot (concrete class). At one of my assignments, I was given an additional duty: Safety Officer. Now I was still a pilot and a C-141 pilot, but I also performed Safety Officer duties (I implemented ISafetyOfficer, so to speak). A pilot wasn't required to be a safety officer, other people could have done it as well.
  All USAF pilots have to follow certain Air Force-wide regulations, and all C-141 (or F-16, or T-38) pilots 'are' USAF pilots. Anyone can be a safety officer. So, to summarize:

  Pilot: abstract class
  C-141 Pilot: concrete class
  ISafety Officer: interface
  added note: this was meant to be an analogy to help explain the concept, not a coding recommendation. See the various comments below, the discussion is interesting." - Jay

Key Points: 
  Abstract class is a class which contain one or more abstract methods, which has to be implemented by sub classes. An abstract class can contain no abstract methods also i.e. abstract class may contain concrete methods. A Java Interface can contain only method declarations and public static final constants and doesn’t contain their implementation. The classes which implement the Interface must provide the method definition for all the methods present.
  


[Java Abstract Class and Interface](http://www.wideskills.com/java-tutorial/java-abstract-class-and-interface/p/0/1) 












