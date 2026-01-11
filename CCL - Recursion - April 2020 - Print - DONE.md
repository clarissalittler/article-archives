**Recursion: Following the shape of data**

*Clarissa Littler*

Software programming has a number of ways to solve problems that can be described as shapes using mathematics. For example, many programming languages have looping in the form of For and While statements. These statements repeatedly loop through data if a condition is met until the condition no longer exists. Some languages use recursion instead of loops to work through a problem until it is solved.

Recursion is one of the foundational tricks for solving problems, on a computer or otherwise. Even if you've never heard the word before you may have seen the idea\! 

Basically, recursion is when you break a problem into smaller parts you can solve individually in order to solve the bigger problem. Recursion is *also* when you have something that references itself, like the joke Google pulls if you search for the word "recursion" 

 

These two definitions are *really the same thing*, which we're going to demonstrate with a little math example: the factorial function. 

If you *haven't* seen the factorial before it's kind of the "Hello World" of recursion, a simple exercise that demonstrates an important concept. We write the factorial of a number like 5\! or 10\! and what the factorial *does* is this 

5\! \= 5\*4\*3\*2\*1 

10\! \= 10\*9\*8\*7\*6\*5\*4\*3\*2\*1 

The value of all the elements of 5\! multiplied together, one element after another, is 120 while the value of 10\! is 3,628,800.

In terms of a *generic* number n we could define factorials as 

n\! \= n\*(n-1)\! 

Oh, that's a nice and short definition isn't it? So what about making the factorial in, say, Python? If you *don't* want to use recursion you're going to need to write a factorial function like 

def fact(n):  
    total \= 1  
    for i in range(n):  
	total \= total\*(n-i)

    return total

\# this should print 120  
print("5\! is %d" % (fact(5)))

and this isn't *wrong* but it's not super obvious why it's *right*. 

Let's use recursion instead of a for-loop: 

def fact(n):  
    if n \> 1:  
	return n\*(fact(n-1))  
    else:  
	return 1

print("5\! is %d" % (fact(5)))

Neat\! This matches closer to how you'd define the factorial in math and, in my opinion, is a little bit easier to read and tell what's happening.

So recursion is a way of writing code that is sensitive to the *shape* of the data you're working with, for solving complex problems by breaking them into simpler parts. There's even more to it, though, like how to make recursive functions run really efficiently—more efficiently than even loops—with things like *tail recursion*. If you want to know more or see more examples check out the links in the rest of the magazine and the article on Snap\! in this issue\!

Further reading:

* Tail Recursion: a way that some languages make recursion more efficient [https://lesleylai.info/en/tail-recursion/](https://lesleylai.info/en/tail-recursion/)  
* 