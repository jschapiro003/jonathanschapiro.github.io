---
layout: post
title:  "CoinSum Algorithm for Dummies"
date:   2015-07-29 20:03:49
categories: jekyll update
---

# Coin Sum: 
How the heck do you solve this thing?!

First, let's define what the coinsum problem actually is.
Here is how Project Euler defines it:

>In England the currency is made up of pound, £, and pence, p, and there are eight coins in general circulation:

>1p, 2p, 5p, 10p, 20p, 50p, £1 (100p) and £2 (200p).

>It is possible to make £2 in the following way:
>
1x£1 + 1x50p + 2x20p + 1x5p + 1x2p + 3x1p

>How many different ways can £2 be made using any number of coins?

For the longest time, this problem was Greek to me. However, I, just like you, sat and struggled with it until it started to make sense. 

Turns out, this problem revolves around the use of decision trees. A decision tree is a representation of all possible paths, or "decisions" that can be explored while trying to reach a specific outcome. In our case, we are aiming to find a combination of coins or decisions that add up to our expected total. 

Let's look at an example that is a simplified version of the coinsum problem:

>Say that we have a list of numbers [1,2,3] and we want to find all possible ways to find a total of 3:

> Our input will be [1,2,3], total = 3

>Our output will be [ [1,1,1],[1,2], [2,1], [3] ]

My first approach was to see if I could write a program to print out all possible decisions and to not worry about finding a decision path that adds up to the target. To do so, I referenced this amazing blog post by another Hack Reactor student, Yan Fan.[Recursion with Javascript](http://blog.fanofyan.com/recursion-with-javascript-pt-2/). In her post, she uses Recursion to print out all possible outcomes of a game of "Rock, Paper, Scissors". Similarly, we want to print out all possible combinations of numbers in our input array. 

Check out this decision tree I put together encompassing all combinations of numbers in our list, creating a tree of depth = 3

![decisionTree](/images/decisionTree.png?raw=true)


As you can see by the "Decision" labels, 1,2 and 3 are our main decision points. We use each of these numbers to start a new path of our tree. 1  compares itself to each of the numbers (1,2,3), 2 then compares itself to each of the numbers, and finally 3 compares itself to each of the numbers. This process continues recursively down each path with the size of the tree growing exponentially. 

Keep in mind that we do not actually start down the root 2 decision path until all of root 1 decision's children have been established. But, I believe that, the key take away here is that each root (1,2,3)  append to themselves each root (1,2,3). I know that is a bit of a mind twister, so grab a coffee and take a second to let that sink in. 

Now, lets think about how we can identify all branches of our decision tree that add up to our target total of 3. This is what the solution would look like pictorally (I hope I spelled that correctly...I'm a programmer).

![decisionTree](/images/solutionsTree.png?raw=true)

The yellow nodes in our decision tree identify paths that solve for a target total of 3. If we ever encounter a red node we know that our current total (the sum of all the nodes in the path) is greater than the target total. At this point, we know that we must backtrack to the last path down are decision tree that was not greater than the target total and continue on from there. We need to apply this sort of thinking to the coding we do in our final solution. 

As a matter of principle and understanding, I always like to represent my solution to any algorithm based problem with a diagram before trying to solve it through code. This allows me to really understand the problem and accurately layout my solution to said problem. Finally lets get to the code.



	var coinsum = function(denominations,total){
    //array to hold possible change combination
    var change = [];
    var currentChange = [];
    var makeChange = function(currentTotal,denominations,currentChange){

        if (currentTotal === total){
            //we've found a working combo
            change.push(currentChange);
            return;
        }
        if (currentTotal > total){
            //bad decison path, backtrack and move onto next path
            return;
        }

       
        for (var i = 0; i < denominations.length; i++){
            var currentDenom = denominations[i]; 
            makeChange(currentTotal+currentDenom,denominations,currentChange.concat(currentDenom));
            
        }
    }
    makeChange(0,denominations,[]);
    return change;
}


Let's walk through this line by line:


	
    //array to hold possible change combination//
    var change = [];

    //array to hold current path down the decision tree - constantly being updated//
    var currentChange = [];

    //recursive subroutine to traverse each node in the decision tree//
    var makeChange = function(currentTotal,denominations,currentChange)

    //check to see if the sum of the nodes in the currentChange array is equal to the targetTotal//
    if (currentTotal === total){
            //we've found a working combo
            change.push(currentChange);
            return;
     }

     //if you have gone too far down the decison path backtrack//
     //pro tip: by virtue of the fact that you are returning once entering this function, you are going to increment whatever step of the
     //for-loop you are currently in
     if (currentTotal > total){
            //bad decison path, backtrack and move onto next path
            return;
     }

     //peform the recursive subroutine on each one of the numbers in the denominations array//
     //this is what creates the 'roots' of our decision tree
      for (var i = 0; i < denominations.length; i++){
            var currentDenom = denominations[i];  //create 'root'
            makeChange(currentTotal+currentDenom,denominations,currentChange.concat(currentDenom));
            
      }

      //kick-off the recursive subroutine
       makeChange(0,denominations,[]);
       // return all possible decision paths
    	return change;

 This approach seems to work just fine when you substitute our naive values for coin denominations.

 And there you have it. I hope that this sheds some light on how to attempt problems like coinsum. 
 If you have any further questions or heaven forbid you find a bug, please feel free to email me at jschapir@gmail.com

 Cheers!







