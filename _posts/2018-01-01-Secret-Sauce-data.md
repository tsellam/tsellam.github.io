---
title: The Secret Sauce Datasets
layout: post
feature_image: "/assets/secret-sauce/Minimoog_panel.jpg"
---

The aim of Secret Sauce is to automatically reverse engineer guitar and synth sounds, and thus answer the question <i><q>Wow, how did they make that sound?!</q></i>.
This post presents the task, the datasets, and makes them available for whoever would like to try.

<!-- more -->

## The Goal

Whether it's a <a href="https://www.youtube.com/watch?v=fWm3mm6CdIQ">light echo</a> on a rockabilly guitar, a <a href="https://www.youtube.com/watch?v=4w8pbGz7E8c">thick pad</a> on a prog rock record or a <a href="https://www.youtube.com/watch?v=meXPbvp3ldg">heavy sub</a> on a hip hop track, effects and synthesizers have become a crucial aspect of modern music. And yet, as <a href="https://www.soundonsound.com/forum/viewforum.php?f=23">Web forums</a> testify, turning ideas into sounds is a difficult craft, which takes years to master.

The aim of the Secret Sauce project is to make it easier for musicians to (re)create sounds. We are developing statistical models to reverse engineer synthesizer patches and guitar effects: give the model a reference sound, and it will tell you how to reproduce it.

To this end, we are releasing three datasets, based on three instruments: a <a href="https://www.native-instruments.com/en/products/komplete/guitar/guitar-rig-5-player/download/">guitar with 5 effects</a>, a <a href="https://tal-software.com/products/tal-noisemaker">substractive synth plug-in</a> and a <a href="https://www.moogmusic.com/products/phattys/sub-phatty">Moog Phatty</a>. For each instrument, we provide 10,000 sound samples, as well as the settings used to produce the sounds. The inference task is to guess the settings from the sounds.




## Datasets

For each dataset, we chose one note (C3), one instrument and one set of parameters. To generate the sounds, we assigned random values to the parameters, sent them through MIDI and recorded the note for a bit less than a second. The code to generate the tracks and clean the data is available on <a href="https://github.com/tsellam/secret-sauce/">Github</a>.




### Guitar Effects
![guitar-rig](/assets/secret-sauce/guitar-rig.jpg){: .blog-snippet}
The Guitar Effect dataset is based on a guitar simulator (<a href="https://www.ableton.com/en/packs/tension/">Ableton Tension</a>) routed to an amp simulator, a distortion, a delay, a chorus/flanger and a reverb. All the effects come from <a href="https://www.native-instruments.com/en/products/komplete/guitar/guitar-rig-5-player/">Guitar Rig 5 Player edition</a>, which is free.

The dataset comes in two flavors. The <a href="https://drive.google.com/open?id=1QL4HLUNds6rm3T0XlWFWy3V_5DKy-yTy">tiny version</a> contains 32 sounds which correspond to every subset of effects (5 binary variables). The <a href="https://drive.google.com/file/d/1b-0anGE1csjUBiTLR1Ji6dOv53IswOQv/view?usp=sharing">full version</a> contains 10,000 samples; we varied both the effects (5 binary variables) and their settings (14 continuous variables).


### TAL-NoiseMaker
![noisemaker](/assets/secret-sauce/noisemaker.png){: .blog-snippet} The Noisemaker dataset is based on TAL's <a href="https://tal-software.com/products/tal-noisemaker">free plugin</a>, which emulates a substractive synthesizer with two oscillators, a sub, two LFOs and separate envelopes for the filter and the amp.

The <a href="https://drive.google.com/file/d/18Q6q9jKayFjwJ-gC84opHz1LSozHSeNi/view?usp=sharing">light version</a> contains 1,000 samples,for which we varied 1 switch and 4 knobs. The <a href="https://drive.google.com/open?id=1-QRmDChzf9MLsgOvUe4HemVqslPlH5ET">full version</a> contains 10,000 samples, we varied 3 switches and 13 knobs.


### Moog Sub Phatty
![noisemaker](/assets/secret-sauce/moog-sub-phatty.jpg){: .blog-snippet} The dataset is based on a <a href="https://www.moogmusic.com/products/phattys/sub-phatty">Moog Sub Phatty</a>, an analog synth with two oscillators and a sub, and a very aggressive sound. In contrast to the Noisemaker dataset, we varied almost every possible parameter on the front panel, leading to extreme (and sometimes silent) sounds.

The dataset contains 10,000 samples, obtained by tweaking 24 knobs and 5 switches. You may obtain it <a href="https://drive.google.com/file/d/1ZIcsoY0Cr8mUcBB8UqfjMRH1_weewUA0/view?usp=sharing">here</a>.

### Details
We sampled the parameter values uniformly over their entire domain (0-127 or 0-16383 based on MIDI specs) and rescale them to the range 0-10.

The samples last between 840ms and 900ms, they are mono encoded in 16 bits/22,050Hz. We did not normalize the volume, but we did use a limiter to avoid saturation. For more information, see the README files in the archives.


## What's next?

The first objective is to go through the tasks with standard ML techniques &mdash; I will present the first results in a separate blog post in the near future.

The next step is to vary the melodic patterns. Currently, we always play the same note, which greatly simplifies the inference. But what happens when we start playing melodies and chords? I suspect that much bigger datasets will be needed to learn robust feature representations.

Finally, in the long term, we can imagine reversing the process, and <i>infer sounds</i> from the settings in the spirit of <a href="https://magenta.tensorflow.org/nsynth">Nsynth</a>, or, perhaps, learn to imitate effects as a <a href="http://ieeexplore.ieee.org/abstract/document/7780634/">style transfer</a> task.



## References
The Secret Sauce project is in the lineage of <a href="http://www.yeeking.net/matthew_yee-king_dphil_thesis_2011.pdf">Yee King's pioneering thesis</a> (2011), which showed that it was possible to program substractive and additive synthesizers with feed-forward nets and genetic algorithms to imitate sounds. We hope to reproduce those results, generalize them to other settings and try many other models. If you know of any other relevant reference, please reach out!

### Acknowledgements
Thanks to <a href="https://bonvoyageorganisation.com/">Adrien Durand</a> for the ideas, and many thanks Léo Sellam for the synthesizer, the recording, the advise and the food.
