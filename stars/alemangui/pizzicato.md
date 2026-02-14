---
project: pizzicato
stars: 1711
description: Library to simplify the way you create and manipulate sounds with the Web Audio API.
url: https://github.com/alemangui/pizzicato
---

Note

Due to lack of time to focus on this project, **I'm actively looking for maintainers** who might be interested in working on Pizzicato. Don't hesitate to contact me! In the meantime, consider the project deprecated.

A Web Audio library
-------------------

Pizzicato aims to simplify the way you create and manipulate sounds via the Web Audio API. Take a look at the demo site here.

Table of contents
-----------------

-   Get Pizzicato
    -   npm
    -   bower
    -   cdnjs
    -   Installing and testing
-   TL;DR: How does it work?
-   Create a sound
    -   Sounds from a wave
    -   Sounds from a file
    -   Sounds from input
    -   Sounds from a function
-   Using sounds
    -   play()
    -   pause()
    -   stop()
    -   clone()
    -   addEffect()
    -   removeEffect()
    -   volume
    -   attack
    -   release
    -   frequency
    -   Events
        -   play
        -   pause
        -   stop
        -   end
    -   Connecting sounds to AudioNodes
-   Grouping sounds
    -   Create a group
    -   addSound()
    -   removeSound()
    -   addEffect()
    -   removeEffect()
    -   play()
    -   pause()
    -   stop()
    -   volume
-   Effects
    -   Delay
    -   Ping Pong Delay
    -   Dub Delay
    -   Distortion
    -   Quadrafuzz
    -   Flanger
    -   Compressor
    -   Low-pass filter
    -   High-pass filter
    -   Stereo Panner
    -   Convolver
    -   Reverb
    -   Ring Modulator
    -   Tremolo
    -   Connecting effects to and from AudioNodes
-   Advanced
    -   Accessing the audio context
    -   Using Pizzicato objects in a web audio graph
    -   General volume
    -   Memory management
-   Support
    -   Browsers
    -   Audio formats

Get Pizzicato
-------------

### npm

```
npm install pizzicato
```

### bower

```
bower install pizzicato
```

### cdnjs

Full source code:

<script src\="https://cdnjs.cloudflare.com/ajax/libs/pizzicato/0.6.4/Pizzicato.js"\></script\>

Minified:

<script src\="https://cdnjs.cloudflare.com/ajax/libs/pizzicato/0.6.4/Pizzicato.min.js"\></script\>

### Installing and testing

_Ensure you have gulp installed:_ `npm install -g gulp`.

Checkout the project and install dependencies with :

```
npm install
```

Run tests with:

```
npm run test
```

By default, Firefox is used for local testing. If you'd like to use Chrome you can use the setting active in TravisCI. To do so, go to `karma.conf.js`, line 5, and change the browsers array to :

```
browsers: ['Chrome_travis_ci'],
```

Build without tests with: `npm run build` or `npm run watch`

TL;DR: How does it work?
------------------------

Include Pizzicato in your site

<script src\="./Pizzicato.js"\></script\>

Create a sound

var sawtoothWave \= new Pizzicato.Sound({ 
    source: 'wave',
    options: {
        type: 'sawtooth'
    }
});

Add effects

var delay \= new Pizzicato.Effects.Delay();
sawtoothWave.addEffect(delay);

Play it!

sawtoothWave.play();

Create a sound
--------------

To create a new sound, use the `Pizzicato.Sound` constructor, which takes an object with the sound's `description` as argument and a callback that will be executed when the sound is ready to be used. If an error occurs, the callback will be called with the error as a parameter.

var sound \= new Pizzicato.Sound(Object description, \[Function callback\]);

For example:

var click \= new Pizzicato.Sound({ source: 'wave' }, function(error) {
    if (!error)
        console.log('Sound ready to use!');
});

Typically, the `description` object contains a string `source` and an object `options`. The `options` object varies depending on the source of the sound being created.

For example, this objects describes a sine waveform with a frequency of 440:

{
    source: 'wave',
    options: {
        type: 'sine',
        frequency: 440
    }
}

Sounds can be created from a variety of sources.

### Sounds from a wave (example)

To create a sound from an oscillator with a certain waveform, use the `source: wave` in your description. Additionally, the following optional parameters are possible inside the `options` object:

