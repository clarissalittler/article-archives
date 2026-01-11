**Archiving: keeping old computers alive with code and elbow grease**

*Clarissa Littler*

Without intervention, one day the last NES will be broken beyond repair. Same with the last Commodore 64, last PS1, last XBox 360, \&c. One day the last 32-bit Intel processor will have stopped working. 

For every one of these systems that falls away, there is an entire swath of media that is in danger of being lost for good: video games, interactive art installations, important pieces of software like Windows 3.1 or DOS. 

The same way losing a human language—a serious problem in itself\!—means you can't read their books or understand their songs, losing the hardware needed for old software means that no one can ever experience it again. No one can play with it, learn from it, and connect with the past. Imagine a video game you really like, maybe even means a lot to you, and not being able to show it to future generations. This has already started happening with Adobe Flash no longer being supported on most computers, which means that a lot of the games, comics, and other media of the 2000s is now impossible to view without a lot of effort. 

Now, if this all sounds dire and scary it's time for the good news\! People—a lot of people—are working hard on this problem\! 

There are two basic ways to keep old things alive: restoration, where you repair what you have to keep it going—like what people do with famous paintings—and *archiving* where you find a way to store copies that can be preserved over time. 

Repairing is difficult for old computer parts because we generally don't have the tools needed. Much of what makes old systems unique are custom built chips, so if you don't have a facility that can make them and detailed plans for how they're built then you're out of luck. 

Archiving, on the other hand, can give you a robust, hard-to-break way of keeping the systems around. 

There are two ways to archive hardware: using software or *using other hardware*. They both involve something called *reverse engineering*, where you figure out how something works from a working copy without source code, specifications, or plans. 

The reason *why* we don't have these things is because these designs were generally *proprietary*, which means they were company secrets. Nintendo will likely never hand out the instructions to build an NES, no matter how long it's been since you could buy one. 

Archiving using *software* means making something called an *emulator*. You've probably seen emulators before\! If you've ever used dolphin, retroarch, zsnes, nesbox, or many others to play old video games then you've seen an emulator\! 

These pieces of software work by pretending to be the actual hardware. So, for example, a NES emulator works by literally mimicking an NES with the right clockspeed, memory layout, \&c. This *can* work great, but is sometimes very difficult to run because you need something much more powerful than the hardware you're emulating to run the simulation fast enough. And by "much more powerful" I mean a Raspberry Pi 0 with a 1GHz processor and 512MB of RAM struggles to emulate a PS1 that was only a 33MHz processor with only 2MB of RAM. 

The other, newer option, is archiving hardware with *other hardware*. This involves a cool bit of tech called a Field-Programmable Gate Array, FPGA for short. 

FPGAs are basically chips whose behavior can be configured through code. You write down a description of how a chip you want should work, apply that to the FPGA, and then the board will, for all intents and purposes, **be** the chip you've described. 

FPGA programming is hard, but once you've got it then it'd be like having a way to make new copies of an NES, or PS1, or Wii but without the complications of figuring out how the original was manufactured. Companies like Analogue are even selling handheld consoles that use FPGAs in order to run original cartridges of old video game systems. That's pretty cool\! 

There's a lot more to the world of archiving old computer systems. There're people who've reverse engineered Windows 3.1. There're people who've managed to re-implement Adobe Flash in a custom web browser just so they could keep reading Homestuck. It's a world full of creative people working hard to keep things they love alive and I think that's amazing\! 

Links:

* The Internet Archive has preserved games in Flash [https://archive.org/details/softwarelibrary\_flash](https://archive.org/details/softwarelibrary_flash)  
* Analogue is a company that uses FPGAs in their products to let you play original cartridges for old systems [https://www.analogue.co](https://www.analogue.co)  
* Here’s a head to head comparison of Nintendo’s SNES Classic, which used software emulation, vs. Analogue’s Nt Classic which was FPGA based [https://www.tomsguide.com/us/snes-classic-vs-super-nt,review-5145.html](https://www.tomsguide.com/us/snes-classic-vs-super-nt,review-5145.html)  
* The custom made open-source, flash supporting, browser that Homestuck fans made to preserve their favorite comic [https://bambosh.github.io/unofficial-homestuck-collection/](https://bambosh.github.io/unofficial-homestuck-collection/)

