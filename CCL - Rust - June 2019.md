**Rust: A New Systems Programming Language**

*Clarissa Littler*

The last couple of issues we've been talking about programming languages that are really important for low-level programming. We talked about assembly languages, which are the lowest level human readable programming languages before the raw instructions to the processor. We've talked about C, an old and important language still used for programming microcontrollers and making operating systems. Now we're at the third part of our trilogy of *systems programming* languages: *Rust*. 

If you have a repl.it  account you can follow along as Rust is one of their supported languages. Otherwise, you'll probably want to install Rust by following the instructions at [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install). 

Now Rust is, despite its name, a pretty new and exciting language\! When we talked about C, we explained the idea of a *runtime system.* The runtime system is all the code included in your compiled program that does things like allocate memory for the data the program needs and give memory back to the operating system when it's done. Runtime systems are usually big complex pieces of code that have to interrupt or slow down the program *you* wrote in order to handle all the clean-up. A big reason why *C doesn't need one* is that it forces you to allocate and deallocate memory yourself, so there’s no need to have another chunk of code running watching to see if something needs to be taken care of. If you read that and thought to yourself "that sounds like it'd be easy to mess up\!" then you'd be right\! 

Over the years, programmers have caused so many bugs by not freeing up memory when they were supposed to, which is called a *memory leak*, or by not matching the size of the memory they’ve allocated with the size of the data they’re reading in and storing.That last one allows something called a *buffer overrun* and is one of the big holes that viruses and hackers use to take over a system. Buffer overruns, and the closely related *stack smashing,* work by throwing a ton of data at a program---way more than it expects---and overwriting past the limits of the memory that was set aside for storage. Because of the way memory on a computer works, blowing past the size of memory the program expected you to use you can overwrite all sorts of things in memory *including the program that’s running.* 

This is where *Rust* comes in. It's a language that doesn't require a big heavy runtime but *also* makes practicing good memory management so much easier than C. 

How does it do *that* you might ask? 

Well, the short answer is that it does *a lot* of checks at compile time to make sure that it knows, before the code is ever run, what happens to your data and when it's no longer being used. Rust can actually insert the necessary code to free up memory at compile time because of these checks\! A cool discussion about this is found on the r/rust reddit: [https://www.reddit.com/r/rust/comments/b742vu/if\_rust\_has\_no\_garbage\_collector\_how\_does\_it/](https://www.reddit.com/r/rust/comments/b742vu/if_rust_has_no_garbage_collector_how_does_it/) 

For example, here's a simple Rust program that fails: 

fn main() {  
  let x \= 10;  
  x \= 5;  
}

If you try this out you should see the error 

error\[E0384\]: cannot assign twice to immutable variable \`x\`  
\--\> main.rs:3:3  
 |  
2 |   let x \= 10;  
 |       \- first assignment to \`x\`  
3 |   x \= 5;  
 |   ^^^^^ cannot assign twice to immutable variable

Oh, huh\! It says that x is *immutable*, which means it can't be changed. Yes, by default variables in Rust can't be changed. If you want to change it, you need to use the mut modifier like 

fn main() {  
  let mut x \= 10;  
  x \= 5;  
}

to say that it's "mutable" rather than "immutable". 

Another concept is *ownership*. Now I'm not going to try and give a better explanation of ownership than the official (and free) Rust book linked below, but I'll explain the basic concept. 

First, in order for Rust to know when it can free up memory it needs to keep very careful track of where data is used. For example, when you pass an argument to a function that data is *given* to the function. The function *owns* it now. If the code that called the function wants to keep using that data then the function has to *give it back*. So this code is flawed 

fn badFun(x : String) \-\> String {  
  x \+ "10"  
}

fn main() {  
  let x \= String::from("heck");  
  badFun(x);  
  print\!("the value of x: {}",x)  
}

and gives the error message 

error\[E0382\]: use of moved value: \`x\`  
\--\> main.rs:8:31  
 |  
7 |   badFun(x);  
 |          \- value moved here  
8 |   print\!("the value of x: {}",x)  
 |                               ^ value used here after move  
 |  
 \= note: move occurs because \`x\` has type \`std::string::String\`, which does not implement the \`Copy\` trait

Is anything bad happening in this code? Sure the function took ownership of a variable and didn’t return it, but so what? Is there any danger of a memory leak? Nope\! But that's the thing about checks like Rust does: it *can't* perfectly know when there's going to be a problem or not so it needs fairly conservative rules to make sure there *won't* be a problem with memory. The good thing about Rust and what I like about its design is that the rules are pretty simple\! If you give a function an argument the function has to give it back\! Or if you set a variable to refer to the same data as another variable, you can only use the *new* name for the data and not the *old*. 

If you want to keep learning Rust there are a **ton** of good resources. 

The Rust book and *Rust by Example* are both good free books online 

* The book: [https://doc.rust-lang.org/book/](https://doc.rust-lang.org/book/) 

* *Rust by Example*: [https://doc.rust-lang.org/stable/rust-by-example/](https://doc.rust-lang.org/stable/rust-by-example/) 

but I **really** liked learning from the *Rustlings* course [https://github.com/rust-lang/rustlings/](https://github.com/rust-lang/rustlings/) which is done in the style of a "koans" tutorial, which are a family of tutorials for learning different programming languages where you learn the language by fixing small broken programs. 

If you have a Raspberry Pi, I'd also take a look at *Physical Computing with Rust* [https://rahul-thakoor.github.io/physical-computing-rust/step\_0.html](https://rahul-thakoor.github.io/physical-computing-rust/step_0.html). This is a still-in-progress tutorial on how to control the GPIO pins of a Raspberry Pi in *Rust* instead of Scratch or Python. 

There’s also the start of tutorial series called *Rust: the Hard Parts* that seems promising: [https://naftuli.wtf/2019/03/20/rust-the-hard-parts/](https://naftuli.wtf/2019/03/20/rust-the-hard-parts/)

Finally, if you've got some programming under your belt you might want to try reading *Learning Rust with Entirely Too Many Linked Lists*: [https://rust-unofficial.github.io/too-many-lists/first-layout.html](https://rust-unofficial.github.io/too-many-lists/first-layout.html). It expects you to understand more programming concepts than the other books but it's a pretty neat approach to learning a language. 

Other cool projects using Rust:

* An emulator for the NES written in Rust: [https://www.michaelburge.us/2019/03/18/nes-design.html](https://www.michaelburge.us/2019/03/18/nes-design.html) 

* An *operating system* written in Rust: [https://www.redox-os.org/](https://www.redox-os.org/) 

* An online book on *writing* operating systems in Rust: [https://os.phil-opp.com/](https://os.phil-opp.com/) (I haven't worked through this yet but boy I want to\!) 

* The rendering engine for the Firefox browser [https://blog.rust-lang.org/2017/11/14/Fearless-Concurrency-In-Firefox-Quantum.html](https://blog.rust-lang.org/2017/11/14/Fearless-Concurrency-In-Firefox-Quantum.html) 

* Did you know that you can have Rust code run in the browser? Rust can compile to WebAssembly, the "assembly language" for browsers\! If you think that sounds cool, don't worry I'll probably write an article on WebAssembly in the future. For now, though, you can check out this book: [https://rustwasm.github.io/docs/book/why-rust-and-webassembly.html](https://rustwasm.github.io/docs/book/why-rust-and-webassembly.html) 

