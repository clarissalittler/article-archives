**Generative Art in TIC-80: it’s full of stars**

Last time we introduced TIC-80, a little all-in-one system for doing games, music, and generative art projects\! We talked about some basic things about how to use code to draw and then drew, an example picture of a snowman. 

As a little reminder here's the code we finished with last time\! 

function TIC()  
 cls(13)

 circ(120,100,22,12)  
 circb(120,100,22,0)

 circ(120,80,18,12)  
 circb(120,80,18,0)

 circ(120,65,13,12)  
 circb(120,65,13,0)

 circ(115,60,2,0)  
 circ(125,60,2,0)

 tri(118,63,122,63,120,70,3)

 line(105,80,85,70,0)  
 line(135,80,155,70,0)  
end

The main concepts here that we'll need this time are 

* there has to be a function called TIC() that acts as the main game loop 

* the screen is 240 pixels wide and 136 pixels tall, with (0,0) as the *upper-left* corner of the screen 

* to draw circles you use the circ function, which takes as its arguments the x and y position of the center of the circle, the radius of the circle, and the number of the color as seen in the sprite making tab 

With all those reminders, now we can talk about how to create a moving field of stars, which means 

* how to use randomness to create an infinitely varying scene 

* how to make things move across the screen 

* how to use Lua's tables as both *lists* and as *objects* 

To start, open TIC-80 and create a new project with new lua, hit esc to see the code, and you should be looking at the basic program that all TIC-80 programs start with. Great, now erase it all so that your file looks like this 

function TIC()

end

and nothing else 

The first thing we need to do is make a list for holding the stars that are going to scroll down the screen. This is our first use of tables. 

stars \= {}

function TIC()

end

Now I'm going to show you a bit of a trick for how to write programs like this, which is that you start by writing what the thing *should do* and then you go back and fill in what you need to do it. So even though we haven't figured out what a "star" is in the program we're going to figure out what we *need* it to be by writing our drawing and movement code first. 

stars \= {}

function TIC()  
   cls(0) \-- we want a black background because space

   for i,s in ipairs(stars) do  
      circ(s.x, s.y, s.r, 13\)

      s.y \= s.y \+ 0.1  
   end  
end

Okay, we have our basics here now: we're using

* a for .. in .. loop to do *something* for every star in the list 

  * i,s means name the place in the list, which is a number, i and grab the actual star in the list and call it s 

  * ipairs(stars) means "take the Lua table stars and treat it like a list" 

* the . syntax to get access to data stored in each star; in this case we're using 

  * s.x as the x position 

  * s.y as the y position 

  * s.r as the radius of the circle 

We can run this code, although it won't do anything because there are no stars in the list\! 

So let's write a *function* to make new stars 

stars \= {}

function makeNewStar

function makeNewStar(top,bottom)  
 local newStar \= {}  
 newStar.x \= math.random(0,239)  
 newStar.y \= math.random(top,bottom)  
 newStar.r \= math.random(0,1)  
 table.insert(stars,newStar)  
end

for i\=1,500 do  
 makeNewStar(0,136)  
end

function TIC()  
   cls(0) \-- we want a black background because space

   for i,s in ipairs(stars) do  
      circ(s.x, s.y, s.r, 13\)

      s.y \= s.y \+ 0.1  
   end  
end

We make a new star just like we made the list of stars, and we set the properties of this new star that we want to use\! Finally, we put the star in the list with the function table.insert. Of course, we couldn't draw anything if we didn't *make* some stars so we also add a for loop that runs 500 times and places stars on the screen between 0 and 136. We generate star position and sizes randomly with the function math.random which can be used to either get a whole number between a range or a fractional number if you give it no argument at all. We'll come back to that in a moment. 

Now if you test this code you'll see a few problems that we need to fix. First, once the stars scroll down they're completely gone\! That means we need to make new stars as the old ones scroll off the screen. Unlike the first stars, we want to make these *above* the top of the screen so they scroll into view and don't just "pop". 

Second, we want the stars to blink: but not all at the same time, so we're going to add code to make a timer that ticks down so that the stars blink every couple of seconds but out of sync with each other. 

Finally, we want the stars to actually move at different rates to give the feeling that they're not all the same distance away. Your eye will sort of naturally assume the ones moving slower are further and the ones moving faster are closer, even without explicit layers to draw\! 

So if we add in all those little changes we get **this** instead 

stars \= {}

function makeNewStar(top,bottom)  
   local newStar \= {}  
   newStar.x \= math.random(0,239)  
   newStar.y \= math.random(top,bottom)  
   newStar.r \= math.random(0,1)  
   newStar.t \= math.random(0,240)  
   newStar.vy \= math.random()/2 \+ 0.1  
   table.insert(stars,newStar)  
end

for i\=1,500 do  
   makeNewStar(0,136)  
end

function TIC()  
   cls(0)

   for i,s in ipairs(stars) do  
      circ(s.x,s.y,s.r,12)  
      s.y \= s.y \+ s.vy  
      if s.t \== 0 then   
         s.r \= (s.r \+ 1)%2  
         s.t \= 240  
      else  
         s.t \= s.t-1  
      end

      if s.y \> 136 then  
         table.remove(stars,i)  
         makeNewStar(-20,-5)  
      end  
   end

end

That concludes our little project for this time. Next time, we’re going to expand on this program and make it interactive\!