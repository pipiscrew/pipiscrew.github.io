---
title: SpeechSynthesizer Class
author: PipisCrew
date: 2017-03-18
categories: [.net]
toc: true
---

```js
//download more voices
//https://www.microsoft.com/en-us/download/details.aspx?id=27224

// Initialize a new instance of the SpeechSynthesizer.
SpeechSynthesizer synth = new SpeechSynthesizer();

// Configure the audio output. 
synth.SetOutputToDefaultAudioDevice();

// Speak a string.
synth.Speak("This example demonstrates a basic use of Speech Synthesizer");

// Which voices are installed
foreach (var voice in synth.GetInstalledVoices())
{
	Console.WriteLine(voice.VoiceInfo.Description);
}
```

ref - https://msdn.microsoft.com/en-us/library/system.speech.synthesis.speechsynthesizer(v=vs.100).aspx

origin - http://www.pipiscrew.com/?p=7232 speechsynthesizer-class