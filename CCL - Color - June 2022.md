**RGB, HSV, IDK: How does a computer display color?**

*Clarissa Littler*

Color is one of those things you don't necessarily think about when it comes to how computers work. I mean, the computer says "put this color in this pixel" and then it appears there and that's the end of it, right? 

Well, what if I told you it's actually all way weirder than that and that there's nothing simple at all about color? 

We need to look at a few different ideas in order to put them all together. The first is what *color* and *light* even are\! The second is how we make colors on a screen. Then finally how programmers represent colors in order to give the screen instructions. 

What is light? Light is a lot like sound: a wave that your body can perceive. Sound is a wave of pressure that shakes the inside of your ear, causing you to hear the wave. How fast it shakes is the *frequency* of the wave. Low frequencies sound *low* to our ears and high frequencies sound, well, *high*. 

Light is slightly weirder in that "what's waving" is a more complicated question but it's still a wave and the frequency of the wave is what your eyes detect as color: low frequencies are *red* and high frequencies are *blue*. When an object has a particular color, it's because the light being emitted from the object is mostly the frequency of that color. 

Now, your eye actually has three kinds of "sensor" in it for color: one for low-frequency light, which means reddish and orange colors, one for medium-frequency light, which means yellows and grassy greens, and one for high frequency light which means blues and purples. This is really different than sound, where you can directly hear the vibration as it shakes your ear.

This bit of biological weirdness is going to lead to something really interesting. You may already know that each pixel in any screen you have has red, green, and blue emitters in it. Computer and phone screens display different colors by changing the proportions of red, green, and blue light emitted in the pixel. 

The catch is that if you add red light and blue light together you just get *red and blue light*. It's like how playing a chord on an instrument doesn't give you a note in-between the notes of the chord, it gives you multiple notes\! So why can we mix light from blue and red LEDs to make purple? It goes back to the fact that our eyes have sensors for low, medium, and high. The red light from the LED stimulates the low-sensor, the blue LED stimulates the high sensor, and your brain interprets the proportion between those two like it would the color purple\! 

Now, each screen and each way of making LEDs is going to lead to differences in how you have to mix light together to emulate different colors. And part of making screens is encoding them with information on how to take the request for a particular color and turn it into a mixture of red, green, and blue to give the desired effect. 

But how do programmers even describe colors? There's a bunch of different ways, but two that are the most common when coding are RGB and HSV. RGB stands for what you might guess: red, green, and blue. You generally describe each of those components with a number between 0 and 255\. That gives a total of 256\*256\*256 possible colors, which is almost 17 million colors. We can't even distinguish much more than ten million colors. 

The big problem with RGB is if I tell you (200,164,190) can you tell me what color that is? I mean you might be able to make guesses if you're experienced but it's not easy to just look at a color as a triple of numbers and know what that will look like. 

HSV (hue, saturation, value \[sometimes brightness\]), on the other hand, is a bit more intuitive once you get the hang of it. The kind of color is the *hue*, expressed as 0 \- 359 degrees like a circle. A hue of 0 is very pure red, a hue of 120 is a light green, a huge of 240 is a deep blue, and through the purples back to red at 360 which is just 0 again. Saturation is how *intense* the color is, with 0% being grey and 100% being the most intense and rich version of that color. Value, again sometimes called brightness, is how *light* it is: like if you were shining a bright or dim white light on it. So if I gave you (300,80,50) as an HSV color you could pretty reasonably guess it's a rich but dark reddish-purple\! 

This is just a first taste of how color works but there’s actually far more to explore in the world of how color spaces are designed, how the human eye responds to color, even in how you have to change the ways you describe colors in RGB to reflect the fact that the human eye has a really complicated response to different intensities of color. It’s a shockingly and fascinatingly complex topic\!