-   `type` _(Optional; `sine`, `square`, `triangle` or `sawtooth`, defaults to `sine`)_: Specifies the type of waveform.
-   `frequency` _(Optional; defaults to 440)_: Indicates the frequency of the wave (i.e., a 440 value will yield an A note).
-   `volume` _(Optional; min: 0, max: 1, defaults to 1)_: Loudness of the sound.
-   `release` _(Optional; defaults to 0.4)_: Value in seconds that indicates the fade-out time when the sound is stopped.
-   `attack` _(Optional; defaults to 0.4)_: Value in seconds that indicates the fade-in time when the sound is played.
-   `detached` _(Optional; defaults to false)_: If true, the sound will not be connected to the context's destination, and thus, will not be audible.

var sound \= new Pizzicato.Sound({ 
        source: 'wave',
        options: { type: 'sawtooth', frequency: 440 }
});

Creating a Pizzicato Sound with an empty constructor will create a sound with a sine wave and a frequency of 440.

var sound \= new Pizzicato.Sound();

### Sounds from a file (example)

In order to load a sound from a file, include the `source: file` in your description. Additionally, the following parameters are possible inside the `options` object:

-   `path` _(Mandatory; string or array of strings)_: Specifies the path of the sound file. It is also possible to have an array of paths to fallback on. Pizzicato will attempt to load the paths in order, passing on to the next one in case of failure.
-   `loop` _(Optional; boolean, defaults to false)_: If set, the file will start playing again after the end.
-   `volume` _(Optional; min: 0, max: 1, defaults to 1)_: Loudness of the sound.
-   `release` _(Optional; defaults to 0)_: Value in seconds that indicates the fade-out time once the sound is stopped.
-   `attack` _(Optional; defaults to 0.4)_: Value in seconds that indicates the fade-in time when the sound is played.
-   `detached` _(Optional; defaults to false)_: If true, the sound will not be connected to the context's destination, and thus, will not be audible.

var sound \= new Pizzicato.Sound({ 
    source: 'file',
    options: { path: './audio/sound.wav' }
}, function() {
    console.log('sound file loaded!');
});

It is possible to pass several paths to fallback in case of error:

var sound \= new Pizzicato.Sound({ 
    source: 'file',
    options: { path: \['./audio/sound-special-format.wav', './audio/sound.wav'\] }
}, function() {
    console.log('sound file loaded!');
});

Alternatively, you can also simply pass a string to the constructor with the path of the sound file.

```
var sound = new Pizzicato.Sound('./audio/sound.wav', function() {...});
```

Check the supported audio files that can be played with Pizzicato.

### Sounds from the user input (example)

It is also possible to use the sound input from the computer. This is usually the microphone, but it could also be a line-in input. To use this, add `source: input` in your description. The following optional parameters are possible inside `options` object:

-   `volume` _(Optional; min: 0, max: 1, defaults to 1)_: Loudness of the sound.
-   `release` _(Optional; defaults to 0)_: Value in seconds that indicates the fade-out time once the sound is stopped.
-   `attack` _(Optional; defaults to 0.4)_: Value in seconds that indicates the fade-in time when the sound is played.
-   `detached` _(Optional; defaults to false)_: If true, the sound will not be connected to the context's destination, and thus, will not be audible.

var voice \= new Pizzicato.Sound({
    source: 'input',
    options: { volume: 0.8 }
});

### Sounds from a function (example)

For more creative freedom, Pizzicato also allows direct audio processing. Sounds can be created from a Javascript function by including `source: script` in the description. The following parameters are possible in the `options` object:

-   `audioFunction` _(Mandatory; function())_: Function that will be called with the audio processing event.
-   `bufferSize` _(Optional; number - must be a power of 2.)_: This value controls how many sample frames will be processed at each audio process event. Lower values will result in lower latency, higher values help prevent glitches.
-   `volume` _(Optional; min: 0, max: 1, defaults to 1)_: Loudness of the sound.
-   `release` _(Optional; defaults to 0)_: Value in seconds that indicates the fade-out time once the sound is stopped.
-   `attack` _(Optional; defaults to 0.4)_: Value in seconds that indicates the fade-in time when the sound is played.
-   `detached` _(Optional; defaults to false)_: If true, the sound will not be connected to the context's destination, and thus, will not be audible.

