---
weight: 1
title: "Deepfake Audio with Wav2Lip"
date: 2022-10-10
lastmod: 2022-10-10
draft: false
author: "Chiawei Lim"
authorLink: "https://www.linkedin.com/in/codenamewei/"
description: "Step-by-step walkthrough on lip-syncing with Wav2Lip"
images: []
resources:
  - name: "featured-image"
    src: "featured-image.jpg"

tags: ["deepfake", "lipsync", "python"]
categories: ["nlp"]

lightgallery: true

toc:
  auto: false
---

### Overview of Deepfake Technology

Deepfake is a technology that creates synthesis media with a subfield of Machine Learning - Deep Learning.

{{< image src="0.jpeg" caption="Photo by the author" >}}

A common use case that the public is aware of is the application of face-swapping. A target face is swapped and merged, often seamlessly on first glance view, to create an altered event.

{{< image src="1.jpeg" caption="Photo by the author" >}}

On a high level, Deepfake can be split into 3 sub-domains based on the focus of the media to alter. The former-mentioned use case (face-swapping) falls under Deepfake vision, where the image or video streams were targeted.

{{< image src="2.jpeg" caption="Photo by the author" >}}

On the other hand, Deepfake audio clone speech from third-party sources to the person in interest. In a scenario where one only communicates through phone calls, one might not be able to tell the authenticity of the sound.

{{< image src="3.jpeg" caption="Photo by the author" >}}

To achieve the impersonation both visually and audibly, one would have to not only look like the desired target but also sound like him. An example is shown below, where a famous actor, Morgan Freeman, is portrayed with a combination of Deepfake audio and Deepfake vision.

{{< image src="youtube_0.jpg" caption="Play the Youtube video at: https://bit.ly/3yI23zN" >}}

### Deepfake Audio with Wav2Lip

#### Environment Setup

This article focuses on Deepfake Audio with the implementation from Github repository https://github.com/Rudrabha/Wav2Lip. The repository is based on the paper _A Lip Sync Expert Is All You Need for Speech to Lip Generation In the Wild_ published at ACM Multimedia 2020.

The setup requires to run the repository includes

**1. Python 3.6**

Create a new virtual python environment with your preferred methods. In this example, conda command is illustrated.

```
conda create -n wav2lip python=3.6
```

**2. Ffmpeg**

```
pip install ffmpeg-python
```

Particularly in Linux OS, the following installation method is preferred.

```
sudo apt-get install ffmpeg
```

**3. Installation of requirements.txt from the repository**

In this step, the repository is first cloned with the command below.

```
git clone https://github.com/Rudrabha/Wav2Lip
```

{{< admonition >}} Note: In the main execution step, the python script in the repository is necessary for the actual merging of audio and video streams.
Packages required, as layout in the file requirements.txt, are installed with the command below.  {{< /admonition >}}

```
pip install -r requirements.txt
```

#### Preparation of files

Largely three data source inputs are required in order to run the lip-sync with Wav2Lip.

{{< image src="4.jpeg" caption="Photo by the author" >}}

##### Model file

Two models are supported out-of-the box:

