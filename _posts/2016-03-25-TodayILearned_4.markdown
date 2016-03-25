---
layout: post
title:  "Let's Build A Web Server Part 2"
date:   2016-03-23 20:03:49
categories: jekyll update
---
In today's article, we are continuing where we left of from yesterday's "How to Build a Web Server Part 1".
The article discusses the idea of a WSGI (Web Server Gateway Interface), the mechanism through which multiple
frameworks can utilize the same web server. Really awesome stuff and not too difficult.

Summary: 
  First, the server starts and loads an ‘application’ callable provided by your Web framework/application
  Then, the server reads a request
  Then, the server parses it
  Then, it builds an ‘environ’ dictionary using the request data
  Then, it calls the ‘application’ callable with the ‘environ’ dictionary and a ‘start_response’ callable as parameters and gets back a response body.
  Then, the server constructs an HTTP response using the data returned by the call to the ‘application’ object and the status and response headers set by the ‘start_response’ callable.
  And finally, the server transmits the HTTP response back to the client

Thanks again to Ruslan for this awesome post

[Let’s Build A Web Server. Part 2.](https://ruslanspivak.com/lsbaws-part2/) 












