# Understand Audio Data with Computer Vision Background


Side by side comparison of audio and visual data for quick understanding.

---

<!--more-->

One aspect that will catch developers’ attention quickest when exploring Github repositories is an informative and succinct readme, often complemented by informative visuals aids.

Visuals aids are great in relaying any content most straightforwardly. When used properly, it allows faster try-out, adoption of the scripts with out-of-the-box guidelines. Here are some examples of how it can be used.

## 1 Introduction

- [Illustration of concept](https://github.com/codenamewei/pydata-science-playground/blob/main/notebooks/markdown/readme.md)

{{< image src="concept.png" caption="Photo by the author" >}}

- [Display of workflow](https://github.com/codenamewei/pydata-science-playground/blob/main/notebooks/markdown/markdown_guidelines.ipynb)

{{< image src="workflow.png" caption="Photo by the author" >}}

## 2 Takeaway

This post focus on how to display images effectively in a markdown file.

## 3 Contents

- 3.1 Method to display the image
- 3.2 Tradeoffs in where to host the image
- 3.3 The engaging element -- Gif
- 3.4 Does it work with video?

---

### 3.1 Method to display the image

The preferred method to display an image is as shown below.

```
<div align="center">
  <img alt="text" src="url" width="500" height="500"><br>
  <sup>This it the caption of the image<sup>
</div>
```

If you are familiar with HTML, you will realize that the snippet of code is in HTML format.

There are 5 parameters to tinker with:

- **align**: Alignment of the image to left, center, or right
- **src**: Relative path or URL pointing to the image
- **alt**: Text for the image area, shown when the image is not found
- **width**: Width of the image in pixels
- **height**: Height of the image in pixels

_Note: Each of these parameters has to be wrapped in a double quote._

**Example:**

{{< gist codenamewei f23367e863299322f453f2558d781259 >}}

In particular, the resizing of image works best by just defining one of the image size (width/height). The other side will be adjusted adaptively along with the changes, maintaining the aspect ratio of the image. This allows the image to be easily presented in a new resolution with no distortions.

{{< gist codenamewei bbca7b451ff32aa65d5cc9fbc8c270aa >}}

Alternatively, the simplest format to insert an image into a markdown file is as shown below

`![text](relative path / url to the image)`

While it works perfectly fine, it does not allow granular controls such as changing the orientation or adjusting the size of the image.

**Example:**

{{< gist codenamewei 562989d36484624b3688ef3c16d54a63 >}}

In practice, both formats are used interchangeably where the latter comes as a quick fix.

### 3.2 Tradeoffs in where to host the image

An immediate next question when comes to append an image in a markdown file will be where to host the image.

There are two options:

- Upload the image to cloud storage and expose it as a public URL
- Add the image into a sub-location in the repository

{{< image src="hostimage.png" caption="Photo by the author" >}}

Both options come with tradeoffs, where the downsides are mentioned below.

{{< image src="tradeoff.png" caption="Photo by the author" >}}

With images placed in the same repository, it’s important to get the relative path right. The relative path pointing towards the image should always be initiated from the markdown file referring to it.

**Examples are shown as below:**

{{< image src="hostimage2.png" caption="Photo by the author" >}}

### 3.3 The engaging element -- Gif

Gif image can be displayed in the mentioned format too. Animated Gif is useful in illustrating steps or procedures.

With consideration of internet bandwidths and the size of the gifs to be embedded, moderate use of Gifs will boost the engagement of the readers.

{{< gist codenamewei 33d14ec0223d5ebff3e2c85361685dc8 >}}

### 3.4 Does it work with video?

On rare occasions, some might have the intention to include video in a markdown file.

An effective way of doing this is to have a good image representation while embedding the video URL.

**Option 1**

```
<div align="center">
    <a href="video_url"><img src="image_url"></a>
</div>
```

**Option 2**

`[![Watch the video](image_url)](video_url)`

{{< gist codenamewei 5de2690015ff5aa211ce3cabdedf2953 >}}

Thanks for reading. Till next time!

