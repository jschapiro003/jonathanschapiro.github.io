---
layout: post
title:  "React Native Lessons Learned"
date:   2015-09-01 20:03:49
categories: jekyll update
---

# React Native Lessons Learned
----------------------------------------------------------------------------------------------
### What did I learn when building a React Native App?

Ok so here's the deal. I'm in the process of building a React Native App and I wanted to share with you some of the lessons that I learned along the way. Each of these topics will hopefully be built out into their own blog post but for now, I find it valuable to put the knowledge out there.


# Common Mistakes
###    1) Choose the correct IP address when loading your application from the development server. If you want to run the app on your phone this is super important.
    - You can get your IP by running ifconfig in your terminal
         - Look for the inet value under en0
         - THIS CHANGES WHEN YOUR WIFI NETWORK CHANGES!!!!
         - When you change WIFI Networks re-run ifconfig and change your ip value
         
###    2) Remember to add main.jsbundle to your project if you would like to bundle the app
        - It is not enough to uncomment jsCodeLocation = [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"]; and run react-native bundle
        - You must also include the main.jsbundle file in your Xcode project
        - Once this is done, you can bundle the app to your iPhone!
        
# Helpful Hints
### 1) ViewDidAppear does not exist! 
        - For those of you that are not coming from an iOS background, ViewDidAppear does the following : Notifies the view controller that its view was added to a view hierarchy.
        -In the definition above, for conversation sake, substitute view with component and view hierarch with index in your navigator. They are not directly equivilant but I think that it can be explained in such a way. 
        - I felt that without componenet lifecycle methods like, ViewDidAppear, it was difficult to reload relevant data at appropriate times. It would be nice to be able to trigger viewDidAppear and reload data from my apps server. For example, I would like for every time a component that displays a user's newest events data comes into view, a Fetch request is made to  my app's API and have the event data be refreshed. I had to come up with somework arounds for such instances (see section about callbacks)
  
###    2) Callbacks are your friend
        - If you would like to call a parent component's method after something has completed in a child component, pass the callback as a property of the child. For example (por ejemplo), we have Parent A and Child B. When we decide to pop Child B off the navigator stack, I would like for a spinner to start spinning in Parent A. As mentioned in helpful hints 1), we do not have a viewDidAppear method to trigger to us that we have arrived back at Parent A. To simulate such behavior, we will pass Parent A's startSpinner() method as a property of Child B. When we are done in Child B we will call ChildB.props.startParentsSpinner(). This will execute Parent A's startSpinner method solving the viewWillAppear.
        
###    3) The ref string
        - Lets say you've got Parent A and Child B components. What happens if you want to call a method of Child B from Parent A? Use the ref string. 
        - Declare <ChildB ref={'childb'}/> in ParentA
        - You can call any method on this.refs.childb with in Parent A.
        -Problem solved!
        
###    4) Conditional components
        - I found it very helpful to use ternary operators to determine what value you would like a specific component to hold.
        - var componentToUse = dataLoaded ? <dataLoadedComponent /> : <dataNotLoadedComponent/>
        - I used this in a tab bar scenario where I only wanted to load a camera component if the current tab was the camera tab. This helped alleviate some performance issues of having the camera component constantly loaded. A true life saver.