- [Wav2Lip](https://iiitaphyd-my.sharepoint.com/:u:/g/personal/radrabha_m_research_iiit_ac_in/Eb3LEzbfuKlJiR600lQWRxgBIY27JZg80f7V9jtMfbNDaQ?e=TBFBVW)
- [Wav2Lip GAN](https://iiitaphyd-my.sharepoint.com/:u:/g/personal/radrabha_m_research_iiit_ac_in/Eb3LEzbfuKlJiR600lQWRxgBIY27JZg80f7V9jtMfbNDaQ?e=TBFBVW)

While only one model is necessary for a single run, do download both for a comparison of the results.

##### Video file

For a desirable output, the input video should fulfill the following conditions.

- Person of interest centered and upfront in the video
- Person of interest with restricted body gesture and minimum head movement
- Person of interest with no occlusions arounds the face region (mask, shadows, hair)
- Preferably person of interest with still lip-movement
- Good lighting with not cluttered background
- Video with good resolution

{{< admonition tip >}}
Particularly, it has been found that the results are promising when the person of interest has no lip movement. This is because, through the algorithm, the mouth area would be altered to match the intonation of the speech. Having any movement from the source complicates the alteration and it might present unnatural results with visible glitches.  {{< /admonition >}}

##### Audio file

For a desirable output, the input audio should fulfill the following conditions.

- Clear and succinct single source of audio (Do not have more than one person conversing with overlapping speech)
- Minimum/no background noises

{{< admonition tip >}}
As the idea is to merge the audio script to the person in interest in the video, both input files should be of similar lengths in time.  {{< /admonition >}}

#### Main Running Step

With the files prepared and saved in local paths, it’s time to run the Wav2Lip using the script inference.py. The script is located in the path of `<path-to>\Wav2Lip\inference.py`.

Command should be constructed in the following manner:

```
python inference.py --checkpoint_path <path-to-model-file> --face <path-to-video-file> --audio <path-to-audio-file>
```

Example of command for better clarity:

```
python inference.py --checkpoint_path C:\Users\codenamewei\deepfake\model\wav2lip_gan.pth --face C:\Users\codenamewei\Documents\deepfake\data\video_short.mp4 --audio C:\Users\codenamewei\Documents\deepfake\data\audio_short.wav
```

The default and frequently used parameters are layouts as below.

For a full list, check out the [parameters settings from the source script.](https://github.com/Rudrabha/Wav2Lip/blob/master/inference.py#L13-L51)

```
--checkpoint_path:
Path to checkpoint file of supported model (Wav2Lip, Wav2Lip GAN)

--face:
Path to video file of supported format (mp4, avi, ...)

--audio:
Path to audio file of supported format (wav, flac, ...)

(Optional) --nosmooth:
When set, this results in no smoothing around the mouth region

(Optional) --pads:
When set, this adjust the range of the region to alter
Parameters set in this manner: (top, bottom, left, right)
Example:
--pads [0, 20, 0, 0]
The example above adds 20 pixels to the chin area

(Optional) --static:
When set to true, only the first frame will be used.
Example:
--static True
```

If you are questioning which model file to use, the readme.md in the repository points out the key properties of each model as shown in the screenshot below.

{{< image src="modelcomparison.png" caption="Photo by the author. Screenshot from Rudrabha/Wav2Lip repository." >}}

Wav2Lip better mimics the mouth movement to the utterance sound, and Wav2Lip + GAN creates better visual quality.

{{< image src="5.jpeg" caption="Photo by the author" >}}

To further understand what it means, check out the example below captured in the same time stamp. One noticeable difference seen in the screenshot below is that Wav2Lip + GAN creates a more visually appealing result, where the teeth are rendered in a natural manner.

{{< image src="6.jpeg" caption="Photo by the author" >}}

This tutorial shows the side-by-side comparison of the end results from the implementation.

{{< image src="youtube_1.jpg" caption="Play the youtube video at: https://bit.ly/3MGaCkL" >}}

### Notes (Updated on 10th October 2022)

To test the implementation of Deepfake audio, two GitHub repositories were under consideration:

- https://github.com/Rudrabha/Wav2Lip (Demonstrated in this article)
- https://github.com/Markfryazino/wav2lip-hq

A promising result is shown with the out-of-the-box model of Wav2Lip. The HD model mentioned in the repository likely will deliver higher performance results.

For Wav2Lip-hq, a noticeable distortion of colors on the result can be seen (as shown in the picture below). The same concern was raised in several issues as well. [#6](https://github.com/Markfryazino/wav2lip-hq/issues/6), [#11](https://github.com/Markfryazino/wav2lip-hq/issues/11). Due to that, it’s very unlikely to leverage the results generated from the repository.

{{< image src="7.jpeg" caption="Photo by the author" >}}

Thanks for reading!
