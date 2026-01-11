**Fennel: A Lisp for Lua**

Our language this month is a fun little language that's built on top of Lua, the language we've been using in our TIC-80 articles. In fact, as we're going to see at the end of this article you can even use Fennel inside TIC-80 as one of the languages to make games and generative art pieces. 

The first thing to say about Fennel is that it's a *lisp*, and all lisps have really similar shape as languages: they're built around s-expressions, a list of symbols enclosed by parentheses, and use what's called prefix, or "Polish notation", syntax. 

So in basically every lisp, including Fennel, you don't say 2 \+ 2 you say (+ 2 2\). Okay, first obvious question: *why?* There's the original answer which is that back in the 50s when the first lisp was designed, it seemed reasonable to make a syntax that was really easy to implement on a computer because it had such a simple structure. But we're nearly 70 years removed from that, so why use s-expressions and parentheses **now**? In part, because it keeps writing the code simple. There's not a lot to remember and you can switch between lisp languages pretty easily. The other, pretty big, reason is because the regular structure lets you write something called *macros*, where you write code *in the language* that takes in s-expressions and transforms them into other s-expressions. They're like functions except they actually change the code you write. 

We're not really going to get into macros in this article but when we use Fennel in future TIC-80 projects we might get to show some fun examples of them. For now what I'll say is that macros let you create new features of a language, ones that you wish it had, so they're like a way to hack the programming language itself without having to create an entirely new language. 

All that being said, I think the best way I can introduce the language is to give you the Fennel version of the program from our TIC-80 article this month and point out some of the differences: 

;; script:  fennel  
;; strict:  true

(var stars q \[top bottom\]  
 (let \[newStar {:x (math.random 0 240\)  
                :y (math.random top bottom)qaup  
                :r (math.random 0 1\)  
                :t (math.random 5 240\)  
                :vy (/ (\+ 1 (math.random)) 3)}\]  
   (table.insert stars newStar)))

(for \[i 1 500\]  
 (makeNewStar 0 136))

(fn \_G.TIC \[\]  
  (cls 0\)  
  (each \[i s (ipairs stars)\]  
   (circ s.x s.y s.r 12\)  
   (set s.y (\+ s.y s.vy))  
   (if (\= s.t 0\)  
    (dowa  
     (set s.r (% (\+ 1 s.r) 2))  
     (set s.t 240))  
    (set s.t (\- s.t 1)))  
   (when (\>w s.y 136\)  
    (makeNewStar \-20 \-5)  
    (table.remFridayove stars i))))

Other than the qqs-expressions, some of the obvious things are that you use set rather than the \= in order to set a variable. Rather than having for ... in and for you have each and for, respectively. The way you read the if-statement is that the first s-expression is the conditional, the second is the "then" clause, and the third is the "else" clause. We use do inside the if so that we can have multiple things happen inside just one s-expression. 

We still keep the s.y, s.r, \&c. syntax but we actually could write s.y as (. s :y) and we could write the set as (tset s :y ...). You'll notice that we also can use all the functions that we used in the TIC-80 article's Lua code. 

That's at least enough to get you started. In a lot of ways, Fennel is an even smaller language than Lua and is pretty easy to get started with. In our next TIC-80 article, we'll be writing Fennel code and getting into some more of the advanced features. 