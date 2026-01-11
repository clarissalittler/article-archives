**Inform 7: telling stories with programs that read like English**

*Clarissa Littler*

Bedroom  
You are in your room, which is possibly inside a space station. You can't remember.

You can see a table (on which are a magazine and the spinning wheel (in which is the hamster)) here.

\>examine hamster  
The hamster squeaks at you happily.

\>take hamster  
I don't suppose the hamster would care for that.

\>take magazine  
Taken.

\>examine magazine  
It's a copy of the February 2021 issue of Beanz\! It seems to have an issue on interactive fiction. You read on...

So the above is an example of the output of the programming language we're going to be talking about in this issue: Inform 7\. Inform 7 is different than most languages for two big reasons. The first is that it doesn't just compile into your typical programs but rather an Inform 7 program creates an entire explorable world in a text adventure format. The second is that Inform 7 programs don't even look like normal programs but look more like describing things in English. 

For example, the code that led to the above is this: 

The Bedroom is a room. "You are in your room, which is possibly inside a space station. You can't remember." There is a table in The Bedroom. On the table is a magazine.  On the table is a transparent container called the spinning wheel. There is an animal called the hamster.  

The description of the hamster is "The hamster squeaks at you happily." The hamster is in the spinning wheel. The description of the magazine is "It's a copy of the February 2021 issue of Beanz\! It seems to have an issue on interactive fiction. You read on...".

Just from this code Inform is able to build an entire world you can interact with. It even understands, for example, from the fact that the hamster is an animal that you can't just easily pick it up and put it in your pocket\! A magazine, on the other hand, is an object which you should be able to hold. 

Interactive fiction like this example has a long and important history in video games. These were, really, the very **first** games going all the way back to the 1970s with games like Adventure or Zork. In fact, Inform 7 is named the way it is because it's a modern version of the Inform system that was used to make interactive fiction games 40 years ago. 

These are games where you type commands in order to take actions in the game: move around between rooms, use objects, eat food, pet dogs\! 

Let's take that last one as a jumping off point. So if, given our example already, we wanted to try petting the hamster we'd get the message 

\>pet the hamster  
That's not a verb I recognise.

But we can add verbs to Inform 7\! Here's the code to add petting animals into your game, a rule to make sure you don't try and pet inanimate objects, and a special exception if you try to pet the scorpion we've also added to our story. 

Petting is an action applying to one visible thing. Understand "pet \[something\]" as petting.

Check petting:  
	if the noun is not an animal, say "You can't pet an inanimate object\! That's weird\!"

Carry out petting:  
	say "You pet \[the noun\]. They seem happy\!"  
	  
Instead of petting the scorpion:  
	say "It's a magic scorpion and it doesn't like touch\! It stings you so hard\!";  
	end the story.

So, yes, we've now shown that you can ensure that your game will get the approval of the twitter account @CanYouPetTheDog, which is probably the most important bar you can ever meet. 

Of course there's so much more you can actually do in Inform 7\. There's systems for vehicles, the passage of time, keeping a score for the player, conversations with characters who remember what you've said, and all sorts of things that let you make really rich and powerful stories. All of that done in a true programming language like nothing else you've ever learned\! 

* Inform 7 website: [http://inform7.com](http://inform7.com)  
* The interactive fiction archive: [http://www.ifarchive.org](http://www.ifarchive.org)  
* An online copy of Zork, the home game that made interactive fiction famous. It sold a half million copies in the early 80s\! [https://classicreload.com/zork-i.html](https://classicreload.com/zork-i.html)  
* A sad and beautiful work of interactive fiction made in Inform 6: Photopia [https://ifdb.tads.org/viewgame?id=ju778uv5xaswnlpl](https://ifdb.tads.org/viewgame?id=ju778uv5xaswnlpl)

  