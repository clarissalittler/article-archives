**Gateways to Computation: Logic gates and bits**

*Clarissa Littler*

In the last issue, we talked about the physics of quantum mechanics and the ways quantum computers calculate things. 

This time we're going to talk a little bit more about how the *hardware* of a computer works and how this relates to building quantum computers. 

To start, we're going to talk about the concept of "logic gates". These are the fundamental building blocks of how a processor is built. How fundamental? Well a typical modern CPU has *millions*\---some even billions---of logic gates. Each logic gate performs a specific operation on a few bits at a time. 

One of the first we'll introduce is the *and*\-gate. The *and*\-gate takes two bits and returns 1 if both of the bits it's given are 1, and 0 otherwise. 

In Python, you'd write it like this: 

def andGate(b1,b2):  
    if (b1 \== 1\) and (b2 \== 1):  
	return 1  
    else:  
	return 0  
So if you think of bits as "1" means true and "0" means false, then an *and*\-gate is basically the same thing as the and you use in *if*\-statements in Python\! There's similarly also an *or*\-gate that gives back a 1 if either—or both\!—of the bits you give it are 1. And the last important gates are the *not*\-gate that sends 0 to 1 & 1 to 0, and the *xor*\-gate \[read this as "ex or" for "exclusive or"\] that returns 1 if **only one** of the inputs is 1. 

From here, we can demonstrate something kind of cool: let's add two bits together using logic gates\! 

So as a reminder of how binary numbers work, a binary number is a series of 1 or 0 and you read them as *powers of two*. So 101 is 4 \+ 1 which is 5 or 0110 is 2 \+ 1 which is 3. With that we can add two bits together like this: 

0 \+ 0 \= 00  
1 \+ 0 \= 01  
0 \+ 1 \= 01  
1 \+ 1 \= 10

So if we look at the two output bits, we can notice an interesting pattern. The right output bit is 1 when *only one* of the input bits is 1. The left output bit is 1 only when *both* of the input bits are 1. Huh. Those sound kind of like logic gates\! If we were to write this as Python code we'd write something like: 

def halfAdder(b1,b2):  
    return (andGate(b1,b2),xorGate(b1,b2))

So you've got the start of a general addition function just from using two gates\! We call this a "half adder", though, because it only operates on one pair of bits at a time and doesn't easily chain together to add multi-bit numbers together. If you can understand how the half-adder works, though, then you're well on the way to understanding how to do all arithmetic with logic gates. 

Something to try: implement the xorGate function yourself and then test out this addition function on ones and zeros\! 

So now we come to quantum computers and qbits. Quantum bits, as we discussed in the last issue, aren't just "on" or "off", "1" or "0", but instead they store a *wave* that describes the *probability* the bit is a "1" or "0". 

These waves can interfere with each other, like noise cancelling headphones, and this allows for very different kinds of math than just adding bits together, and those operations will be carried about by *quantum* gates. Quantum gates are inherently more complex that the simple gates we’ve seen so far: for example, all quantum gates must be *reversible*\! 

What does that mean? Well, reversible operation is one you can undo: opening a backpack is reversible because you can close it. Turning left is reversible because you can turn right. Adding two is reversible because you can subtract two. Crushing a soda can isn't reversible because you can never get it completely back in its old shape. Multiplying by zero isn't reversible, because you can't recover the original number just by looking at zero. And here's the punchline: logic gates like the *and*\-gate and *xor*\-gate are **not** reversible, similarly to why multiplying by zero isn't reversible. If I tell you an *and*\-gate returned a 0 can you tell me what the inputs were? 

But if things like *and* and *xor* gates aren't reversible, how can we do math with a quantum computer? 

That's what we'll cover next time\! 