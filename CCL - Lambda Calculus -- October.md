**Lambda calculus**

*Clarissa Littler*

Programming languages are cool. There's so many and most of them are really different from one another\! We've covered a lot of really interesting ones so far: languages that treat pictures as programs, languages designed to run on mobile devices, languages designed to do computing fast, and many others. 

Now, we're going to talk about a programming language *completely* unlike everything else we've seen but one that's still exerting influence today: the lambda calculus. 

The lambda calculus is **old**, old enough that it predates computers. It was invented by Alonzo Church, a mathematician, in the *1930s*. You may not have heard of Church before, but you've probably heard of one of the students that worked for him: Alan Turing\! There's a neat connection here between Turing's work and Church's lambda calculus. You see, Turing came up with what we now call "Turing machines" as a way of figuring out what you *could* do with a machine that calculates. That may be surprising, but even though computers didn't yet exist, the idea of a machine that could do math had been around since the early 1800s when people like Ada Lovelace wrote the first algorithm for a *very* hypothetical computer called the Analytical Engine. 

Church, on the other hand, tried to answer the question of the limits of computers by inventing a symbolic system, the lambda calculus, for doing calculations. It's a kind of "algebra" of computation, where each expression you could write down in the lambda calculus *executes* to perform a complex calculation. In other words, it's a language for *programs* you can write down that can be executed to calculate a number. It's a programming language, though a special one that was meant to be calculated by hand instead\! 

That's enough of a preface. What's it actually *look* like? Well here's how you write the numbers 0 through 3 in the lambda calculus 

0 \=λ s. λ z. z

1 \=λ s. λ z. sz

2 \=λ s. λ z. s (s z)

3 \=λ s.λ z. s (s (s z))

And here's an if-else-statement in the lambda calculus 

if \= λ b. λ t. λf. b t f

And here's how you write a while-loop, call the Y-combinator\! 

Y \= λ f. (λx. f (x x)) (λx. f (x x))

Now, you're probably looking at those and thinking "how are these numbers or if-statements or loops?" well they key to the lambda calculus is that it's super-minimalist. Everything is a function in the lambda calculus. An *anonymous*, unnamed, function. This means you’re going to have to think really differently about what things like numbers *mean*.

If you've tried Python or JavaScript you may have seen *anonymous* functions before. In Python, they look like lambda x: x \* 3. In JavaScript they look like 

function(x) {return x \* 3};

Notice the literal word lambda in the Python example? Yeah, that's a reference to the lambda calculus\! 

Now JavaScript and Python have other programming constructs and data in their programming language. The lambda calculus, on the other hand, is *only* its anonymous functions. 

Numbers? Anonymous functions. Booleans? Anonymous functions. While-loops? Anonymous functions\! 

Everything is a function. 

We can break the syntax of the lambda calculus into three pieces, then: 

* defining functions 

* applying functions 

* using variables 

Defining functions always looks like 

λ x. l

where by the lambda symbol, λ, signifies "hey, we're starting to define a function", by *x* we mean *any* letter, which is going to be the *argument* to the function, and the *l* means the body of the function. 

Applying a function just means you write two (or more) things next to each other. So up above we have a part of a function that reads as 

λ x. f (x x)

The *body* of this function reads as "apply *f* to the result of applying *x* to *x*". 

Finally, you use a variable just by writing the variable. In our previous example, *x* is a use of the variable *x* we’ve set aside in the declaration 

λ x. . . .

Okay\! So we've completely described how you write down lambda calculus programs, but how do you *run* them? 

If the only thing in the language are *functions* then the only thing you could possibly do with these functions is call them\! The fact that everything is a function in the lambda calculus can make it look more complicated than it is. Instead, let's consider the following JavaScript expression 

(function(x) {return 2\*x;})(10)

what happens when this code is run? It runs the *body* of the function with the argument x replaced by 10 everywhere. In this case, the function returns 20. 

Applying functions in the lambda calculus works exactly the same way\! You just eat an argument and *substitute* it into the body of the function. 

There's only one weird edge case here. If you have something like 

(λ s.λ z. s (s z)) z

then what does this become? At first glance it looks like it might become 

λ z. z (z z)

but that's not right because the two different variables named *z* have different scopes, in other words they were defined in two different places. Going back to JavaScript this is like how the following program 

var y \= 10;  
var funny \= (function(x) {return (function(y){console.log(y\*x)});})(y);  
funny(3);

prints out 30 because the y you define on line 1 isn't the same thing as the y in the function definition on line 2\. 

In the lambda calculus, though, there's no automated system to keep track of scope and whether two variables just happen to have the same name but are different\! Instead, there's a rule in the lambda calculus that *if* variables would get confused like up above you just rename the offending variable. 

So instead of 

(λ s.λ z. s (s z)) z

you rename the *z* to something not already in use 

(λ s.λ q. s (s q)) z

So now when you reduce this function you get 

λ q. z (z q)

There\! That fixes the problem. 

We're finally ready to explain how in the world these functions 

0 \=λ s. λ z. z

1 \=λ s. λ z. s z

2 \=λ s. λ z. s (s z)

3 \=λ s. λ z. s (s (s z))

count as numbers\!

If you look at them you’ll see that each of these “numbers” follows a pattern: each takes two arguments, an *s* argument and a *z* argument. We define 0 as a function that throws away its *s* argument and returns its *z* argument unchanged. We define 1 as a function that applies its *s* argument once to its *z* argument. Similarly 2 and 3 are the functions that apply their *s* argument to their *z* argument two and three times, respectively.  

Sounding it out, the idea is that a *natural number*, which is either zero or a positive whole number, represents the ability to do something multiple times. A kind of for-loop\! The number 3 "is" the ability to do something, anything, three times. The number 0 means do nothing, leave things the same. 

Okay, but you might be asking yourself "if these are numbers, how can I do math with them?" There's actually a good answer for that\! 

We can start by explaining how to *add one* to a number in the lambda calculus. If a number *n* is "do something *n* times" then adding one means "do it one more time". So that looks like 

addOne \= λ n. λ s. λ z. s (n s z)

Go ahead and try applying the function *addOne* to some of those numbers. Just try doing it pen & paper. You should see that it does exactly what we want. 

Well if we can add one, then we can define addition\! What's addition, after all? It's just writing adding one repeatedly\! In other words, 5 \+ 4 "means" add one to four a total of five times. Luckily, we have something that means "do something repeatedly": numbers\! 

This means that 

add \= λ n λ m. n addOne m

Again, if you try it out you can prove to yourself that addition really works *even when all you have is functions*. 

There's so much more to play with and learn about here, but we'll leave this for now and instead I'll say you should read the links provided and try making programs in the lambda calculus yourself\! 

Further reading:

* A technically heavy but concise introduction that goes further than we did: [http://www.inf.fu-berlin.de/lehre/WS03/alpi/lambda.pdf](http://www.inf.fu-berlin.de/lehre/WS03/alpi/lambda.pdf)  
* A very light metaphoric way of doing lambda calculus computations: [http://worrydream.com/AlligatorEggs/](http://worrydream.com/AlligatorEggs/)  
* The wiki entry on the lambda calculus is actually really helpful: [https://en.wikipedia.org/wiki/Lambda\_calculus](https://en.wikipedia.org/wiki/Lambda_calculus)

