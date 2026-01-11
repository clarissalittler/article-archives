**Closures: The cutest trick you haven’t heard of**

*Clarissa Littler*

There's a really neat little feature hidden inside a bunch of different languages, one that you may have never heard of by name even if you've used it without knowing: closures. 

Any language that has 

1. variables, that is a way to name and store data to use later

2. first-class functions, that is functions that you can return as values or bind to variables 

has closures\! We need to explain a few concepts in order to make sense of it all, though. First, we need to talk about *variable scope*. The *scope* of a variable defines where the variable is well-defined and how you figure out, if there are multiple variables in a program with the same name, which piece of data you-the-programmer are trying to use. 

So for example, if you have a Lua program that reads as 

x \= 10  
function doofyFun(x)  
   local x \= 20  
   return x  
end

print(doofyFun(30))  
print(x)

you have three different uses of the variable x. Can you name them all? Which one actually gets returned by doofyFun and printed out? Here's another question for you: what value is going to be printed by the last line? 

The answer to the first question is that in the  return x is going to only see the most recently defined x, the one closest to it. In this case, that's the x made in the line local x \= 20. This is an example of what we call shadowing\! The answer to the second question gives us an interesting twist. When we change an x inside doofyFun it *can't* affect the x declared at the beginning. It starts the program with a 10 inside it and it ends the program with a 10 inside it. 

This tells us that data defined inside functions are in some sense *invisible* to the rest of the program. But what happens to these variables when the function has run and is done? Well, **normally** they're *garbage collected*—a concept that we've touched a couple of times in past issues. This means that because no other code can *reference* these variables anymore, in other words they're not *in scope* for anything else in the program, then the language implementation knows it can just free up those containers of data to be recycled for other variables the program might make later. 

What if, though, you have something like the following program 

function newCounter()  
   local c \= 0  
   return function ()  
      c \= c \+ 1  
      return c  
   end  
end

counter \= newCounter()

print(counter())  
print(counter())  
print(counter())

This is doing something kinda neat\! We have a function newCounter that first defines a new variable, c, and sets it to 0\. Then it *returns* a *function*. What does this function do? Well every time it's run it adds one to the variable c and then returns the value inside c. 

We then make a counter with the newCounter function and call it inside three calls to print. Any guess what this does? Try it yourself, or try the equivalent Python code at the repl.it website if that's more convenient. 

def newCounter():  
    c \= 0

    def inner():  
	nonlocal c  
	c \= c+1  
	return c

    return inner

counter \= newCounter()  
print(counter())  
print(counter())  
print(counter())

The cool trick here is that since you're referencing the variable c inside the "inner" function then it can't get garbage collected, but it's visible to *only* the inner function. In other words, the inner function has "closed" over these variables that no one else can see or use. That's why the inner function is called a closure\! 

You can test this by making two *different* counters with the newCounter function. If you increment each of these counters you'll see that they increase separately: two different c variables each visible to exactly one counter. 

Okay, that's a neat trick but what's it good for? Well, it's common in a lot of programming\! JavaScript libraries in particular are famous for using closures everywhere, but you'll notice it all over the place once you've seen the pattern once. If you haven't read it yet, try reading the Roblox article in this issue and see if you can spot some places where I snuck in closures to make the code easier\! 