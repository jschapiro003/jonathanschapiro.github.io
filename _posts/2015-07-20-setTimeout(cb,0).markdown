---
layout: post
title:  "setTimeout() with no delay?!?! - The Javascript Event Loop"
date:   2015-07-07 20:03:49
categories: jekyll update
---
What we have here folks is a very tricky interview question and, if you are heavy into asynchronous code, an extremely important piece of information. The question this blog post aims to address is, what is the result of this code snippet and how does the code behave with relation to the `Javascript Event Loop`?



		foo();
		setTimeout(function(){				
			console.log('hello world');
		},0)
		foo();



Many of you might expect that the output of this code will be:
	

		//the return value of foo()
		//'hello world'
		//the return value of foo()

	
Unfortunately, you are quite mistaken. The actual output of this code regardless of the 0 second delay is:
	

		//the return value of foo()
		//the return value of foo()
		//'hello world'

	

It turns out that, regardless of whether or not the delay of a setTimeout function is 0, the execution of the callback function provided to said function waits for the call stack to be empty in order to execute the callback.



Let's dive a little deeper. Refer to this link: [Loupe Javascript Runtime](http://latentflip.com/loupe/?code=ZnVuY3Rpb24gZm9vKCl7CiAgICBjb25zb2xlLmxvZygnZm9vJyk7Cn0KCmZvbygpOwpzZXRUaW1lb3V0KGZ1bmN0aW9uKCl7CiAgICBjb25zb2xlLmxvZygnaGVsbG8gd29ybGQnKTsKfSwwKTsKCmZvbygpOw%3D%3D!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)
  and have it off to the side for reference.

As you can see, when we run the code snippet, we notice this ordering:

	1) foo gets added to the call stack.
	2) foo executes console.log('foo')
	2) the setTimeout function gets added to the Event Listener Hash (aka 'Web API's section') and its callback gets added to the Callback Queue. 
	3) the second invocation of foo gets added to the call stack
	4) the second invocation of foo executes console.log('foo')
	5) the call stack is now empty
	6) we now check to see if there is anything in the Callback Queue
		6.1) there is, so we dequeue whatever is in the Callback Queue (the callback provided to the setTimeout function)
	7) fin

I hope that this clears up any confusion regarding what happens when we give setTimeout a delay of 0!
Thanks for reading!

Additional Resources:
	[Philip Roberts - Loupe Javascript Runtime Visualizer](http://latentflip.com/loupe/)
	&&
	[Philip Roberts: What the heck is the event loop anyway?!](https://www.youtube.com/watch?v=8aGhZQkoFbQ)










