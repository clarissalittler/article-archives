**How data is stored**

*Clarissa Littler*

When programmers and computer scientists say "data" they mean basically *everything* that can be stored on a computer or transmitted across the internet. At the end of the day, this data is always just a sequence of millions—sometimes billions and occasionally trillions—of bits, ones and zeros. But these ones and zeros aren't just in some random order\! They're an *encoding* of data, a way of converting things like pictures, songs, \&c. into ones and zeros in a consistent, efficient way so that they can be understood later by video players, web servers, things like that.

Before we continue, let’s just quickly talk about how bits---ones and zeros---can be combined to make bigger numbers. Take an ordinary number like 324: what this actually says is the number that’s 4 \+ 2\*10 \+ 3\*100: the digits in each place can range from 0 to 9 and each place represents “how many” of a power of 10 it represents. Binary numbers work the same way, except the numbers in each place must be either zero or one---so a *bit*\---and they represent powers of *2* instead of 10\. So if you read the binary number 101101 from right to left like you would a normal number you get 1 \+ 0\*2 \+ 1\*4 \+ 1\*8 \+ 0\* 16 \+ 1\*32, which is *45*. In programming we often talk about a *n-bit number*, where *n* is the number of bits we use to store the number. If you’ve heard people talk about *bytes* of storage, those are *8-bit numbers* that can be used to represent a number between 0 and 255\.

Now back to encodings\! Some encodings are super simple. The old-school ASCII text standard just assigned every letter, number, and symbol on the keyboard a 7-bit number, 0-127. The modern UTF-8 text encoding allows characters to be represented by 8–32 bits and covers over a million possible characters in order to better support languages other than English. 

Other encodings are more complex, like the aac or ogg vorbis standards for encoding music that're used when streaming. They have to encode not just the data of the music but all sorts of *meta*\-data, like the name of the musician, song, album, and year it was made. 

Encodings frequently also do some kind of *compression*. Compression is about finding ways to make data *smaller* yet reconstructable, usually by removing redundancies---things that are repeated. To make this less abstract, here's a very simple compression scheme: compress strings of digits by replacing every sequence of the same number with a pair of 

* how many times the number occurs 

* the number that's being repeated 

so, for example, you would compress the sequence 

000222334444444448888867777777523355 to 3032239458167715122325 which is almost half the length. If there was *more* redundancy you'd get even better compression, but the closer the string is to **random** the less compressible it is. 

Why is this necessary? Well, consider a 4k video on YouTube: a 15-minute video would be about a *terabyte* of data, which would take—depending on your internet speed—anywhere from an hour to days to download. Well, does a 15-minute 4k video actually take days to stream? Obviously not\! That's the compression at work. 

You might be wondering "what's *redundant* in video?" and the answer is quite a lot if you're thinking about it as individual frames of video, of which there are generally either 30 or 60 per second. Not much changes from one frame to the next unless the camera is swinging wildly. The backgrounds stay roughly the same, and the position of people and lighting stays roughly the same at these small slices of time. This means that you can just record what *changes* between each frame rather than repeat all the information. Once you know this it'll be really obvious that's what's happening when a video file breaks or gets corrupted: you'll see odd smears of some parts moving and other parts staying the same when they shouldn't be, like a hand will smear around an otherwise unchanging background. It's kinda cool, actually. 

Errors and corruption of data leads us to the last topic I want to hit briefly, which is *error correcting code*—a way of doing encoding where the program reading the data later can tell if it got damaged somehow. For example, one of the simplest error correcting schemes is to literally **double** every bit. So 

100101 becomes 110000110011 

and then you know that if you ever see a pair like 10 then something happened that caused a bit to get flipped. If you triple every bit, you can not only tell when a bit got damaged but also know what it should have been. In other words, if you see a triple of 101 you know it must have started as 111 and fix it. A lot of error-correcting codes are more sophisticated than this but they generally follow the opposite principal of compression: you **add** redundancy instead of removing it\! 

This has just been a very *fast* overview of the topic of encodings, one of those things that is so invisible to how we use computers but makes all the technology around us work. 

Links:

* A fantastic pair of videos from the channel Technology Connections on how encoding of digital sound works ( https://www.youtube.com/watch?v=Gd\_mhBf\_FJA [https://www.youtube.com/watch?v=pWjdWCePgvA](https://www.youtube.com/watch?v=pWjdWCePgvA))  
* A video on a much more sophisticated error-correcting encoding than what we talked about [https://www.youtube.com/watch?v=fBRMaEAFLE0](https://www.youtube.com/watch?v=fBRMaEAFLE0)  
* How Ogg Vorbis compresses audio [https://grahammitchell.com/writings/vorbis\_intro.html](https://grahammitchell.com/writings/vorbis_intro.html)  
* An incredible, interactive, deep dive into JPEG encoding: [https://parametric.press/issue-01/unraveling-the-jpeg/](https://parametric.press/issue-01/unraveling-the-jpeg/)

  