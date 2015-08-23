---
layout: post
title:  "Testing Your iOS Apps without a Developers Account"
date:   2015-08-21 20:03:49
categories: jekyll update
---

#Testing Your iOS Apps without a Developers Account
Howdy folks. Amazing news! You no longer need a Developer's Account to test your apps on your iPhone. 
It's taken Apple 7 years to allow it, but the time has finally come. Unfortunately, I am a bit late to the game as I have not done iOS development for some time now. Nevertheless, I was recently building something in Ionic and needed to test it on an actual device. Here's how it's done: 

1. Make sure to download Xcode 7 beta 5 [Download Here](https://developer.apple.com/xcode/downloads/)
2. Navigate to your Xcode project that you would like to run on your device
3. Select your project in the project navigator 
![projectNavigator](/images/projectNavigator.png?raw=true)
4. You should now be shown the target display for your project
![badBundle](/images/badBundle.png?raw=true)
5. Navigate to the General tab
6. Select or add your name from the Team dropdown in the identity section
![goodName](/images/goodName.png?raw=true)
7. You may be prompted to "Fix issue" as "No matching provisioning profiles found"
8. Click "Fix Issue"

> An odd bug I encountered when building my Ionic App was when trying to build it. Upon building the app, a series of numbers was added to the Bundle Identifier. This prevented me from running the app on my phone. Removing the numbers fixed the issue. 

9. Now you are good to go. Choose your device from the dropdown menu and clikc the play button.
![runApp](/images/runApp.png?raw=true)



I hope this helped. I know it helped me. Just trying to pass on some tips.
If you have any questions or corrections, send an email to me at jschapir@gmail.com