For example:

var whiteNoise \= Pizzicato.Sound({
    source: 'script',
    options: {
        audioFunction: function(e) {
            var output \= e.outputBuffer.getChannelData(0);
            for (var i \= 0; i < e.outputBuffer.length; i++)
                output\[i\] \= Math.random();
        }
    }
});

Using sounds
------------

### Play (example)

You can play a sound by calling it's `play` function. It takes two optional parameters:

-   `when` _(number, defaults to 0)_: Time in seconds to wait before playing the sound.
-   `offset` _(number, defaults to 0)_: Time in seconds where the sound will start.

For example, the following code will wait two seconds, then play a sound starting from position 00:04:

sound.play(2, 4);

### Pause

You can pause a sound by calling it's `pause` function. Next time the sound is played, it will continue from where it left off.

sound.pause();

### Stop

You can stop a sound by calling it's `stop` function. Next time the sound is played, it will continue from the start of the sound.

sound.stop();

### Clone

You can clone a sound object by calling it's `clone` function. The object returned will have the same parameters as the original sound.

sound.clone();

### Add effects (example)

You can add effects to a sound object by calling it's `addEffect(effect)` function. The function gets as parameter a Pizzicato Effect (see effects).

-   `effect` _(type: Pizzicato.Effect)_: The effect to add to the sound object.

Example:

var sound \= new Pizzicato.Sound();
var delay \= new Pizzicato.Effects.Delay();
sound.addEffect(delay);

### Remove effects

You can remove effects that have been added to a sound object by calling it's `removeEffect(effect)` function. The function gets as parameter a Pizzicato Effect (see effects) that is already applied to the sound object.

-   `effect` _(type: Pizzicato.Effect)_: The effect to remove from the sound object.

Example:

var sound \= new Pizzicato.Sound();
var delay \= new Pizzicato.Effects.Delay();
sound.addEffect(delay);
...
sound.removeEffect(delay);

### Volume

Use the sound's `volume` property to modify its volume.

-   `volume` _(min: 0, max: 1, defaults to 1)_: The sound's volume

Example:

var sound \= new Pizzicato.Sound();
sound.volume \= 0.5;

### Attack (example)

Use the sound's `attack` property to modify its attack (or fade-in) value. This value eases the beginning of the sound, often avoiding unwanted clicks.

-   `attack` _(min: 0, max: 10, defaults to 0.04)_: The sound's attack.

Example:

var sound \= new Pizzicato.Sound();
sound.attack \= 0.9;

### Release (example)

Use the sound's `release` property to modify its release (or fade-out) value. This value eases the end of the sound, often avoiding unwanted clicks.

-   `release` _(min: 0, max: 10, defaults to 0.04)_: The sound's release.

Example:

var sound \= new Pizzicato.Sound();
sound.release \= 0.9;

### Frequency

If you started a sound of type wave, you can modify the frequency of the oscillator by altering the `frequency` property.

-   `frequency` _(defaults to 440)_: The oscillator's frequency of a sound of type wave.

Example:

var sound \= new Pizzicato.Sound();

sound.play();

// go up an octave
sound.frequency \= 880; // a5

### Events

It is possible to subscribe to the following events that will occur on the Sound object: `play`, `pause`, `stop`, `end`.

#### `play` event

The `play` event will be fired when the sound is played.

Example:

var sound \= new Pizzicato.Sound();

sound.on('play', function() {
  //...
})

#### `pause` event

Fired when the sound is paused. For example:

var sound \= new Pizzicato.Sound();

sound.on('pause', function() {
  //...
})

#### `stop` event

Fired when the sound is stopped. For example:

var sound \= new Pizzicato.Sound();

sound.on('stop', function() {
  //...
})

#### `end` event

Fired when the sound has ended. This is only valid for sounds coming from a file. For example:

var sound \= new Pizzicato.Sound();

sound.on('end', function() {
  //...
})

###Connecting sounds to AudioNodes It is possible to connect AudioNodes to sound objects by using the `connect` method. More details in the advanced section of this file.

Grouping sounds (example)
-------------------------

