---
title: "Project setup for better workflow on Unveiling"
subtitle: "My process and workflow of audio creation and implementation for the game Unveiling "
date: 2024-01-09T15:20:50+03:00
tags: ["Unveiling", "sfx", "FMOD", "Chark", "Reaper"]
---

Before diving into a project, I believe that a crucial step is to plan the workflow that will guide the entire process. It's essential to develop a structured approach and stick to it. To streamline my work, I've considered optimizing my use of [Reaper](https://www.reaper.fm/) and [FMOD](https://www.fmod.com/).

When working with **Reaper**, I find that naming conventions are crucial for understanding and efficiently handling files after rendering. As for **FMOD** events, I use a similar naming system to the asset files. However, importing files into **FMOD** was a bit tedious for me initially.

I explored the integration **FMOD** has with **Reaper**, but I'll discuss that later. As the saying goes, a good workflow is half the job done, right?

# Reaper setup
The primary objective here is to establish a workflow for both asset files and projects. I'll focus on two critical steps that are currently of utmost importance to me: naming conventions and project organization.

Firstly, let's delve into the significance of a consistent naming convention. This aspect is vital for clarity and efficiency, ensuring that asset files are easily understandable and manageable. A well-thought-out naming system can significantly enhance the overall organization and accessibility of the files. I had issues with this, because I wrote a misleading title, that tooks like a half an hour of chatter just of this. My mistake!

Next, I want to highlight the importance of structuring projects effectively. Organizing projects systematically is key to a streamlined workflow. By implementing a logical project structure, it becomes easier to navigate through files, collaborate with others, and maintain an easy development process.

These two aspects, naming conventions and project organization, play a pivotal role in setting up an effective workflow for asset files and projects alike.

## Naming convention
At first I had come up with the naming system here. I made them into three different groups:
- Music
- Sound Effects
- Voice Overs

So, this is where I start building my groups. It comes in handy down the line when I'm mixing in the middleware. As I go forward, I break them into sub-groups, and those have their own sub-groups, and so on. It's all about making sure I can find exactly what I need without getting lost in a ton of events.

For music I know that there wouldn't be much of it so it got divided into two parts:
- Drones
- General

Same as for the voice overs, there are two types of voices:
- NHI (non human intelligence)
- Player

The player doesn't have voice lines, but only breathing sounds, but still I wanted to extract it from others for mastering purposes and in the end it didn't seem logical to add it as SFX. As for the NHI, there was a lot of the samples - around 250 individual samples. They were grouped by the level that they are going to be used in:
- Forest
- Desert
- Pyramids
- Museum
- Simulation

And then comes the biggest part - SFX. These are going to be the biggest part of all of the audio. I grouped them into:
	- Ambient
	- Player
	- General
	- Interactable
	- Museum
	- NHI
	- UI

As for the naming, I used a system that maybe not be that understandable at first sight, but it's easier for me:
- M_ - main group type for music
	- Dr_ - drones for the sub group type
	- Ge_ general for the sub group type
- S_ - main group type for SFX
	- Am_ - ambience
	- Pl_ - player
	- Ge_ - general
	- In_ - interactable
	- Mu_ - museum
	- Nh_ - NHI
	- Ui_ - UI
- V_ main group type for VO
	- En_ - for the entity
	- Pl_ - for the player

Later on, I considered adding another layer of abbreviations for SFX names. For instance, for the player's sub-groups like Impacts, Footsteps, Jumps, etc., I name them accordingly:
- S_PlIm_Concrete - this would mean that it is a `SFX` oriented on the `Player` and specifically `Impacts`.
- S_GeCa_EngineFail - this would mean that it is a `SFX`, the sub-group is `General` and `Ca` would be for `Car`.

You get the idea. I'm still not sure if this is the ideal approach. Perhaps using full names would be better, but I'll figure that out in future projects. There's always room for improvement!

## Project Setup

In the past, I tried work with everything into one project — definitely not the wisest choice. With more experience, I've shifted to managing multiple projects. The project naming is still a bit chaotic and needs refinement, but here's a glimpse into the current state of my project folder
![project_folder.png](/img/unveiling_project_setup/project_folder.png)

You can understand most of it, but some are still misleading for me which to use like `SG_NHI_UFO` and `SG_UFO`. One is for drones, guess which one. Yeah, I didn't think this through with the naming. And in some of those projects there are some inconsistencies especially for the ones that were done on the last weeks before the release.

But that's not what I'm getting into now. The main point I want to bring up is that inside, I've set up Reaper sub-projects that the main project calls. In these sub-projects, I create all the tracks, samples, and FX chains, and then in the main project, I export the files. This trick helps cut down on CPU load and makes it easier to work with the rendered assets.
![project_main.png](/img/unveiling_project_setup/project_main.png)

I rely on regions for exporting asset files, and with Reaper's wildcards, it becomes a breeze to export the specific naming I need for different types of audio assets.

Another reason for using sub-projects within the main project is to avoid having any effects attached to the tracks. Linking the Reaper project with FMOD and refreshing the exported assets from FMOD causes crashes and generates error logs if there are effects on the tracks. It either doesn't import the assets or imports them corrupted. It's a bit of an extra step, but it works for now. I'm still on the lookout for a better approach to seamlessly link Reaper projects with FMOD projects.

# FMOD setup
Now in FMOD, as I mentioned, I've based the events on the audio file names as you can see here:
![fmod_events_hierarchy.png](/img/unveiling_project_setup/fmod_events_hierarchy.png)
It makes things a lot tidier and more accessible when I need them

"Since it's a relatively small game with around 30 minutes of gameplay, I decided to keep everything in a single master bank. I didn't feel the need to deal with multiple banks that I'd have to load or reload."

Now, onto the new technique I stumbled upon in FMOD – linking Reaper projects to FMOD. I absolutely love this feature! You simply drag the DAW project into FMOD's asset tab, specify the directory of your exported files, and upon refreshing, it imports the new files. No more navigating through file directories, no more drag and drops – just a refresh, and it's all here!
![fmod_asset_hierarcy.png](/img/unveiling_project_setup/fmod_asset_hierarcy.png)

As an example, if I happen to leave an effect on a Reaper track, FMOD throws up this error.
![fmod_error.png](/img/unveiling_project_setup/fmod_error.png)

That's why in Reaper's main project, I opt for sub-projects, keeping the main one clean solely for exporting purposes.

Lastly, for the mixer, I adopted the same approach of grouping track events. This will be beneficial down the line when balancing the overall audio levels.
![fmod_routing.png](/img/unveiling_project_setup/fmod_routing.png)

# Thank you
Thank you for reading! I hope that this was informative for you!
If you are interested more in the game there is a [Youtube video](https://www.youtube.com/watch?v=vzC4W_8MLMo) and a [Steam link](https://store.steampowered.com/app/2719950/Unveiling/)