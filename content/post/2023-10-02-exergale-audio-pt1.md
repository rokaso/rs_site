---
title: "Exergale: audio in game"
subtitle: "The audio and implementation of them used in VR game Exergale"
date: 2023-10-02T13:20:50+03:00
tags: ["Unity", "ExerGale", "sfx", "VR", "FMOD", "Chark"]
---

This year, I've been neck-deep in two projects, putting in loads of work, and truth be told, it's been so hectic that I've neglected this blog for quite a while. But hey, better late than never, right?

Let me tell you about one of those projects, [ExerGale](https://exergale.com/), a VR game that's all about flying, gliding, and climbing through a fantastic world. Right now, the game offers two modes: one where you can just soar around like a bird, and another where you hit a button and go on a crystal-collecting spree to rack up a high score.

So, what's got me excited? Well, I want to chat about what's cool in the sound department of this game.
# Water bounce

Incorporating the water bounce mechanic into the game adds an extra layer of excitement to flying around the islands. When you, as a player, touch the water, it doesn't abruptly halt your progress; instead, it allows you to maintain control, giving you a slight boost upward, much like a skipping stone.

Now, let's discuss how the water bounce should sound. I've opted to utilize the "speed on collision" parameter, which triggers three distinct sample types:
- **Hard bounce** {{< sound src="/img/eg_audio_pt1/S_InIm_Water_Bounce_Hard_1.mp3" class="S_InIm_Water_Bounce_Hard_1" >}}
- **Medium bounce** {{< sound src="/img/eg_audio_pt1/S_InIm_Water_Bounce_Medium_1.mp3" class="S_InIm_Water_Bounce_Medium_1" >}}
- **Soft bounce** {{< sound src="/img/eg_audio_pt1/S_InIm_Water_Bounce_Small_1.mp3" class="S_InIm_Water_Bounce_Small_1" >}} 

Here's the FMOD parameter setup for water bounce.
![fmod_event](/img/eg_audio_pt1/Pasted_image_20230826131252.png)
The sound triggered by the "speed on collision" parameter is fairly straightforward. However, I encountered issues when the parameter transitioned between one track and another. This resulted in an overlap of sound samples, where both samples played simultaneously. To address this, I introduced a slight gap between the tracks within their automation ranges, with a gap size of 0.001 in value.

Although it's tricky to exactly predict the speed on where the two samples might overlap, I chose to resolve this problem to guarantee a smooth experience and peace of mind.

# Statue Turrets

When you're immersed in a game, you're naturally prepared for some challenges along the way. While striving for a high score in [ExerGale](https://exergale.com/), mastering the art of flying is key to achieving your best results. However, what if there were obstacles that could slow you down? Now, instead of effortlessly gliding through the skies and valleys, you must skillfully evade projectiles aimed at you. Of course, if you're skilled, you can even use them as a boost 😉, but that's a different story.

Let's delve into the sounds of the statue turrets. I've categorized them into five distinct states:
- **Statue Charging:** This is the sound when the statue turret is building up power. {{< sound src="/img/eg_audio_pt1/S_InEn_Statue_Charging.mp3" class="S_InEn_Statue_Charging" >}} 
- **Statue Destroyed:** The sound that accompanies the destruction of the statue turret. {{< sound src="/img/eg_audio_pt1/S_InEn_Statue_Destroyed_3.mp3" class="S_InEn_Statue_Destroyed_3" >}} 
- **Statue Projectile Impact:** When the turret's projectile hits its target, this sound comes into play. {{< sound src="/img/eg_audio_pt1/S_InEn_Statue_ProjectileImpact_4.mp3" class="S_InEn_Statue_ProjectileImpact_4" >}} {{< sound src="/img/eg_audio_pt1/S_InEn_Statue_ProjectileImpact_Voice_1.mp3" class="S_InEn_Statue_ProjectileImpact_Voice_1" >}} 
- **Statue Projectile Wind:** The sound of the projectile whizzing through the air before impact.{{< sound src="/img/eg_audio_pt1/S_InEn_Statue_ProjectileFlyby_1.mp3" class="S_InEn_Statue_ProjectileFlyby_1" >}} 
- **Statue Shoot:** This sound is emitted when the turret fires its projectile. {{< sound src="/img/eg_audio_pt1/S_InEn_Statue_Shooting_5.mp3" class="S_InEn_Statue_Shooting_5" >}} 
## Using voices

As I've been playing around with these statues, I've been thinking about how to match their looks with the right sounds. After some testing, I had this idea to infusing a shamanic essence into the soundscape. You see, these statues, reminiscent of a bygone era in ancient civilizations, expel enigmatic purple orbs. Now, what kind of sound could go with that? How about some cryptic language that you can't understand, a deep voice, and a subtle rhythmic undertone? It'd be like they're chanting some crazy magical spell.

As an example:
- Projectile impact:
	- My voice {{< sound src="/img/eg_audio_pt1/29-230609_1442.mp3" class="29-230609_1442" >}} 
	- After FX applied {{< sound src="/img/eg_audio_pt1/S_InEn_Statue_ProjectileImpact_Voice_4.mp3" class="S_InEn_Statue_ProjectileImpact_Voice_4" >}} 
- Statue charging:
	- My voice  {{< sound src="/img/eg_audio_pt1/07-230607_1553.mp3" class="07-230607_1553" >}} 
	- After FX applied {{< sound src="/img/eg_audio_pt1/S_InEn_Statue_Charging.mp3" class="S_InEn_Statue_Charging" >}} 

## Using game engine parameters 

Another intriguing use of voice within the game involves the utilization of a crow's vocalization. This particular audio sample is sourced from the [Boom Library - Birds of Prey](https://www.boomlibrary.com/sound-effects/birds-of-prey/).

Here's how it works: In FMOD, I've created an event that functions as a short loop. Inside this event, there are three distinct crow samples that are randomly selected each time the event is triggered. Additionally, I've implemented a distance parameter obtained from Unity. This parameter represents the distance between the player and the sound source.

When the source is far away, no sound is heard. However, as the source approaches, the volume and equalization (EQ) parameters of the sound dynamically change based on the proximity, providing an immersive auditory experience. ![fmod_event](/img/eg_audio_pt1/Pasted_image_20230927141120.png)

Finally, this feature is integrated with the statue's projectile. When the projectile swiftly passes by the player, you can distinctly hear the effect in action.
{{< video src="/img/eg_audio_pt1/Eg Turretsounds.m4v" >}}

# Ambience

For ambient sounds, I've implemented two techniques.

The first one is the wind ambiance, which is controlled by the flight speed. I've detailed this technique in a previous blog post - [Generating Wind Sounds](https://sutkusaudio.com/post/2021-10-15-generating-wind-sounds/).

The second technique involves the ambiance of the water. I've linked the ocean wave crashing FMOD event to the water source, and the sound volume changes based on the distance between the player and the water source.

Now, it may sound like I've simply used the FMOD spatializer effect, but I haven't completed the ocean wave ambiance yet. Currently, it's a 2D sound, meaning that regardless of the head position, the audio sounds the same, and you can't determine the source's location. My plan to enhance this is to make the audio source track the player within the water body and adjust the sound direction to reflect the water's orientation.

# Echo chamber

Lastly, I'd like to discuss an audio feature in the game known as the echo chambers. So, what exactly are these? Well, they're essentially invisible boxes within the game scene. When a player enters one, it triggers an event in FMOD that either starts or stops the [Snapshots](https://www.fmod.com/docs/2.02/studio/glossary.html#snapshot), in which I can set a chain of effects.

For this, I make use of the reverb effect to enhance the desired experience.

Setting up this kind of system is actually quite simple. It's called just like any other FMOD audio event. The key is to remember to stop the snapshots. It operates in a manner similar to an FMOD event loop – if you want it to end, you have to manually stop it.

But here's the thing: it's a global FMOD parameter. So, when you reload the scene or move to another scene, the snapshot doesn't clear on its own. You'll need to take extra steps to turn off the snapshot; it's not tied to a specific game object.

In contrast, with FMOD audio events, if the associated game object is destroyed, the audio is automatically cut off. This works wonderfully for loops, as they are destroyed with the game objects when you switch to a new level. However, the same convenience doesn't apply to snapshots. As I mentioned earlier, you have to take additional measures to switch them off.

{{< video src="/img/eg_audio_pt1/Eg Reverb Blog.m4v" >}}
This is the echo chamber in use.

# Thank you
Thank you for reading this post. While writing it, I've realized that I can delve deeper into some topics, and I likely will. I hope you found this post informative as well. 

If you have any suggestions while reading this and want to let me know you can contact me via email: rokas@sutkusaudio.com or on [instagram](https://www.instagram.com/sutkusaudio/).