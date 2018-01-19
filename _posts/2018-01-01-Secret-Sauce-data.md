---
title: Introducing the Secret Sauce datasets
layout: post
feature_image: "/assets/secret-sauce/Minimoog_panel.jpg"
---

The aim of the Secret Sauce project is to automatically reverse engineer studio sounds, with a focus on guitar effects and synthesizers. Ultimately, we wish to answer the question <i><q>Wow, how did they make that sound?!</q></i>.
This post presents the task and makes the datasets available for whoever would like to try.

<!-- more -->


*Note: for early results, see our follow-up post <a href="{{ site.baseurl }}{% post_url 2018-01-13-Secret-Sauce-First-Results %}">here</a>!*


## The Goal

Whether it's a <a href="https://www.youtube.com/watch?v=fWm3mm6CdIQ">light echo</a> on a rockabilly guitar, a <a href="https://www.youtube.com/watch?v=4w8pbGz7E8c">thick pad</a> on a prog rock record or a <a href="https://www.youtube.com/watch?v=meXPbvp3ldg">heavy sub</a> on a hip hop track, electronic instruments and effects have become a crucial aspect of modern music.

Yet, as many <a href="https://www.soundonsound.com/forum/viewforum.php?f=23">forums</a> and <a href="https://www.youtube.com/watch?v=atvtBE6t48M">YouTube videos</a> testify, turning ideas into sounds is a difficult craft, which takes years to master. Currently, the method of choice is trial and error, which is often slow and tedious &mdash; just ask my neighbors, who will probably never forgive me for the hours I spent trying to sound like <a href="https://www.youtube.com/watch?v=UbkqE4fpvdI">the records that I enjoy</a>. Wouldn't it be great if musicians could simply provide an example of what they want, from a record or real life, and the machines would automatically tune themselves?

The aim of the Secret Sauce project is to do just that.  We are developing statistical models to reverse-engineer guitar and synthesizer sounds: **give the model a reference sound, and it will tell you how to reproduce it**.

A major obstacle is the lack of training data. Music producers rarely give away their presets, which explains the name of our project. And even if they did, separating the sounds that interest us from the others is known to be a <a href="https://en.wikipedia.org/wiki/Source_separation">difficult task</a>. More convenient <a href="http://www.musicradar.com/news/tech/sampleradar-976-free-classic-synth-samples-225241">sample banks</a> do exist, but few, if any, are labeled.

Our approach is to generate samples from scratch. Thanks to <a href="https://en.wikipedia.org/wiki/MIDI">MIDI</a>, many music devices can communicate with computers. Therefore, it is possible to generate and record thousands of random sounds automatically, though this comes at the cost of a bit of a engineering.

We are releasing five collections of sounds created with this method. We recorded a (simulated) <a href="https://www.native-instruments.com/en/products/komplete/guitar/guitar-rig-5-player/download/">guitar with 5 effects</a>, a <a href="https://tal-software.com/products/tal-noisemaker">subtractive synth plug-in</a> and a <a href="https://www.moogmusic.com/products/phattys/sub-phatty">Moog Sub Phatty</a>. For each instrument, we provide up to 10,000 sound samples, each based on the same note, as well as the settings that we used to produce them. We hope that those datasets will inspire researchers and musicians as much they inspired us!




## Datasets

For each dataset, we chose one note (C3), one instrument and one set of parameters. To generate the sounds, we assigned random values to the parameters, sent them through MIDI and recorded the note for a bit less than a second. The code to generate the tracks and clean the data is available on <a href="https://github.com/tsellam/secret-sauce/">Github</a>, it relies heavily on <a href="https://github.com/olemb/mido">mido</a>, a great MIDI library for Python.




### Guitar Effects
![guitar-rig](/assets/secret-sauce/guitar-rig.jpg){: .blog-snippet}
The Guitar Effect dataset is based on a guitar simulator (<a href="https://www.ableton.com/en/packs/tension/">Ableton Tension</a>) routed to an amp simulator, a distortion, a delay, a chorus/flanger and a reverb. All the effects come from <a href="https://www.native-instruments.com/en/products/komplete/guitar/guitar-rig-5-player/">Guitar Rig 5 Player edition</a>, which is free.

The dataset comes in two flavors. The <a href="https://drive.google.com/open?id=1QL4HLUNds6rm3T0XlWFWy3V_5DKy-yTy">tiny version</a> contains 32 sounds which correspond to every subset of effects (5 binary variables). The <a href="https://drive.google.com/file/d/1b-0anGE1csjUBiTLR1Ji6dOv53IswOQv/view?usp=sharing">full version</a> contains 10,000 samples; we varied both the effects (5 binary variables) and their settings (14 continuous variables).

