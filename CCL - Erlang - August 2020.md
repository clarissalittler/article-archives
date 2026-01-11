**Erlang: A Language for Big Important Programs**

*Clarissa Littler*

Some languages are general purpose, meant to be the main thing you use for almost every problem. Other languages are more special purpose, meant for particular uses and problems. Erlang, the language we're talking about in this issue, is much more the latter than the former\! Specifically, Erlang is a language for *concurrent* and *distributed* programming. 

Before we jump directly into talking about Erlang, let's take a few moments to talk about how concurrency works and what distributed programming even is. To start, modern computers all have multiple *cores* inside their processors: each core is capable of running at least one (but usually two) threads at a time. A *thread* is often an entire program but it can also be *a part* of a program, with a program using many threads at once to do its work. When a program uses multiple threads, its said to be a "concurrent" program. 

Why might you need multiple threads? Well, things like web-servers where you need threads listening for new connections and handling their requests or online games or even algorithmic music systems like *Sonic Pi* where each thread is a different pattern of music playing independently from each other. 

Distributed programming is similar to *concurrent* programming but instead of multiple threads running on *one* computer it's separate programs running on multiple machines that are still capable of working together like one **big** program. A lot of what people call "the cloud" is just big networks of computers running distributed programs. 

It's easy to understand *why* Erlang was made to be a language for concurrent and distributed computing when you know that the company who made it, Ericsson, is a huge telecommunications company. Erlang was made to help Ericsson programmers write the code that made the telephone switches, the computers that route phone calls from source to destination, work. They needed a programming language suited for running big complicated distributed code that *needed to never fail*. Back in the 1980s, when Erlang was first made, there weren't exactly a lot of languages up to the task: so Joe Armstrong and his colleagues made one\! Even though it's been used for many, many, kinds of projects since the '80s, Erlang still shows its roots in telecommunications: it's the language that WhatsApp—one of the most popular texting services in the world—was developed in\! 

Though it was originally only used within Ericsson, Erlang has been open source and freely available for over twenty years now. You can get it from the main Erlang site here: [https://www.erlang.org/](https://www.erlang.org/). 

Erlang is a very simple language to learn. It only has a few very flexible kinds of data, including *lists* and *tuples*. Tuples, much like tables in Lua discussed elsewhere in this issue, are a super flexible datatype that can be used like objects are in most languages. There are no loops, only recursive functions. Variables are even simpler in Erlang than most other languages\! You can give a variable a value *only once* and then never change it again\! If that seems weird, it's a feature that makes it harder for concurrent programs to mess up. Most of the problems that happen with concurrency are things called *race conditions*, which are when two threads attempt to change data at the same time but neither knows the other one was doing it. Really, probably the most complicated thing about Erlang programming is remembering that all variables have to start with a capital letter\! 

Here's a small example program in Erlang, which creates an "echo server" that you can run from the Erlang command line *erl*. 

\-module(echothing).  
\-export(\[start/0\]).

start() \-\>  
    spawn(fun() \-\> loop(\[\]) end).

loop(Msgs) \-\>  
    receive  
	Msg \-\>  
	    io:format("You just said \~p\~n", \[Msg\]),  
	    io:format("And \~p other things\~n",\[Msgs\]),  
	    loop(\[Msg|Msgs\])  
end.

You run this by starting *erl*, which you installed when you installed Erlang, and then first typing c(echothing). and hitting enter to load the program. Now, type Pid \= echothing:start(). and hit enter again to start the server. You've now bound the variable Pid to the name of the thread that's running the server\! You can send it messages with Pid \! "whatever you want" and see the result. 

That's it for our very, very brief introduction to Erlang. It's a language I highly recommend learning because while it is simple it will absolutely force you to think differently about programming\! 