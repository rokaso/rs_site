---
title: Generating wind from a noise sample in a game engine 
date: 2021-10-28
tags: ["tools", "unity", "sfx"]
---

In here I'll be writing about how I added an interesting system of wind SFX in Unity by using white noise and Unity's sound mixer effects. I'd call this a dynamic wind SFX even. Because right know this is directly linked with the boat's speed velocity. As it goes faster the wind becomes more high pitched and when it is going slower the wind is more on the low-end.

# Generated Wind Effect
I found this technique in one of [Blipsounds](https://blipsounds.com/) [video's](https://www.youtube.com/c/Blipsounds) by Ryan Stunkel. The [video](https://www.youtube.com/watch?v=Sq9ZnZr1Xqc) is about whooshes here but to make the wind effect you just need to automate the resonant frequency point to a certain range. Upon testing I found that from 300Hz to 1500Hz is a good range here. But this is due to adding high-pass and low-pass filters that also cut off some of the frequencies. The range to 1500Hz is just for some low volume texture. Previous testing held best results at 1000Hz without other filters. Going above it made it sound too synthetic.

## Preparing the engine
First we add the white noise sound into Unity. It is a good practice to add game objects for sounds when working with prefabs to have easy access when more of the same prefabs are generated into the engine. This will be more tidy and you'll have the sounds at hand. Will save time and nerves trying to find all the sound effects, trying to add them every time.

{{< video src="/img/unity_wind_generated/add_object.m4v" >}}

In the object we add a component "Audio Source" which we link the sound that will be played (Also, if you are trying to do this by yourself, don't forget to add an "Audio Listener" component. This was previously added, so I didn't want to break the flow of the architecture).

{{< video src="/img/unity_wind_generated/add_audio_source.m4v" >}}

If we test this out it should play white noise once the game is started.
{{< video src="/img/unity_wind_generated/white_noise_on_game.m4v" poster="/img/unity_wind_generated/white_noise_on_game.png" >}}

Next we want to make this more windy. Going to Window -> Audio -> Audio Mixer (or CTRL + 8) opens up the mixer. At first I found that the Master mixer that is added by default didn't let me link it to my audio source component so I deleted it and added a new one. Maybe it was alright with the default one, but I got impatient fast.

{{< video src="/img/unity_wind_generated/unity_mixer.m4v" >}}

Now in the inspector let's add a lowpass, highpass filter and an EQ. Meddle a bit with parameters to find the sweet spot for the wind. Changing ParamEQ Centre freq parameter we can start to hear the gusts of wind. 

{{< video src="/img/unity_wind_generated/filters_on_wind.m4v" >}}

This is the parameter that will be attached to the boat's speed. Right clicking it select the "Expose 'Centre freq' to script". And in the mixer menu top right name your parameter in "Exposed Parameters". This gives us control for the gust automation from scripts.

{{< video src="/img/unity_wind_generated/exposed_params.m4v" >}}


## Coding the control

Edvinas gave me a recommendation on making parameters easy configurable in Unity. All the parameters are made with serialized fields with `[SerializeField]`. This makes faster parameter changes when adding more game objects with the same script. 
![serializedfield scripts](/img/unity_wind_generated/serializable_fields.png)
For making the frequency slider we just need to add a range parameter:
```C#
		[SerializeField]
        [Range(0, 2000)]
        private float frequency = 0f; 
```
Currently this is a work for testing purposes so we add a timer that keeps on calling our needed function periodicaly. In this instance it is called every 0.1s. This will let the parameter change be more responsive to change.
```C#
        [Min(0.1f)]
        [SerializeField]
        private float time = 1f;

        [Min(0.1f)]
        [SerializeField]
        private float repeateRate = 0.1f;

        private void Start()
        {
            InvokeRepeating("SetWindFrequency", time, repeateRate);
        }
```
`SetWindFrequency` is the function that will be called, `time` is a delay for when the first function will be called. And `repeatRate` how periodically it will be called.
So. For the magical part:
```C#
	[SerializeField]
    public AudioMixer masterMixer;

    [SerializeField]
    [Range(0, 2000)]
    private float frequency = 0f;

    [SerializeField]
    private string eqName = "Wind EQ";

    [SerializeField]
    private FloatReference currentSpeed;

	public void SetWindFrequency()
    {
        frequency = currentSpeed.Value * 10;
        masterMixer.SetFloat(eqName, frequency);
        Debug.Log("Current Freq:" + frequency);
    }
```
This is a bigger chunk to go through. Let us start with `AudioMixer` this creates an instance of Unity's audio mixer which will help us access the EQ parameters. `eqName` is the EQ parameter that we named in the exposed parameters. And `currentSpeed` is the parameter for the boat's speed. This was already done by Edvinas and I didn't do much digging for now into it, just used it for the parameter control. As for the method `SetWindFrequency` itself. Right now the max speed I could reach was about 120km/h. So that makes that the max frequency will be to 1200Hz. We use `masterMixer.SetFloat(eqName, frequency);` to get the parameter by name which is `Wind EQ` and set it's value. And the `Debug.Log` command is just to check what values have been passed on to confirm that it is working.

# Results
{{< video src="/img/unity_wind_generated/result_video.m4v" poster="/img/unity_wind_generated/result_video.png" >}}


# Conclusion
For now this is great. But this can be improved by adding an LFO to make short wind gusts while it is blowing just to make more audible motions. Also after the gusts being added there will be space to think about adding sail sounds. This I think will be done with a number of cloths.
