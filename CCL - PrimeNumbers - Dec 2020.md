1. **Finding prime numbers for fun and profit**

2. 

Prime numbers are one of those fun little things in mathematics that start so simple but end up being so important, not just to math but to programming as well\! By the end of this article we're going to explain why certain numbers are so vitally important to talking, shopping, and existing online safely.

So first let's review what *prime numbers* are. They're integers, whole numbers, other than 1 that can **only** be evenly divided by themselves or by 1\. What I mean by evenly divided is giving a whole number as a result. So 6/2 evenly divides into 3, but 5/2 doesn't because 5/2 is 2.5.

Some really quick examples: 2 is prime, 3 is prime, but 4 *isn't* because 4/2 is 2\. The reason why mathematicians and computer scientists alike care about prime numbers is that every whole number is either a prime number or can be represented *uniquely* as a product of prime numbers. What "uniquely" means here is that there aren't choices to make, there's only **one way** to break the number into a product of primes. 

As an example, what about a number like 236? 236 ends up being the product 2\*2\*59, all of which are prime numbers. Wait, you might ask, how do you know that *59* is a prime number? It's true, that doesn't seem incredibly obvious does it? To be able to break a number into primes we need to know *which* numbers are prime in the first place. We'll come back to that question *shortly* after we discuss *why* computer scientists use prime numbers.

What's the importance of prime numbers for online life? That comes down to *cryptography* and specifically something called asymmetric encryption.

Asymmetric encryption is generally not used to make big swaths of data secure but rather is an important part of *handshakes*, the kinds of protocols used to establish that each computer in a conversation is exactly who it says it is. In asymmetric encryption, you have a *public key* and a *private key.* The public key is public, meaning anyone can have it and in fact **needs** to have it for the next part. The private key? You alone should have your private key. To prove your identity, you're going to encrypt a message with your private key and then if it can be unencrypted with your *public* key you've proven you sent the message.

To generate your public and private key, you first pick two *very large* prime numbers: you multiply them together to make your public key and do a different, more complex, set of operations on them to make the private key. The entire reason why you can distribute the public key freely is because while it's very easy to multiply two numbers, even big ones, it's incredibly hard to look at a huge number---like numbers with *hundreds* of digits huge---and be able to figure out what prime numbers make them up.

Here as an example, try to figure out which two prime numbers make up this relatively small number: 3183379\. At the end of the article I'll tell you which they were\!

This is such a hard problem that there’s only one kind of computer that could solve it quickly and that’s a quantum computer. This is actually one of the main things that makes people excited and scared of quantum computers: they can be used to break asymmetric encryption.

So back to the question of *how do you know a number is prime?* It turns out, this is a pretty hard question because the only way to know a number *is* prime is because you've failed to show it *isn't*. That's because the definition of "prime" means you've shown there *aren't* any other numbers that divide it. The simplest solution in code is the *brute force* check, where you check one by one to see if there is a number that can divide the number you're testing\! If there isn't one, then you know the number is prime.

Here’s how a brute force check might work with code by first importing a library with math functions:

import math

def isprime(n):  
    isPrime \= True \# assume it's prime until you find a factor  
    for x in range(2,1+int(math.sqrt(n))):   
        \# check from 2 til squareroot of n  
        \# (the 1 \+ is so the for loop includes the sqrt)  
        if n % x \== 0:  
            isPrime \= False  
    return isPrime

But a more sophisticated, and actually quite old, algorithm is the *sieve of Eratosthenes* which is best described like this: if you want to find all the primes below a certain number, say 100, then first start by writing down each number below 100\. Now go to the first prime number, 2, and cross off all multiples of 2 starting with 4\. The next number not crossed off is 3, so cross off all multiples of 3 that haven't already been crossed off. The next number not crossed off will be 5, so continue the process until there's no more numbers under 100 to cross off. What *isn't* crossed off are all the prime numbers below your limit.

The Sieve of Eratosthenes is an algorithm that has more upfront work but is actually *more* efficient because it calculates not just whether one number is prime but what *all* the prime numbers below a certain number are.

The funny thing, though, is that in industrial cryptographic applications things like this aren't used but rather *probabilistic* tests, which rather than giving an absolutely correct answer give an answer that's *very unlikely* to be wrong. In the asymmetric encryption we talked about, they generally use something called *Fermat's test* which is incredibly fast and has a ridiculously tiny chance of being wrong. This allows for fast public/private key generation\!

So prime numbers are both an interesting thing to study in their own right but also weirdly important to the ways we communicate online every day. Sometimes the most unlikely parts of mathematics suddenly become the most practical\!

Answer: 1361 & 2339

