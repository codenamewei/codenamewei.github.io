# Youtube to Text with Speech Recognition in Python


Python-based libraries to download Youtube videos for NLP use cases

---

<!--more-->

## 1 Introduction

In the effort to build a conversational speech-to-text NLP model, I started to dive in on the methods to retrieve audio data from Youtube platform. The goal is to have data pairing between the audio and text snippet as the input data source.

{{< image src="audio0.png" caption="Photo by the author" >}}

There are two libraries to retrieve sets of audio and text data from the Youtube platform.

- [you-get](https://github.com/soimort/you-get) library

- [youtube2text](https://github.com/codenamewei/youtube2text) library

## 2 You-get Library

A straightforward method is by using the [you-get](https://github.com/soimort/you-get) library. The python-based library can be easily installed with pip.

`pip install you-get`

The python-based library use terminal commands for the operations. The audio file can be retrieved in various outputs (.mp4, .webm) while the texts are presented in the SubRip subtitle output file (.srt).

Using the library after installation is straightforward. Get information on which sources to download with the following command in a terminal.

`you-get -i https://www.youtube.com/watch?v=2M_kCCcNDts`

{{< image src="youget1.jpeg" caption="Photo by the author" >}}

Proceed to download with the command below. Change the itag value to a selected tag with the preferred output type (.mp4, .webm).

`you-get --itag=137 https://www.youtube.com/watch?v=2M_kCCcNDts`

Alternatively, running the command without specifying the tag value will download the default in the list.

`you-get https://www.youtube.com/watch?v=2M_kCCcNDts`

The subtitle file is in the following manner.

{{< image src="youget2.jpg" caption="Photo by the author">}}

Notice how the texts are all lowercase and do not separate with the end of sentence punctuation. Due to that, sequential steps of post-processing work have to be performed to get working pairs of audio and text.

## 3 Youtube2text Library

Youtube2text library is designed to get a suitable format for the audio<>text pairing. The library supports three functionalities at the time of writing.

- Retrieve Youtube URL as audio and text output
- Download Youtube audio in an audio file format (.wav, .flac)
- Extract the audio file to text output

Install the library by pip with the following command.

`pip install youtube2text`

To retrieve a youtube URL as audio and text output, run the following command in a python environment.

```
from youtube2text import Youtube2Text

converter = Youtube2Text()

converter.url2text("https://www.youtube.com/watch?v=Ad9Q8rM0Am0&t=114s")
```

The library currently supports audio in wav or flac format and text in csv format, where the output is stored in the sub-folders of the designated path or default path `<HOMEPATH>\youtube2text`.

{{< image src="filedirectory.png" caption="Photo by the author">}}

The layout of the directories is listed below. _Audio_ folder contains the audio file as a whole, while _audio-chunks_ folder stores snippets of audio file matching to the metadata in the text file. Csv file in the text folder is the output of the translation from audio to text.

```
<Own Path> or <HOME_DIRECTORY>/youtube2text
│
├── audio/
│   └── 2022Jan02_011802.wav
|
├── audio-chunks/
│   └── 2022Jan02_011802
│       ├── chunk1.wav
│       ├── chunk2.wav
│       └── chunk3.wav
│
└── text/
    └── 2022Jan02_011802.csv
```

The goal of mine is to prepare audio and translated text to train a custom Automatic Speech Recognition (ASR) model. Any attempts in using large language pretrained model would require the newly added audio data to be sampled in a desired frequency (example: 16 kHz). The selected sampling rate should match to the ones where the existing NLP model has been trained with. With that context, it’s important for the audio data retrieving process to allows the toggling of the sample rate. Youtube2text is designed to factor [the toggling of audio sample rate](https://github.com/codenamewei/youtube2text/blob/main/src/youtube2text/youtube2text.py#L111).

```
converter.url2audio(urlpath = "https://www.youtube.com/watch?v=rFYcvrKkr90", audiosamplingrate = 22000)
```

Let’s take a glimpse into the text file. The text file contains 2 columns: text and wav. Metadata of audio chunk mapping to a text sentence is provided side by side.

{{< image src="excel.jpeg" caption="Photo by the author">}}

Text file outputs are arranged in a manner to allow the correction of any sentence if needed.

Since the audio is translated to text with existing speech recognition model, the text generated is highly dependent on the quality of the audio output. It might not be all the times where audio is articulated in a precise manner. To put things into context, imagine that a Ted talk with speaker who articulates with zero background noise would be interpretable than webinars hosting more than one person with background music.

With a few attempts, it is obvious that the text requires manual inspection and correction to produce high quality translated text data. Do expect to spend time and effort in this process to get high quality translated text.

While it might be tedious at times, this helps to ensure a good raw source of data is prepared for subsequent NLP model training.The replaying of audio chunk alongside the text column makes it easier to find the correspond part pairing to the audio output.

The column stating the file is important for the task such as ASR use case. In the latter step to train the model, the data preparation step reads in audio file from the specific audio path and preprocess the vector embeddings. Otherwise, if the metadata of wav information is not needed, the column stating the file can be eliminated easily by deleting the column in a single step.

{{< image src="excel2.jpeg" caption="Photo by the author">}}

Check out the [python notebook](https://github.com/codenamewei/youtube2text/blob/main/tests/howtouse.ipynb) for more examples of using the youtube2text library.

Thanks for reading.

## 4 Resources

- https://github.com/soimort/you-get
- https://github.com/codenamewei/youtube2text

