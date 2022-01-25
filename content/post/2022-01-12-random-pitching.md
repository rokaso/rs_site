---
title: Random pitch changing for samples in Unity
date: 2022-01-12
draft: false
tags: ["script", "unity", "sfx"]
---

Doing sound design you find yourself that you have a good sample to add to the game, but the sample is so good that any other would not fit, but you need more variations so that it wouldn't fatigue the ears but just making a wee bit of pitch shifting and exporting it seems cheesy. Well now, what if we would do that in the game engine itself? Now that would be more stylish, wouldn't it? This approach would save some memory. Let's see how this could be achieved in Unity.

# The script

There will be two scripts used here. The first one is used to add a sample and a little bit of tuning. For it we will add a pitch and a volume parameter which can be controlled with a slider.

``` C#
public class AudioPool
{
    public AudioClip clip;

    [Range(0f, 1f)]
    public float volume = 0.8f;
    [Range(0.1f, 3f)]
    public float pitch = 1f;

    [HideInInspector]
    public AudioSource source;
}
```

And for the second script. We will start with having a range in which the pitch will get changed. In Unity `1.0f` is the original sample pitch. Going lower than one will lower the pitch, and going higher than one will make the pitch higher. At `Start()` we initialize the sample and pass it's values.
We'll also add the minimum and maximum value as sliders for in which range will the pitch randomization will happen. 
``` C#
public class AudioRandomPitch : MonoBehaviour
    {
        [Range(0.1f, 3f)]
        public float minimum = 0.1f;
        [Range(0.1f, 3f)]
        public float maximum = 3f;

        public AudioPool sound;
        void Start()
        {
            sound.source = gameObject.AddComponent<AudioSource>();
            sound.source.clip = sound.clip;

            sound.source.volume = sound.volume;
            sound.source.pitch = sound.pitch;
        }
    }
```

Now, for the range randomizing. Here we will add a `Play()` method. In it will be randomization begin. We will take the sample the we got initialized and add it here to `pool`. Pass the volume value that we set of the sample and get the pitch. `Random.Range(min, max)` is (as you can tell) for randomizing the values between minimum and maximum value. After it is calculated we play the source file with out pitch.

``` C#
    public void Play()
    {
        AudioPool pool = sound;
        pool.source.volume = pool.volume;
        pool.source.pitch = Random.Range(minimum, maximum);
        pool.source.Play();
    }
```

The second script in full will look like this.
``` C#
public class AudioRandomPitch : MonoBehaviour
    {
        [Range(0.1f, 3f)]
        public float minimum = 0.1f;
        [Range(0.1f, 3f)]
        public float maximum = 3f;

        public AudioPool sound;
        void Start()
        {
            sound.source = gameObject.AddComponent<AudioSource>();
            sound.source.clip = sound.clip;

            sound.source.volume = sound.volume;
            sound.source.pitch = sound.pitch;
            }

        public void Play()
        {
            AudioPool pool = sound;
            pool.source.volume = pool.volume;
            pool.source.pitch = Random.Range(minimum, maximum);
            pool.source.Play();
        }
    }
```

The second script uses the first script for the audio. This is especially useful for when we will need to randomize samples instead of pitch. It takes the parameters of the audio and Unity Audio Emitter default settings and transfers to our object. 

This is how our script should look like when added to a game object.

![second script](/img/unity_pitch_random/second_script.png)

# Adding the sound

Now we will be needing to add our sample. As in this game the orbs will be used a lot of times I'll be adding this into the prefab which allows us to add only one time and the rest of the orbs will be updated. As in my previous post lets add a game object called SFX and then another game object into it. Making it separate and not to get more confusing.

{{< video src="/img/unity_pitch_random/Object.m4v">}}

And let's add our script to our Pick Up object and attach a sound to it.

{{< video src="/img/unity_pitch_random/Pitch_Random_Script.m4v">}}

And add it to the event where it is picked up. This is also a script but done for the orbs on how they work - their mechanics. I won't go much into this script now. It's done using [scriptable events](https://github.com/chark/scriptable-events) (which can be downloaded from github and there's a documentation if you want to learn to use it) made by my friend [Edvinas](https://edvinas.dev/). In here I just add a field where my sound will play after collecting the orb and select the function we added to our script.

{{< video src="/img/unity_pitch_random/Pitch_Play.m4v">}}

# Results

Now when we play test what we've done we should hear different pitches of the sample we added every time we pick up an orb.

{{< video src="/img/unity_pitch_random/result.m4v">}}

# Conclusion

Using pitch shifting can help us to make the sound scene more dynamic. Instead of listening to only the same sample we add pitch variation, which helps with ear fatigue.
Also after showing this functionality I've been suggested to make the pitch going up if in a certain time-frame if the orb is caught. Seems like an interesting functionality to do!