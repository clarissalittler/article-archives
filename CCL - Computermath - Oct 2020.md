**How Computers Have Changed Mathematics**

*Clarissa Littler*

Over the last few decades, computers have had a massive impact on how mathematics is done. Now, you might hear that and think "yes, of course, computers can do stuff with numbers fast" and that **is true** but **not** what I'm talking about\! No, I mean something a little weirder and more interesting. 

To start, though, I need to talk about what mathematicians actually do. Mathematicians mostly don't deal with *numbers* as such, at least not doing things like adding & multiplying numbers. Mathematicians study the *structure* of things. They answer questions like "how would geometry work if there are 10 axes of movement instead of three?" or "do all algebra equations have solutions?". Or sometimes they try to understand what different ideas have in common, like how are strings in a programming language, positive whole numbers, and lists all the same thing? (The answer is that they’re all examples of something called a *monoid\!*) 

Sometimes mathematicians tackle problems like these out of idle curiosity, and sometimes because it's inspired by real world problems: for example weird problems in geometry are important to physicists & finding algorithms to factor big numbers into primes matters a lot to computer security. 

Instead of number crunching, mathematicians tend to *write proofs*. A proof to a mathematician is a lot like performing experiments in science. It's the way they figure out if they're right. A proof, though, is also like an argument to convince someone. Here's an example of a very simple proof\! 

Proof that there's no largest number: 

Suppose that there was a number, let's call it n, that's the largest number. If it's the largest number, then no other number can be bigger than it. We also know that we can always add one to any number. 

But\! We also know that n+1 is bigger than n, so n can't be the largest number. 

If no number can be the largest number, then clearly there is no largest number. 

Hopefully that makes it clear what I mean: proofs are **arguments**. They're ways of demonstrating something is true by thinking about it and using rules that we already know are true to show something *else* is true. 

This is, however, something computers have started to be able to help mathematicians do\! There's a couple of different ways, too. One of them is *interactive theorem proving*, which basically involves programming to make proofs. 

I’m including two examples, but I *don’t* expect them to make sense. I just want you to be able to see them & note that they both look different than other programming languages but yet still *are* programming.

Here's the proof above in the language Isabelle 

theorem no\_biggest: "¬ (∃ n::nat. ∀ m::nat. n \> m)"  
proof (rule notI)  
 assume h1: "(∃ n::nat. ∀ m::nat. n \> m)"  
 then obtain x::nat where p:"∀ m::nat. x \> m" by blast   
 hence "Suc x \< x" by blast  
 thus False by auto

and here in the language Agda 

≡Not\< : {x y : nat} \-\> x ≡ y \-\> ¬ (x \< y)  
≡Not\< refl (lt2 l) \= ≡Not\< refl l

no-biggest : ¬ (Σ\[ n ∈ nat \] ((m : nat) \-\> m \< n))  
no-biggest ⟨ n , p ⟩ \= ≡Not\< refl (p n)

This is a very strange kind of programming\! It's some of the weirdest, most difficult, and most fun, programming I have ever done in my life. The basic idea is that the program computes a bunch of operations in a *logic*, a symbolic system for reasoning about truth, and the final computed thing is a proof *in* that logic. It's so neat and is something mathematicians *and* programmers should probably learn. 

Chip manufacturers like Intel use these techniques to verify that their chip designs work as intended. Companies working on electronic voting machines need to validate their protocols to make sure they’re secure. Researchers at New South Wales in Australia once proved that the core of an operating system worked correctly using the Isabelle system mentioned above.

This isn't the only way computers have helped mathematicians write proofs\! An early example was the proof of the *four color theorem*, a math problem inspired by cartography. Basically, the theorem was proposed as a **guess** of what someone thought was true: that you could take any map—no matter how weird you drew it—and using no more than four colors you could color in all the countries on the map without having the same color touching. The four-color problem sounds reasonable but was *very very hard to prove*. It kinda makes sense, right? How do you take an *infinite number* of possible maps you could draw and prove that **all** of them can be colored in like this? Well, in the 1970s mathematicians figured out that if they could prove the four-color theorem worked for about 2000 cases then it would work for every possible map. 

But checking those 2000 cases? That would have taken years, and years, and years. Mathematicians get bored very easily\! Do you know who doesn't get bored—that we know of at least? A computer\! So Kenneth Appel and Wolfgang Haken figured out how to get a computer to run through and check each of these nearly 2000 cases. Since this was on a computer from the 1970s, it still took awhile: the equivalent of about forty days\! 

And I've been stressing that these techniques are weird and hard, because they are, but it might also make you wonder "why would a mathematician want to do them?" Mostly because it helps make math an *experimental* field. You can easily play with definitions and ideas, try things out, and the computer helps keep it all straight for you. The computer becomes an assistant that keeps you from making mistakes and, once you can feel more confident because of it, you can try so many odd things without fear. 

Links:

* Agda theorem prover: [https://wiki.portal.chalmers.se/agda/pmwiki.php](https://wiki.portal.chalmers.se/agda/pmwiki.php)  
* Isabelle theorem prover: [https://isabelle.in.tum.de/](https://isabelle.in.tum.de/)  
* A different perspective on how computers are turning mathematics into an experimental science: [https://carma.newcastle.edu.au/resources/jon/Preprints/Books/Crucible/crucible.pdf](https://carma.newcastle.edu.au/resources/jon/Preprints/Books/Crucible/crucible.pdf)  
* A cute visual introduction to the four-color theorem: [https://www.mathsisfun.com/activity/coloring.html](https://www.mathsisfun.com/activity/coloring.html)  
* The Incredible Proof Machine: an accessible introduction to logic & proofs for kids [http://incredible.pm/](http://incredible.pm/)