Groups are a way to handle multiple `Pz.Sound` objects at the same time.

### Create a group (example)

The `Pizzicato.Group` constructor takes an optional array of sound objects. Please note these sounds must be detached for them to be usable inside a group (more details about detached sounds here).

-   `sounds` _(array, defaults to \[\])_: The sounds to be added to the group.

Example:

var drums \= new Pizzicato.Sound('./audio/drums.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');

var group \= new Pizzicato.Group(\[drums, guitar\]);

### addSound()

To add a sound to a group, use the function `addSound()`, which receives one parameter:

-   `sound` _(Pz.Sound, mandatory)_: The sound to be added to the group.

Example:

var drums \= new Pizzicato.Sound('./audio/drums.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var group \= new Pizzicato.Group();

group.addSound(drums)
group.addSound(guitar)

### removeSound()

To remove a sound to a group, use the function `removeSound()`, which receives one parameter:

-   `sound` _(Pz.Sound, mandatory)_: The sound to be removed from the group.

Example:

var drums \= new Pizzicato.Sound('./audio/drums.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var group \= new Pizzicato.Group(\[guitar, drums\]);

group.removeSound(drums)
group.removeSound(guitar)

### addEffect()

To add an effect to a group, use the function `addEffect()`. Please note all sounds inside the group will be affected by the added effect. The function receives one parameter:

-   `effect` _(Pz.Effect, mandatory)_: The effect to be added to the group.

Example:

var bass \= new Pizzicato.Sound('./audio/bass.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var delay \= new Pizzicato.Effects.Delay();
var group \= new Pizzicato.Group(\[guitar, drums\]);

group.addEffect(delay)

### removeEffect()

To remove an effect to a group, use the function `removeEffect()`. The function receives one parameter:

-   `effect` _(Pz.Effect, mandatory)_: The effect to be removed from the group.

Example:

var bass \= new Pizzicato.Sound('./audio/bass.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var delay \= new Pizzicato.Effects.Delay();
var group \= new Pizzicato.Group(\[guitar, drums\]);

group.addEffect(delay)

group.removeEffect(delay)

### play()

You can play all sounds of a group simultaneously using the function `play`, which takes no parameters.

Example:

var drums \= new Pizzicato.Sound('./audio/drums.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var group \= new Pizzicato.Group(\[guitar, drums\]);

group.play();

### pause()

You can pause all sounds of a group simultaneously using the function `pause`, which takes no parameters. Next time the group is played, it will continue from where it left off.

Example:

var drums \= new Pizzicato.Sound('./audio/drums.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var group \= new Pizzicato.Group(\[guitar, drums\]);

group.play();
group.pause();

### stop()

You can stop all sounds of a group simultaneously using the function `stop`, which takes no parameters. Next time the group is played, it will continue from the start of the sounds composing it.

Example:

var drums \= new Pizzicato.Sound('./audio/drums.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var group \= new Pizzicato.Group(\[guitar, drums\]);

group.play();
group.stop();

### volume

Use the group's `volume` property to modify the volume of all the group.

-   `volume` _(min: 0, max: 1, defaults to 1)_: The sound's volume

Example:

var drums \= new Pizzicato.Sound('./audio/drums.mp3');
var guitar \= new Pizzicato.Sound('./audio/guitar.mp3');
var group \= new Pizzicato.Group(\[guitar, drums\]);

group.volume \= 0.5;

Effects
-------

Once a sound is created you can add effects to it by using the `addEffect` function. To remove an effect, you can use the `removeEffect` function.

var delay \= new Pizzicato.Effects.Delay();
sound.addEffect(delay);
sound.removeEffect(delay);

### Delay (example)

The delay effect plays back the sound a certain number of times in defined intervals, giving the impression of an echo. The following options are available when creating a delay effect:

-   `feedback` _(min: 0, max: 1, defaults to 0.5)_: The intensity with which the input will echo back. A larger value will result in more echo repetitions.
-   `time` _(min: 0, max: 1, defaults to 0.3)_: Interval time in seconds.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output (the delayed sound).

Example:

var delay \= new Pizzicato.Effects.Delay({
    feedback: 0.8,
    time: 0.22,
    mix: 0.75
});
sound.addEffect(delay);
sound.play();

### Ping Pong Delay (example)

The ping pong delay effect is similar to a regular Delay effect, however on each feedback loop the output is swapped between left and right channels. The following options are available when creating a delay effect:

-   `feedback` _(min: 0, max: 1, defaults to 0.5)_: The intensity with which the input will echo back. A larger value will result in more echo repetitions.
-   `time` _(min: 0, max: 1, defaults to 0.3)_: Interval time in seconds.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output (the delayed sound).

Example:

var pingPongDelay \= new Pizzicato.Effects.PingPongDelay({
    feedback: 0.3,
    time: 0.2,
    mix: 0.68
});
sound.addEffect(pingPongDelay);
sound.play();

### Dub Delay (example)

The dub delay effect is similar to a regular Delay effect, however on each feedback loop the output is routed through a biquad filter.

This effect is based on Chris Lowis' article Creating dub delay effects with the Web Audio API.

The following options are available when creating a delay effect:

-   `feedback` _(min: 0, max: 1, defaults to 0.5)_: The intensity with which the input will echo back. A larger value will result in more echo repetitions.
-   `time` _(min: 0, max: 1, defaults to 0.3)_: Interval time in seconds.
-   `cutoff` _(min: 0, max: 4000, defaults to 700)_: Frequency value applied to each successive loop. The lower the value, the more different each repetition will be perceived.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output (the delayed sound).

Example:

var dubDelay \= new Pizzicato.Effects.DubDelay({
    feedback: 0.6,
    time: 0.7,
    mix: 0.5,
    cutoff: 700
});
sound.addEffect(dubDelay);
sound.play();

### Distortion (example)

The distortion effect adds a basic "override" to the sound. The distortion effect only takes one parameter:

-   `gain` _(min: 0, max: 1, defaults to 0.5)_: Amount of distortion applied.

Example:

var distortion \= new Pizzicato.Effects.Distortion({
    gain: 0.4
});
sound.addEffect(delay);
sound.play();

### Quadrafuzz (example)

The quadrafuzz effect divides the sound into separate bands and then distorts each band independently, allowing you to control which frequencies you distort and how much.

The quadrafuzz code in Pizzicato is based on Michel Buffa's implementation of the quadrafuzz effect.

The effect takes the following parameters:

-   `lowGain` _(min: 0, max: 1, defaults to 0.6)_:
-   `midLowGain` _(min: 0, max: 1, defaults to 0.8)_:
-   `midHighGain` _(min: 0, max: 1, defaults to 0.5)_:
-   `highGain` _(min: 0, max: 1, defaults to 0.6)_:

Example:

var quadrafuzz \= new Pizzicato.Effects.Quadrafuzz({
    lowGain: 0.6,
    midLowGain: 0.8,
    midHighGain: 0.5,
    highGain: 0.6,
});

sound.addEffect(quadrafuzz);
sound.play();

### Flanger (example)

The flanger produces a swirling effect by delaying a "copy" of the sound by a small, gradually changing period. The flanger effect takes the following parameters:

-   `time` _(min: 0, max: 1, defaults to 0.45)_: Changes the small delay time applied to the copied signal.
-   `speed` _(min: 0, max: 1, defaults to 0.2)_: Changes the speed at which the flanging occurs.
-   `depth` _(min: 0, max: 1, defaults to 0.1)_: Changes the depth/intensity of the swirling effect.
-   `feedback` _(min: 0, max: 1, defaults to 0.1)_: Changes the volume of the delayed sound.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output.

Example:

var flanger \= new Pizzicato.Effects.Flanger({
    time: 0.45,
    speed: 0.2,
    depth: 0.1,
    feedback: 0.1,
    mix: 0.5
});

sound.addEffect(flanger);
sound.play();

### Compressor (example)

A compressor allows reducing the range between the loudest and the quietest parts of a sound. This is done by boosting the quiet segments and attenuating the loud ones.

The following options are available when creating a compressor effect:

-   `threshold` _(min: -100, max: 0, defaults to -24)_: The decibel value above which the compression will start taking effect.
-   `knee` _(min: 0, max: 40, defaults to 30)_: A value representing the range above the threshold where the curve smoothly transitions to the "ratio" portion.
-   `attack` _(min: 0, max: 1, defaults to 0.003)_: How soon the compressor starts to compress the dynamics after the threshold is exceeded. Short values will result in a fast response to sudden, loud sounds, but will make the changes in volume more obvious to listeners.
-   `release` _(min: 0, max: 1, defaults to 0.025)_: How soon the compressor starts to release the volume level back to normal after the level drops below the threshold.
-   `ratio` _(min: 1, max: 20, defaults to 12)_: The amount of compression applied to the audio once it passes the threshold level. The higher the Ratio the more the loud parts of the audio will be compressed.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output.

Example:

var compressor \= new Pizzicato.Effects.Compressor({
    threshold: \-20,
    knee: 22,
    attack: 0.05,
    release: 0.05,
    ratio: 18
});
sound.addEffect(compressor);
sound.play();

### Low-pass filter (example)

A low-pass filter passes signals with a frequency lower than a pre-determined cutoff frequency and attenuates signals with frequencies higher than the cutoff frequency.

-   `frequency` _(min: 10, max: 22050, defaults to 350)_: The cutoff frequency of the low-pass filter.
-   `peak` _(min: 0.0001, max: 1000, defaults to 1)_: Indicates how peaked the frequency is around the cutoff frequency. The greater the value is, the greater is the peak.

Example:

var lowPassFilter \= new Pizzicato.Effects.LowPassFilter({
    frequency: 400,
    peak: 10
});

sound.addEffect(lowPassFilter);
sound.play();

### High-pass filter (example)

A high-pass filter is the opposite of a low-pass filter (described above). It attenuates signals with a frequency lower than a pre-determined cutoff frequency and passes signals with frequencies higher than the cutoff frequency.

-   `frequency` _(min: 10, max: 22050, defaults to 350)_: The cutoff frequency of the high-pass filter.
-   `peak` _(min: 0.0001, max: 1000, defaults to 1)_: Indicates how peaked the frequency is around the cutoff frequency. The greater the value is, the greater is the peak.

Example:

var highPassFilter \= new Pizzicato.Effects.HighPassFilter({
    frequency: 120,
    peak: 10
});

sound.addEffect(highPassFilter);
sound.play();

### Stereo panner (example)

The stereo panner is used to adjust the level of a sound through the left and right speakers. A `-1` value will channel all the sound through the left speaker, whereas a `1` value will do so through the right speaker.

-   `pan` _(min: -1, max: 1, defaults to 0)_: Pan value between -1 (full left pan) and 1 (full right pan).

Example:

var stereoPanner \= new Pizzicato.Effects.StereoPanner({
    pan: 0.5
});

sound.addEffect(stereoPanner);
sound.play();

### Convolver (example)

The convolver effect allows the sound to be heard with a certain ressonance or repercussion. This can be useful to simulate certain environments such as auditoriums, concert halls, or small rooms.

In order to get this acoustic environment, an external audio file must be used as a sound sample. This audio file must contain the desired ambience that will shape the convolution. Due to this file, this effect is asynchronous, so a callback can be provided and will be executed once the effect is ready to be used.

The reverb is similar but allows programatic adjustments instead of requiring an external impulse file.

_options object_

-   `impulse` _(Mandatory; string)_: Path to your impulse file.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output.

_callback_

-   `callback` _(function)_: function executed when the impulse file has been correctly loaded and the effect is ready to be used.

Example:

var convolver \= new Pizzicato.Effects.Convolver({
    impulse: './path/to/your/impulse.wav',
    mix: 0.5
}, function() {
    console.log('Convolver ready to be used.');
});

sound.addEffect(convolver);
sound.play();

### Reverb (example)

The reverb effect is similar to the convolver effect in that it allows the sound to be heard with a certain ressonance or repercussion. This simulates a particular physical environment in which the sound could be played (e.g., an auditorium, a concert hall, etc).

Unlike the convolver effect, the reverb can be adjusted programatically without the need for any external elements.

-   `time` _(min: 0.0001, max: 10, defaults to 0.01)_: Duration of impulse, in seconds.
-   `decay` _(min: 0, max: 10, defaults to 0.01)_: The rate for the reflections of sound to fade away.
-   `reverse` _(boolean)_: Whether or not to reverse the impulse shape.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output.

Example:

var reverb \= new Pizzicato.Effects.Reverb({
    time: 1,
    decay: 0.8,
    reverse: true,
    mix: 0.5
});

sound.addEffect(reverb);
sound.play();

### Ring Modulator (example)

The ring modulator effect combines two input signals, where one of the inputs is a sine wave modulating the other.

This article from the BBC - from where this effect was based from - goes into deeper detail and explains how to recreate it. The 'ring' in this effect derives from the layout of diode nodes in the original analogue equipment, and also refers to the sound being increasingly modulated as it travels through the ring of diodes.

-   `distortion` _(min: 0.2, max: 50, defaults to 1)_: Level of distortion applied to the diode nodes.
-   `speed` _(min: 0, max: 2000, defaults to 30)_: The frequency of the modulating signal.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output.

Example:

var ringModulator \= new Pizzicato.Effects.RingModulator({
    speed: 10,
    distortion: 4,
    mix: 0.5
});

sound.addEffect(ringModulator);
sound.play();

### Tremolo (example)

The tremolo effect changes the volume of the sound over time. The outcome would be similar as if you turned the volume node up and down periodically.

-   `speed` _(min: 0, max: 20, defaults to 4)_: The speed at which the volume will change.
-   `depth` _(min: 0, max: 1, defaults to 1)_: The intensity of the volume change.
-   `mix` _(min: 0, max: 1, defaults to 0.5)_: Volume balance between the original audio and the effected output.

Example:

var tremolo \= new Pizzicato.Effects.Tremolo({
    speed: 5,
    depth: 1,
    mix: 0.5
});

sound.addEffect(tremolo);
sound.play();

### Connecting effects to and from AudioNodes

It is possible to connect AudioNodes to effects (and viceversa) by using the `connect` method. More details in the advanced section of this file.

Advanced
--------

### Accessing the audio context

If needed, the audio context used by Pizzicato is always accessible:

var context \= Pizzicato.context;

### Using Pizzicato objects in a web audio graph

You can use effects and sounds as part of an existing web audio graph.

#### Connecting nodes to a Pizzicato.Sound object

Using the `connect` method, you can connect audio nodes to a Pizzicato.Sound object. For example:

var analyser \= Pizzicato.context.createAnalyser();
var sound \= new Pizzicato.Sound();

sound.connect(analyser);

#### Creating a detached Pizzicato.Sound object

All Pizzicato.Sound objects are connected to the context's destination by default. In the example above, the `sound` object will be connected to an analyser node and it will also remain connected to the context's destination node.

To have a Pizzicato.Sound object that is not connected to the context's destination, use the `detached` option as follows:

var analyser \= Pizzicato.context.createAnalyser();
var sound \= new Pizzicato.Sound({ 
    source: 'wave', 
    options: { 
        detached: true 
    } 
});

sound.connect(analyser);

#### Connecting nodes to effects

Pizzicato effects can also be used in a web audio graph without the need to create Pizzicato.Sound objects by using the `connect` method.

Additionally, the `connect` method in an AudioNode can receive a Pizzicato effect as a parameter.

var oscillator \= Pizzicato.context.createOscillator();
var distortion \= new Pizzicato.Effects.Distortion();
var analyser \= Pizzicato.context.createAnalyser();

oscillator.connect(distortion);
distortion.connect(analyser);

### General volume

In order to change the general volume of all Pizzicato sounds, you can directly modify the property `volume`:

Pizzicato.volume \= 0.3;

### Memory management

When creating large numbers of Pizzicato objects you may experience a tipping point after which all sounds in the site are muted. This can vary depending on your browser, operating system and computer running the code.

To release some of the load, you can call the `disconnect` function on the Pizzicato.Sound objects no longer in use. This will disconnect them from the context's destination and they will become orphaned graphs, which will be freed when necessary.

Support
-------

### Browsers

Pizzicato can only work in browsers with Web Audio support. This means:

-   Firefox 31+
-   Chrome 31+
-   Safari 7+ (input source not available in Safari)
-   Opera 30+
-   Edge 13+

### Audio formats

Pizzicato supports audio formats supported by your browser. These may vary depending on your system version and browser.
