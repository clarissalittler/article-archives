**How would a computer shake hands?**

*Clarissa Littler* 

Computers talk to each other all the time: your browser talks to web sites, your phone talks  to a keyboard over bluetooth, your computer talks to a raspberry pi to get remote access. 

But how do they recognize each other or say "hi, we need to talk"? 

In computer science, this process is generally called a *handshake*. For computers, a handshake might be one of two very different things: the first is how to tell if the two computers are actually hearing each other, *and* the other is how the two computers tell if they're *really* talking to who they think they should be talking to. 

Consider: have you ever been on voice with someone and it takes a second to figure out if you can hear each other? 

"Hello?" "Hey, hello?" "Hellooo?" "Yeah, hey, can you hear me?" "Yeah I hear ya" 

Your computer does this every time it talks to a web server, although it looks more like 

"Hey, server, I want to talk to you\! I've got a number here, 35235998, can you send me back one more than that to tell me that you heard me?" 

"Yeah, no problem, here's your number: 35235999\. Now, I've got a number for you, 796342, can you send back one more than that to let me know you heard me?" 

"Okay, server, here's your number: 796343." 

"Great, good to hear from you, now what do you need?" 

Of course this happens in a fraction of a second and is a lot less wordy when the computers do it, but this is roughly what happens in the TCP (transfer control protocol) that the whole internet is built on. 

Let’s talk about the second kind of handshake computers do, the kind that's about establishing *identity*. It’s like a text from a number or an account you don't know. How do you figure out if the person messaging you is who they say they are? They *could* be your friend or they could be someone messing with you. 

How would you solve this problem? First, you might want to ask another friend, someone who knows the person they’re claiming to be, if they recognize who messaged you. If they recognize the account name or cell number you’re good. Next, you might want to reference something only you and the real person would know, like an inside joke. You could call this *a shared secret*. 

*TSL* (transport security layer) is the protocol that computers use for secure communications on websites, like logging into social media or buying something online, and it's similar to what we've just described. The friend helps you out is a "certificate authority" and the *shared secret* is something you and the server generate together: a *shared key*. The shared key is also used to *encrypt* your messages, so only you and the real server can read each other’s messages. If you’re wondering “hey, if I’m talking across the internet how do I even reliably get a shared secret with another computer?” that’s a very good question\!

As you might guess, once we're dealing with privacy concerns  like how to buy things safely on the internet we need to be *incredibly* careful to make sure who we're talking to. Designing the kind of protocols that can *always* get this right is a really complicated part of computer science, the kind of thing that people have to work really hard on. In particular, the generation of shared secrets involves something called *public key cryptography*.

You don’t have to be working on making online voting safe to try these ideas out: experiment with  designing protocols on your own. Think of how  you and your friends can set up methods  for identifying each other over text, over passed notes, or any other way you could communicate. Or you could  create shared secrets, code words, or schemes to encrypt messages. The most fun---and educational---part, of course, is trying to beat the system and fool each other.