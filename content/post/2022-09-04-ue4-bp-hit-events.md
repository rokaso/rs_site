---
title: Using UE4 Hit Events in Blueprints
subtitle: Generating log dropping sounds in UE4 with the blueprint system
date: 2022-09-04
tags: ["ue4", "unreal engine 4", "sfx", "VR", "blueprints"]
---

Playing sounds on collision events is probably one of the most used event types in game audio. This can be by dropping an item on the ground, wall, table or bashing the item into other objects for example hitting a sword into a rock.

### Preparing the Component
In the components tab we add a procedural mesh component by pressing on the `Add Component` button, scrolling to the rendering section and finding the `Procedural Mesh` component (or upon pressing just typing the name).
![add_component_procedural_mesh](/img/ue_hit_events/add_component_procedural_mesh.png)

In the details of the `Procedural Mesh` component of which we created we find the `Collision` window and on it Collision tab. To make it work for events that we want to use the `Simulation Generates Hit Event` has to be on. More about his can be found [On Component Hit](https://docs.unrealengine.com/5.0/en-US/API/Runtime/Engine/Components/UPrimitiveComponent/OnComponentHit/).
![object_collision](/img/ue_hit_events/object_collision.png)

### The Events
To start of in the `Procedural Mesh` component we scroll down to the event tab and press the `+` button on `On Component Hit`. This generates us the start of the event function.
![component_hit_event](/img/ue_hit_events/component_hit_event.png)

And add our sound cue/asset that we want to play when the event is called. As I'm working on a scene with wood chopping. I'm going to add dropping sounds when the log is dropped on any type of surfaces. 
![event_hit_sound_play](/img/ue_hit_events/event_hit_sound_play.png)

And now we have a problem, for some reason the logs try to play a hundred of samples at the same time. I noticed when testing the functionality of this that sometimes the log that has fallen on the ground is still calling the sound cue. Adding prints with the magnitude of the impulse I found out that even lying on the ground it gave me an impulse of around 30 of the vectors length. While a simple small drop, like 2cm above the ground, had about 290 of the vectors length.

So the logical approach is to add a threshold when the sound should be played and when not. By using a `Branch` statement and the `Vector Magnitude` calculator we can check if the magnitude is more than 250 or not. And if it is true we can play the sounds.
![event_hit_sound_play_filtered](/img/ue_hit_events/event_hit_sound_play_filtered.png)

To even go further I started to play with the Log sizes and it's mass. When the size of the log is increased or decreased the mass of it also changes respectively. If in the game an artist or developer will want to make the logs bigger, we'll hit into the same problem that there will be multiple hit events generating. And if the log is going to be smaller then there is a chance that it might not get the events generated. So we will be calculating the magnitude of the impact based on the mass.

I did some testing with the sizes. And when the log is at a scale of 1. The minimum magnitude it generates is about 50 of the vectors length and the maximum is about 250 of the vectors length. So I'll be using these values for calculations.

![event_hit_with_mass_filtering](/img/ue_hit_events/event_hit_with_mass_filtering.png)

Here I check if the values are in the range of the wanted magnitude which is multiplied by the mass of the logs. This makes it more easier to generate sounds based on the size. As the value of the mass changes, the algorithms range adapts to it. This is very useful when we are chopping the log with an axe. As each chop makes the log smaller, it's mass gets smaller.

Next up what I wanted to do is to have more responsiveness with the worlds surfaces. I want to have sounds played on different surfaces like wood, ground, metal, water, ect.

First of all we need to define the surface types that are there in the project itself.
Go to Edit -> Project Settings -> Engine -> Physics. Scrolling down there will be a list of `Physical Surfaces`. 

![physical_surfaces](/img/ue_hit_events/physical_surfaces.png)

Now we can add the check of the surface upon the hit events. For this we will use `Switch on EPhysicalSurface`. This allows us to play sounds based on which surface type has been called.

![switch_on_surfaces](/img/ue_hit_events/switch_on_surfaces.png)

For now I just want to have a ground sound and a wood sound. Just to see how  it is working.

And here is the result.

{{< video src="/img/ue_hit_events/result_video_ue4_event_hits.m4v" poster="/img/ue_hit_events/result_video_ue4_event_hits.png" >}}

### Conclusion

I'm very interested to know why the logs are generating multiple calls (and I mean a LOT). As to what I've understood is this should not be the case. Currently I have no idea why this is, but learning on maybe I'll find what is happening and will be able to fix this issue.