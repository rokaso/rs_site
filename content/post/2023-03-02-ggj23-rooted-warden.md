---
title: "Rooted Warden - Global Game Jam 2023"
subtitle: "The making of audio in Rooted Warden with FMOD"
date: 2023-03-02
tags: ["Unity", "Global Game Jam", "sfx", "VR", "FMOD"]
---

The Global Game Jam 2023 took place on February 3-5. As you all know, this event brings together developers, designers, artists, and creative thinkers from around the world to collaborate, share ideas, and build new and innovative games in just one weekend. I attended it in Kaunas, Lithuania which is organized by [LŽKA](https://www.lzka.lt/) and the website of the event can be found [here](https://www.gamejam.lt/). This years art was done by an amazing artist - [Teresė Žvinakevičiūtė](https://www.instagram.com/teresesutkus/).

This years topic was - Roots. And so we are proud to deliver the game that we worked on through the weekend - [Rooted Warden](https://github.com/ugnelis/moon-gale). It's about an armour without a knight that has to protect it's core from blobs that are spawning towards the center. With passing time the intensity level gets higher and it becomes much harder to keep the core defended. So, how did we do it?

# The Team
I want to start with the people that worked on this project. This project was a collaboration of two studios - [CHARK](https://chark.io/) and [Moonleaf studio](https://moonleafstudio.com/). The team consisted of 7 very talented people (only six faces in the photo, Vaidas got sick and helped us remotely when he could). Left to right:
- [Edvinas](https://edvinas.dev/) - developer
- [Ugnius](https://github.com/ugnelis/) - developer
- Me - audio
- [Gantas](https://www.artstation.com/gcolde) - 3D artist, shaders
- Miglė - lead artist
- [Airidas](https://www.artstation.com/shorte) - developer, VFX artist
- Vaidas (remote) - producer
![the team](/img/ggj23_rooted_warden/moon_gale_team.jpg)

The whole teams synergy was very good and it brought up an amazing flow state. Such a good flow state that I believe there was only one git conflict through the few days. I just want to thank all of these people, because it was an amazing experience to work with them!

# Workflow
As soon as we got to know the topic, we went on a call with Vaidas to brainstorm what could this project be. The first idea that was suggested is about a mole that digs underground and has to evade roots while all of it is synced to music. Something like Audiosurf, but with roots and moles. Another idea was about a slime-mold like game that has to spread out as far as it can collecting food. Well, there were quite a few ideas. But mainly we sat at the idea that there should be a protagonist that has to save it's light core from the roots of darkness. The brainstorm went out of hand it was almost 10PM (the venue closing time) so we had to go home and continue the idea generation. We had made into different scope's based on how much we will be able to do. I think the idea generating session had been over at 1AM.

## Ambience
Next morning we went over some details, confirmed with the team that all was well and started working. I started from ambience, as this is a great way to start the whole storytelling of the world. Ambience sets the tone of the place whether there is someone there or not. It creates the mood and serves as the foundation of the place, it is the setting of it all, the base. From it you can build other sounds that can supplement the environment. It is beneficial for a couple of reasons: it helps you build new sounds and while listening to it over time you can determine if the created ambience is annoying or not. Is it sitting unconsciously in the background or is it to much in your face.

{{< sound src="/img/ggj23_rooted_warden/Amb_Wind_Low.mp3" class="Amb_Wind_Low" >}}
{{< sound src="/img/ggj23_rooted_warden/Amb_Water_Drop.mp3" class="Amb_Water_Drop" >}}

These are the two samples used for making ambience a 3 second low wind drone and a one shot water drop. Hooked it up in FMOD, made the water drop to have a 33% chance of being called so that it wouldn't be called every single time.
![fmod_cave_ambient](/img/ggj23_rooted_warden/fmod_cave_ambient.png)

The wind has a multi-band EQ that has a LFO frequency modulator that makes the wind sound more varied with it's frequency shifts. The LFO modulator shape is randomized.
![fmod_cave_wind_sfx_eq](/img/ggj23_rooted_warden/fmod_cave_wind_sfx_eq.png)

And for the water drop a lot of things happen. It has a pitch-shifter, gain control and reverb wet level that randomizes in a range. As for the delay, I've set a LFO to the delay time that runs from a 100ms to 5 second. The dry level and feedback is set to off. What this does to the water drops is quite interesting. The water drop has a 33% chance of being played and even when it is played, there is a delay applyed that it doesn't sound at the same beat, sort of, it variates. Every time it has to play it waits somewhere between 100ms and 5 second.
![fmod_cave_water_drop_fx](/img/ggj23_rooted_warden/fmod_cave_water_drop_fx.png)
It is fun to test this. I found that sometimes, when the delay time reaches 5 seconds in that time frame it can call another water drop sound and when the delay start to begin it's effect you can hear two water drops with a slight delay. It sounds as if there are two water drops one after the other which is a cool effect. It seems like a bug, but I'll take it as a feature!

A lot of sounds were used from libraries. Some collected by me, but most of them from other bought or downloaded sources. The main idea was to practice FMOD and gain more knowledge with this middle-ware. Well of course it wasn't just a simple drag'n'drop. I edited the sounds to fit my needs by layering and using effects. Just a few examples of the SFX used here:
- Slime exploding {{< sound src="/img/ggj23_rooted_warden/E_Slime_Explode_03.mp3" class="E_Slime_Explode_03" >}}
- Slime appear {{< sound src="/img/ggj23_rooted_warden/E_Slime_Appear_02.mp3" class="E_Slime_Appear_02" >}}
- Player dashing {{< sound src="/img/ggj23_rooted_warden/P_Dash_03.mp3" class="P_Dash_03" >}}
- Attack whoosh {{< sound src="/img/ggj23_rooted_warden/P_Attack_whoosh_03.mp3" class="P_Attack_whoosh_03" >}}

## Music
Saturday was very productive, but the evening was coming to it's end. The venue this day is closing at 9PM. We had to leave the museum and we already had a backup plan for this. [Chark](https://chark.io/) office is 15min on foot from the place. We relocated there and started to work more hyped. I wasn't very keen on making music for this game, as with music I am more critical to myself. Also I don't produce music that often for games, I do live events with my `Novation Circuit`, but I don't put them in the same category. I was afraid that making a track isn't possible in a few days and here we are left with a few hours. But it had to be done, so I opened `Arturia Pigments` and `Vital`. 
{{< sound src="/img/ggj23_rooted_warden/Music_amb_Arpegiated_Loop_1.mp3" class="Music_amb_Arpegiated_Loop_1" >}}
{{< sound src="/img/ggj23_rooted_warden/Music_amb_Omnious_Loop_1.mp3" class="Music_amb_Omnious_Loop_1" >}}
{{< sound src="/img/ggj23_rooted_warden/Music_amb_Random_Sequencer_1.mp3" class="Music_amb_Random_Sequencer_1" >}}
{{< sound src="/img/ggj23_rooted_warden/Music_amb_Sci-Fi_texture_01.mp3" class="Music_amb_Sci-Fi_texture_01" >}}

These are the main samples for the ambient music with some minor variations. And that is it, the whole magic is done in FMOD. I've made these loops play based on the progress of the player in game. The longer the player plays the more the higher the intensity level becomes.  The higher the intensity level the shift of music becomes, but up to a certain level. I'll show you how this FMOD event looks like.
![fmod_music_event](/img/ggj23_rooted_warden/fmod_music_event.png)
It seems a lot, but it is easy to grasp here what is happening. Let's start with the tracks. There are 6 tracks here. At different intensity levels - different tracks are being played. At intensity level 0 or 1 we play the first part which is looping an empty timeline. At level two the `Ominous` track is being played, then a `Texture` track is added, after that the `Texture` is no longer played and `Arpegiated2` track plays with the `Ominous` track and so forth.

The fun part is the top bar with all the green labels. These redirect to which region marker should the event track be playing - they are called transition markers. The white marker is the region marker, and the transition markers redirect to the marker based on the `MusicIntensity` value. So if we have a value between 4 and 5, the timeline cursor will jump to the `Fourth` label.
![fmod_music_transistion_condition](/img/ggj23_rooted_warden/fmod_music_transistion_condition.png)

Here is an example of how this works
{{< video src="/img/ggj23_rooted_warden/fmod_music_intensity.m4v" poster="/img/ggj23_rooted_warden/fmod_music_intensity.png" >}}

## Last touches
Well I finished with the music past 2AM and got home at about 3AM. Others stayed for longer. Edvinas who entered beast mode, stayed there until 7AM. At the venue we discussed that he will probably won't come until the submission time is over, but at about 9-10AM he wrote that he will be there in 30min. And so we continued. Airidas made the amazing core through the night so I supplemented it with a sound effect.

At this point it was time to work with UI, so the click sound was added and the snapshot event created. It is amazing how easy it is to use snapshots. They are called the same way as any audio event is called from FMOD. I added a multi-band EQ and lowered the volume sounds to all the music and SFX except for the UI elements. So on entering the menu it lowers the volume and adds a low-pass filter and exiting the menu it goes back to normal. The bug that I made is that I placed the FMOD event emitter by accident on the UI prefab itself and it always called it when anything was happening with UI. So even turning off the menu it would enable the snapshot. Took me a while, but I finally found it, deleted it and it was working as intended.

And this was it. The deadline was upon us, we made some cuts and delivered the game. Then in the last 20min we started to montage the trailer after sending the gameplay footage. In the mean time I tried to make the loops into a trailer song. And this is the result: 
{{< sound src="/img/ggj23_rooted_warden/Trailer_Music.mp3" class="Trailer_Music" >}}

It was an intense weekend but I LOVE the output. This game looks very good considering that it was done in one weekend. I want to thank the team because every single one of them made a fantastic job and it was very pleasant and fun to work with everyone! So thank you!

# Technology
So all of the software used for this game is FMOD for implementation and Reaper for samples. Using FMOD in this project was a huge advantage to the whole project. The workflow was swift, all the needed effects are already there, no need to make a script for an effect, or make an audio pool to randomize samples from. It has everything you need and more. Sending values from Unity to FMOD events let's you use it in was that can enhance audio, like linking it to a reverb or a multi-band EQ. 

Also I got to learn new things to use which I haven't used before - snapshots. I've tried to fiddle with it, but didn't put much time into it. But now it seemed like the perfect chance. It works the same way as playing sounds. Using the same FMOD's event emitter component to play and stop the snapshot. Simple to use, though I had an issue because I left one event emitter constantly calling it, so I spent a few hours trying to find the error.

FMOD components:
- 14 events 
- 1 snapshot
- 2 Events were music - Menu music and Level music
- 11 (+ 1) Events for SFX (one bonus event we didn't use because it was only a jump test event to check if FMOD is working with Unity).

# Result
The game can be downloaded from [GitHub](https://github.com/ugnelis/moon-gale).
Here is the trailer video.
{{< video src="/img/ggj23_rooted_warden/MoonGale_RootedWarden.m4v" poster="/img/ggj23_rooted_warden/MoonGale_RootedWarden.png" >}}