**Downloads**:
 <a href="https://drive.google.com/open?id=1QL4HLUNds6rm3T0XlWFWy3V_5DKy-yTy">**Tiny version**</a> -
 <a href="https://drive.google.com/file/d/1b-0anGE1csjUBiTLR1Ji6dOv53IswOQv">**Full version**</a>


### TAL-NoiseMaker
![noisemaker](/assets/secret-sauce/noisemaker.png){: .blog-snippet} The Noisemaker dataset is based on TAL's <a href="https://tal-software.com/products/tal-noisemaker">free plugin</a>, which emulates a substractive synthesizer with two oscillators, a sub, two LFOs and separate envelopes for the filter and the amp.

The <a href="https://drive.google.com/file/d/18Q6q9jKayFjwJ-gC84opHz1LSozHSeNi/view?usp=sharing">light version</a> contains 1,000 samples,for which we varied 1 switch and 4 knobs. The <a href="https://drive.google.com/open?id=1-QRmDChzf9MLsgOvUe4HemVqslPlH5ET">full version</a> contains 10,000 samples, we varied 3 switches and 13 knobs.

**Downloads** : <a href="https://drive.google.com/file/d/18Q6q9jKayFjwJ-gC84opHz1LSozHSeNi">**Light version**</a> - <a href="https://drive.google.com/open?id=1-QRmDChzf9MLsgOvUe4HemVqslPlH5ET">**Full version**</a>



### Moog Sub Phatty
![noisemaker](/assets/secret-sauce/moog-sub-phatty.jpg){: .blog-snippet} The dataset is based on a <a href="https://www.moogmusic.com/products/phattys/sub-phatty">Moog Sub Phatty</a>, an analog synth with two oscillators and a sub, and a very aggressive sound. In contrast to the Noisemaker dataset, we varied almost every possible parameter on the front panel, leading to extreme (and sometimes silent) sounds.

The dataset contains 10,000 samples, obtained by tweaking 24 knobs and 5 switches.

**Downloads**: <a href="https://drive.google.com/file/d/1ZIcsoY0Cr8mUcBB8UqfjMRH1_weewUA0">**Full version**</a>

### Details
We sampled the parameter values uniformly over their entire domain (0-127 or 0-16383 based on MIDI specs) and rescale them to the range 0-10.

The samples last between 840ms and 900ms, they are mono encoded in 16 bits/22,050Hz. We did not normalize the volume, but we did use a limiter to avoid saturation. For more information, see the README files in the archives.


## What's next?

For now, our objective is to go through the tasks with various machine learning techniques. We already obtained a few results, described in our <a href="{{ site.baseurl }}{% post_url 2018-01-13-Secret-Sauce-First-Results %}">follow-up blog post</a>. How close are we to a solution? The video below lets you judge by yourself. We play sounds #8000 to #8015 of the Noisemaker dataset twice. First, we use the original settings. Then, we use settings predicted by a recurrent neural net.
<iframe width="560" height="315" src="https://www.youtube.com/embed/YLJU9CkSgTs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
Close, but not quite there! More info in the <a href="{{ site.baseurl }}{% post_url 2018-01-13-Secret-Sauce-First-Results %}">post</a>.

The next step is to vary the melodic patterns. Currently, we always play the same note, which greatly simplifies the problem. But what happens when we start playing melodies and chords? I suspect that we will need bigger datasets to learn robust representations.

Finally, in the long term, we can imagine reversing the process, and <i>infer sounds</i> from the settings in the spirit of <a href="https://magenta.tensorflow.org/nsynth">Nsynth</a>, or, perhaps, learn to imitate effects as a <a href="http://ieeexplore.ieee.org/abstract/document/7780634/">style transfer</a> task.



## References
The Secret Sauce project is in the lineage of <a href="http://www.yeeking.net/matthew_yee-king_dphil_thesis_2011.pdf">Yee King's pioneering thesis</a> (2011), which showed that it was possible to program substractive and additive synthesizers with feed-forward nets and genetic algorithms to imitate sounds. We hope to reproduce those results, generalize them to other settings and try many other models. Yee King's Website is <a href="http://www.yeeking.net/">here</a>, and his code <a href="https://github.com/yeeking/dx7-programmer">here</a>.

If you know any other relevant reference, please <a href="mailto:thibault.sellam@gmail.com">reach out</a>!

### Acknowledgements
Many thanks to Léo Sellam for the synthesizer, the recording, the advise and the food. I also thank <a href="https://bonvoyageorganisation.com/">Adrien Durand</a> for his insights, <a href="https://jaan.io/">Jaan Altosaar</a> and <a href="http://eugenewu.net/">Eugene Wu</a> for their feedback and the <a href="https://cudbg.github.io/lab/">WuLab</a> for the support.
