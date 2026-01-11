**How computers remember things**

*Clarissa Littler*

You may have heard people talk about computers having "memory". But what exactly is it? How do computers use it? And how is it any different from, say, a hard drive or any other storage a computer or phone might use?  

In general, when people talk about a computer's memory they mean *RAM*. RAM means "random access memory", which is just another way of saying that you can grab data from *any* of the tiny bins that make up the memory. 

But why do computers even *need* RAM?

Like a lot of things about computers, it comes down to *speed*. You see, programs have all sorts of data that they need to record and access. Some of that is just *the program itself*. As it's running, the code of the program needs to be read or else the processor couldn’t see what instruction to run next. But also there's all the data the program *itself* needs to keep track of. 

Consider a Minecraft server. It needs to be able to keep track of the positions of *every* block in the instance, every player's position, every NPC's position, every player's inventory, etc. That's a lot of stuff to remember and check\! 

When you have to keep track of so much and you have to access it fast enough to keep the game going at 60 frames per second then *speed matters*. 

The problem with *hard disk drives* (HDDs) or *solid state drives* (SSDs) is that they are *way too slow* to be used by a running program. Even a really good SSD is going to be *at least* 10x slower than RAM and possibly more like 50x or 100x. An HDD is *at least* 10x slower than an SSD. In terms of our poor Minecraft server, if access to every one of those bits of data was slowed down by 100x you'd be lucky to get the game running at even 1 FPS. 

So we’ve established that we need special storage that's faster than a hard drive, but that's not the end of the story. There's more to memory on a computer than just RAM. There's kinds of memory inside your computer that are to RAM what RAM is to a hard drive.

Before we start talking about them, I want to change a little bit of how we're talking about time. Rather than talking about *human* time, I think it'd be good to talk about time from the perspective of the *computer*. Computers have their own sense of time, measured by an internal clock that drives the computer’s rhythm like a metronome.

These *clock cycles* are kind of the base unit of time, because a computer can never do anything faster than one "clock cycle". So let's call these *computer-seconds* to be more accurate. How fast a computer tells us the conversion ratio from human-seconds to computer-seconds. A 3 GHz (gigahertz) computer runs at a speed of three billion computer-seconds for every human-second. **So, getting data from RAM takes at least five computer-minutes.**

Now let's talk about the other kinds of memory and how fast it is. There's two real other kinds of memory in your computer beyond the RAM. There's the kind that each core, the parts that actually execute code inside the CPU, has which are the *registers*. 

Registers can hold only a few *bytes* of data. That's right, not gigabytes, megabytes, or even kilobytes: bytes. Like a single number. On the other hand, reading from and writing to a register can be done *in one computer-second*. This makes registers perfect as a kind of scratch paper, holding all the intermediate steps of calculations that the computer has to do. 

The last kind of memory that your computer has is the *cache*. The cache is for holding onto data that keeps getting used again and again so that you don't have to go all the way out to RAM to get it. Cache, in its best case, takes only a few computer-seconds to operate but can be more. If the registers are scratch paper for doing calculations, then the cache is like copying down the math problems you have to do into your notebook so you don't have to keep looking them up. 

This is, however, only the quickest of overviews. If you find this interesting at all you might want to read more about the details of how all these kinds of memory are implemented\! There’s all sorts of neat tricks and technology that goes into making this hardware and there’s always opportunities for a cunning engineer to make computers even better.

* This is a slightly more technical piece on how the cache in most CPUs works: [https://www.makeuseof.com/tag/what-is-cpu-cache/](https://www.makeuseof.com/tag/what-is-cpu-cache/)  
* A short YouTube video on how different kinds of memory and board are made [https://www.youtube.com/watch?v=3s7KG6QwUeQ](https://www.youtube.com/watch?v=3s7KG6QwUeQ)

