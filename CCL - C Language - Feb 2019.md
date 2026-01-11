**C: The Language of Bare Metal**

*Clarissa Littler* 

For this issue's highlighted language, we're going **really** old-school. We're going to talk about one of the early workhorse languages used to program hardware and write operating systems for over 40 years: *C*\! 

C is old, but still incredibly important. All major operating systems today have a core of millions of lines of C code. That's not just "legacy" code either, left behind because it was too much of a pain to migrate to something more modern. No, C is a useful and indispensable language with few true competitors (except, perhaps, for *Rust* which we'll talk about in a future issue). 

"But what if I don't **want** to write an operating system?" you might ask. Even still, if you want to program an Arduino or code up something for embedded hardware you're **going** to want to use C. 

Now that I've hyped it, let's talk about exactly what C is and why it's so unique and important. To explain that, we're going to take a digression to talk about *runtime systems* for programming languages. 

When you write code in Scratch, Python, Ruby, or most other languages you never have to think about *how* the data you use gets made. You can create a list or an array and just add elements to it as you need. When you're done using those data structures you can just forget about them and they'll be taken care of, erased by the *garbage collector* at *runtime*. If you're wondering what a garbage collector is, you can check out an older article here: [https://www.kidscodecs.com/garbage-collection/](https://www.kidscodecs.com/garbage-collection/). The short-and-sweet version is that a garbage collector for a programming language is code that takes care of figuring out *what* data is no longer used in the program, chooses *when* to get rid of it, and then *destroys* the old data in order to free up memory. 

Now where does this garbage collector code live? It's running when your program runs, but it's not a part of the operating system because it's different for each programming language. Instead, it lives in the *runtime system*. When you run programs in an interpreter, the runtime system is a part of the interpreter. But when you *compile* programs, the runtime system is essentially a big chunk of code that the compiler sneaks into the executable file that's created so that the program can run even without an interpreter. 

The runtime system for a language does a lot more than just garbage collection. Haskell's runtime handles the *lazy evaluation* we talked about last issue. JavaScript's runs the complex event handling system JavaScript uses. Ruby's handles the creation of all its lightweight threads. In other words, the runtime system for mosts languages mediates between the operating system and the program as it runs, handling all the communication between the two needed to make threads or do garbage collection or store computations to run later. 

What does this have to do with *C*, though? Well, *C doesn't need a runtime*—not in the same sense as other languages at least\! 

C has been designed so that it doesn't need this mediation, which means that it *doesn't need an operating system*. That makes sense\! C is for *writing* operating systems\! 

It also means that you can run C code on things like Arduino boards, which are far too small in memory and limited in power to run an actual operating system. 

All that being said, what does C look like? Well here's what a for-loop looks like 

int i;  
int result \= 0;  
for(i=0;i\<10;i++){  
  result \+= i;  
 }

I'm betting this looks kinda familiar if you've ever programmed in something like JavaScript, Java, C\#, or many other programming languages. A massive number of languages over the last 40 years have taken cues from C's syntax. Which means, of course, that we should absolutely blame Dennis Ritchie, the original creator of C, for the predominance of semicolons and curly-braces in programming today\! 

Speaking of Ritchie, though, there's *still* not a better place to start learning C than he and Brian Kernighan's book on C: *The C Programming Language*. It's a book so famous it has its own wikipedia page: [https://en.wikipedia.org/wiki/The\_C\_Programming\_Language](https://en.wikipedia.org/wiki/The_C_Programming_Language) 

To wrap things up, though, I want to at least talk about one of those features that helps C not need a runtime: *pointers*. 

Unlike most languages, C lets you actually see where in the computer's memory data is stored. So for every variable you declare you can then grab its memory location, its *address*, with the & operator, like in this program that declares a variable i and then prints out its address 

\#include \<stdio.h\>

int main(void) {  
  int i;  
  printf("%d\\n",\&i);  
  return 0;  
}

If you run this program multiple times you'll almost assuredly get a different number corresponding to a different location in memory. 

Of course, there's not much you can do if you can only *get* addresses. You should be able to do something with them too\! That's where C's pointer types come into play. They're a special kind of variable that you can store addresses in. 

For example, we can change our example above to use a pointer variable instead. 

\#include \<stdio.h\>

int main(void) {  
  int i;  
  i=10;  
  int\* pointy \= \&i;  
  printf("%d\\n",pointy);  
  return 0;  
}

Where things get really fun is that *arrays* in C are really just an application of pointers: they’re really just a pointer to a sequence of memory addresses reserved for your program to use. So code like this 

int pup\[10\];

sets aside space to hold 10 integers in consecutive memory addresses. If you print out the value of the variable pup you'll actually get the address to the first element of the array, which means that pup+2 is, for example, the address of the *third* element of the array. C gives you the now-standard pup\[2\] notation as well to access the third element of the array, but maybe now this gives you some insight into *why* arrays in most languages start counting at 0\! 

Finally, even strings in C are arrays of characters and, thus, are pointers under the hood.

So that's my pitch for why C is an important language to learn and just a taste of some of what still makes it unique. 

Happy hacking\! 

Further reading:

* A tutorial on C by the author of a famous online book about network programming: [https://beej.us/guide/bgc/html/single/bgc.html](https://beej.us/guide/bgc/html/single/bgc.html)  
* A decent tutorial just on pointers: [http://pw1.netcom.com/\~tjensen/ptr/pointers.htm](http://pw1.netcom.com/~tjensen/ptr/pointers.htm)

  