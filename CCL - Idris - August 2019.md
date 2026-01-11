**Idris : The Power of Weird Types**

*Clarissa Littler*

Who likes types in programming languages? If you’ve used typed languages like C or Java you might think of types as annoying things that get in the way. Labels you have to annotate your code with so that the compiler accepts the program *you* already know is correct. After all, that’s why people like languages without type checking like Python, JavaScript, Lua, and Ruby.

But what if there was a language where the types are not only *not* annoying and *don’t* get in the way, but they let you do cool things Python can’t even touch: a compiler that interactively helps you write code or *proves* your code works exactly right with no guesswork? 

You're in luck, dear reader, because there are *multiple* languages out there like this today\! They're called *dependently typed* languages. In this article, we'll be focusing on what I think is the most practical of them: Idris. Idris was created only a few years ago by Prof. Edwin Brady who works out of University of St. Andrews in Scotland. (I have to point out that he also created the absolutely useful and not at all a meme language *Whitespace* that ignores every character that isn't a space, a tab, or a newline.) 

To get started with Idris you need to download it from the main website ([https://www.idris-lang.org/](https://www.idris-lang.org/)) and install it. If you're on Windows or OS X there should be up-to-date binaries you can download, otherwise you'll have to build the compiler yourself—which is less intimidating than it sounds\! 

For the interactive programming experience you'll *also* need to download the code editor *Atom* ([https://atom.io/](https://atom.io/)) and then install the Idris support by going to the *Settings* tab, clicking on *Install*, and then searching for & installing the Idris package. 

Idris is a general purpose language suitable for a lot of things: web programming, graphics, and—if I have my way over the next couple of years—games writing. 

The best introductions to Idris are the official Idris tutorial ([http://docs.idris-lang.org/en/latest/tutorial/index.html](http://docs.idris-lang.org/en/latest/tutorial/index.html)) and Edwin Brady's book *Type-Driven Development with Idris* ([https://www.goodreads.com/book/show/26331996-type-driven-development-with-idris](https://www.goodreads.com/book/show/26331996-type-driven-development-with-idris)). What I want to do in the rest of this article is give you a taste of what dependent types mean, why they're weird, and why you want to use them anyway. There's also a companion piece in this same issue, *What Even Are Types?*, that covers some of these topics in a more conceptual way apart from programming. 

The simplest way to explain dependently typed languages is that they're languages where the types aren't just attached to data and checked at compile time. The types *are* data just like any other, and they can be returned by functions or computed in your program. Types can *depend* on data so that they can take a variety of shapes. 

Here's an example of a *family* of types, one for each natural (i.e. whole and greater than or equal to zero) number: the length-indexed vectors. These are lists that carry how many elements they have *in their type*. I'll show the code just as an example but then describe in words what it means. 

data Vect : Nat \-\> Type \-\> Type where  
 Nil : Vec 0 a  
 (::) : a \-\> Vect n a \-\> Vect (1 \+ n) a

We're defining a new *datatype* called Vect. Vect *depends* on a natural number, which will represent the length, and another type a to represent the things that will go in the list. The next two lines define that there are two ways to make a Vect. The first is that it can be empty, or Nil, which means it has length 0\. The second is that you can take an item of type a and put it into a Vect of length n in order to make a new longer Vect. 

Vect can help prevent errors like writing past the end of an array, which is cool and helpful, but I think we’re ready to get really *weird*. I'm going to show you the code for defining, typechecking, and interpreting a tiny programming language into Idris. 

data U : Type where  
 Unit : U  
 Buul : U  
 N  : U  
 Fun : U \-\> U \-\> U

Sem : U \-\> Type  
Sem Unit \= ()  
Sem Buul \= Bool  
Sem (Fun a b) \= Sem a \-\> Sem b  
Sem N \= Nat

data Syn : U \-\> Type where  
End : Syn Unit  
Seq: Syn a \-\> Syn b \-\> Syn b  
Tr : Syn Buul  
Fls : Syn Buul  
Zd : Syn N  
Sc : Syn N \-\> Syn N  
Add : Syn (Fun N (Fun N N))  
Ifthn : Syn Buul \-\> Syn a \-\> Syn a \-\> Syn a  
Appl : Syn (Fun a b) \-\> Syn a \-\> Syn b

interp : Syn u \-\> Sem u  
interp End \= ()  
interp (Seq x y) \= let x' \= (interp x) in interp y  
interp Tr \= True  
interp Fls \= False  
interp Zd \= 0  
interp (Sc x) \= S (interp x)  
interp Add \= (+)  
interp (Ifthn x y z) \= if (interp x) then interp y else interp z  
interp (Appl x y) \= (interp x) (interp y)

What on Earth is this? Let me summarize: we start by defining a type U that describes all possible types in the little programming language we're defining. We then create a *function* Sem that takes in elements of U **and gives us back types in Idris**. We combine the syntax and typechecking **together** by defining a type Syn that describes all the syntax of our language *with its type*. Finally, we have our interp function that takes a program of type u, then runs the program and returns an *Idris* value of type Sem u.

Remember how I said earlier that the Idris compiler can help you write code interactively? A big chunk of the code underneath the line interp : Syn u \-\> Sem u was actually generated *by* Idris because I asked it to use the type of Syn u to generate a skeleton of the function that I could fill in. 

I don't expect all of this to sink in. Mostly, I'm just hoping, dear reader, you'll look at this and go "what???" or some variation thereof.

Dependently typed languages are *strange* in the best way & I hope you'll check this one out\!

Links and further reading:

* Idris website and tutorial: [https://www.idris-lang.org/](https://www.idris-lang.org/) [http://docs.idris-lang.org/en/latest/tutorial/index.html](http://docs.idris-lang.org/en/latest/tutorial/index.html)  
* The Idris book: [https://www.goodreads.com/book/show/26331996-type-driven-development-with-idris](https://www.goodreads.com/book/show/26331996-type-driven-development-with-idris)  
* Curry-Howard isomorphism: the thing that connects types and logic [https://en.wikipedia.org/wiki/Curry%E2%80%93Howard\_correspondence](https://en.wikipedia.org/wiki/Curry%E2%80%93Howard_correspondence)  
* A difficult but incredible book on what dependent types can do. It’s about an older dependently typed language for **mathematicians** called *Martin-Löf Type Theory* [http://www.cse.chalmers.se/research/group/logic/book/book.pdf](http://www.cse.chalmers.se/research/group/logic/book/book.pdf)

