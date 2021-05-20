---
title: Neanderthal tools sound gathering
subtitle: The process we had from gathering sound to implementing into the game  
date: 2021-05-10
tags: ["tools", "unity", "sfx", "VR"]
---

To get the best results one must be prepared in advanced to be able to get the most out of what he wants to accomplish. So here I'll be writing the process I had with my friend Edvinas who is doing his masters thesis on interactive media in museums. A bit about the thesis is that they are researching on new ways to help museums convey history in modern day and that is by using VR. They have been cooperating with Archaeological Museum in Zagreb to develop a small VR game about the neanderthals how they made their tools and what technology they used. The link to the game will be found in a later post as it is not yet made public. 

### Researching
The very first thing that has needed to be done is sitting down and getting to know the specifics of how neanderthals worked, what they used and how they used it. So we talked. A lot of information was given as well as a simpler breakdown. At this stage I learned interesting things about how people in that time managed to survive, how they built things, how they lived. Yes there were things known that they used bones and flint for a lot of things, but interestingly enough what they used as glue to connect the stick with the sharp flint. I will not spoil the game here for anyone that hasn't played it yet.
So yes we had to talk about the game vision, what the general feel should be, what is expected from a player, how to make it for the player more easily to comprehend what is happening and also to have in mind that we should not overwhelm the player. The first list of what sounds will be needed looked like this: 
* Flint shattering/dropping
* Stone dropping
* Wood dropping
* Stone scraping
* Interractions
* Fire (idle burning and adding more wood to it)
* Ghost (idling as well as apearance/disapearance)
* Cave ambience (windy feel, water droplets from time to time)
* Main menu ambience
* Success action
* Footsteps
Later on the list was expanded by boulder shattering sounds. Which is what can be noted. That what ever the agreed list is at the begining it can be expanded as testing ensues. It is a good thing to take into mind when figuring deadlines for yourself. Add forethinking into the equation. You will definetly spend more time on the things that are unknown/never considered. But this comes with practice so no need to overthink it just to observe it and take into account when working on later projects.

### Gathering
This is the stage that we [gathered all the sources](https://www.instagram.com/p/CNIqkhknyMY/?utm_source=ig_web_copy_link) we thought were needed as source material before transfering to the DAW and editing them. We had to search for a lot of flint to make as much variations as possible for it so upon research we headed to the nearest river we had, which is also the biggest one in Lithuania.
![nemunas](/img/post2/nemunas.png)
As well as getting rocks to shatter the flint, some bark, sticks and anything else we thought that might add interesting texture.
![resources](/img/post2/matts.png)
And so the shattering, breaking and crunching begins!
![shattering](/img/post2/shatter.mp4)

No need to show here all the shatterings and breakings. So instead let listen to them!

![Footsteps](/img/post2/pedutes.wav)
![Flint Shatter](/img/post2/titnago_shatter.wav)
![titnago_skeveldros](/img/post2/titnago_skeveldros.wav)
![titnagos_impact](/img/post2/titnagos_impact.wav)
![trekst_krebzt](/img/post2/trekst_krebzt.wav)

### Cleaning
And of course the file cleaning stage. The day was a bit windy and even though we went between the trees that the blow wouldn't go directly into the mic there were leave rustling thoughout the files.
![rx](/img/post2/rx.png)
But that doesn't stop me from making the most of the files. Conveniently RX8 has a function called De-Rustle which help to remove the rustling sound from the files, of course that needs a few iterations to remove most of the unwanted sounds and to leave the wanted parts relatively untouched.
![derustle](/img/post2/derustle.png)

Here is an example with De-Wind function as I already had De-Rustled all the files.
Firstly the original.
![footstep_no_fx](/img/post2/footstep_no_fx.wav)
And after the fx processing.
![footstep_with_fx](/img/post2/footstep_with_fx.wav)

### Implementing
Well now. Sorry to disappoint for this stage. But I didn't implement any sounds to the game. It was on a very tight schedule so I let my friend handle all of them in Unity. From all the engine side I can show you the mixer settings used here as Edvinas mentioned this was a great way to divide sounds, not by sounds themselves but by the type of sounds.
![engine mixer](/img/post2/unity_mixer.png)

And this is how the game looks and sounds! Don't worry - no spoilers here.
![game_vid1](/img/post2/game_vid1.mp4)