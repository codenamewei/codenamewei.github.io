---
weight: 1
title: "Part 1: Displaying Image in Jupyter Notebook"
date: 2023-10-21
lastmod: 2023-10-21
draft: false
author: "Chiawei Lim"
authorLink: "https://www.linkedin.com/in/codenamewei/"
description: "Part 1: Displaying Image in Jupyter Notebook"
images: []
resources:
  - name: "featured-image"
    src: "featured-image.jpg"

tags: ["markdown", "python", "jupyter"]
categories: ["jupyter"]

lightgallery: true

toc:
  auto: false
---


There are times when data science practitioners and their target audiences need to check images while working on code in Jupyter files. This article lays out various ways to present images in Jupyter Notebooks cells, as well as the tradeoffs between each method.



### Displaying Image using Markdown Syntax

The most straightforward method is switching a Jupyter cell into Markdown format, and passing in image.

**Method 1: Display the image with Markdown Syntax**

```
![alt text](image_path)
```

The format is straightforwards with 3 parts:

1. **Exclamation mark !**
2. **Square bracket []** with alternate texts to be presented if the image is not found
3. **Parentheses ()** with the desired image to be displayed

The image path can either be

- an image URL
- a local image path (absolute/relative)

Below are examples of each variant.

**Image URL**
```
![Sample Image](https://i.pinimg.com/564x/88/67/a4/8867a454935fa63595614875e48a6b53--samoyed-funny-samoyed-dogs.jpg)
```

**Local Relative Path**
```
![Sample Image](metadata/samoyed.jpg) 
```

**Local Absolute Path**
```
![Sample Image](mypath/to/metadata/samoyed.jpg)
```
<sup>_[Check out the code in Jupyter Notebook](https://github.com/codenamewei/technical-posts/blob/main/jupyter/post1_displaying-image-in-jupyter-notebook/show_image.ipynb)_</sup>


**Tradeoffs:**  
Pros:
- Straightforward
- Simple syntax, easy to remember

Cons: 
- Not able to make any changes, such as adjusting the side

The perk of this approach is that it is really simple. 

Do it a few times, and you will remember it at the back of your mind. The downside, however, is the lack of knobs to adjust the size of the image. This is often necessary when it comes to working with images from multiple sources.

**Method 2: Display the image with HTML Syntax**

If you are familiar with the frontend stack, HTML should be no stranger to you.

```
<img src="image_path" width="width_length" height="height_length" alt="alt text">
```

The _src_ parameter is necessary while the rest are optional.

```
<img src="image_path">
```

Like the previous method, the image_path can be from different sources as illustrated below:

**Image URL**
```
<img src="https://i.pinimg.com/564x/88/67/a4/8867a454935fa63595614875e48a6b53--samoyed-funny-samoyed-dogs.jpg">
```

**Local Relative Path**
```
<img src="metadata/samoyed.jpg">
```

**Local Absolute Path**
```
<img src="mypath/to/metadata/samoyed.jpg">
```
<sup>_[Check out the code in Jupyter Notebook](https://github.com/codenamewei/technical-posts/blob/main/jupyter/post1_displaying-image-in-jupyter-notebook/show_image.ipynb)_</sup>

When it comes to adjusting the size of the image, changing either one (width/height) keeps the aspect ratio of the image. 

This has been useful instead of trying for a few runs (between the combination of different widths and heights) to check on the outcome of the image.

```
<img src="metadata/samoyed.jpg" width="250">
```
<sup>_[Check out the code in Jupyter Notebook](https://github.com/codenamewei/technical-posts/blob/main/jupyter/post1_displaying-image-in-jupyter-notebook/show_image.ipynb)_</sup>


**Tradeoffs:**  
Pros:
- Able to adjust the size (width, height, or both)

Cons: 
- Small adoption curves if users are not familiar with HTML syntax

### Displaying Image using Python Syntax


**Import the necessary libraries**

To display images using Python, install the libraries with **requirements.txt**

```
pip install -r requirements.txt
```

The dependencies are laid out below.

```
numpy==1.25.0
imread-from-url==0.1.3
opencv-python==4.8.0.74
matplotlib==3.7.2
ipympl==0.9.3
```

Likewise, the image source can be either of the options below.

**Image URL**
```
Image(url = image_url, width=value, height=value)
```

**Local Relative/Absolute Path**
```
Image(filename = "path/to/image", width=value, height=value)
```

Adjusting of image can be performed with the parameter width and height.  

Examples are shown below.

**Image URL**
```
Image(url="https://i.pinimg.com/564x/88/67/a4/8867a454935fa63595614875e48a6b53--samoyed-funny-samoyed-dogs.jpg")
```

**Adjust the Size**
```
Image(filename="metadata/samoyed.jpg", width="250") # use either one to keep the aspect ratio
```
<sup>_[Check out the code in Jupyter Notebook](https://github.com/codenamewei/technical-posts/blob/main/jupyter/post1_displaying-image-in-jupyter-notebook/show_image.ipynb)_</sup>

**Tradeoffs:**  
Pros:
- Works seamlessly during the development stage, especially if Python is preferred.

Cons: 
- Small adoption curves for first-time users.

**For more sophisticated tasks such as drawing rectangle on image**

Check out the code below:


```
%matplotlib inline
%matplotlib widget

import matplotlib.pyplot as plt
import matplotlib.image as mpimg
import matplotlib.patches as patches

#change R, B axis to correctly display color
outimg = img[:,:,::-1]

imgplot = plt.imshow(outimg, aspect = "auto")

# Create figure and axes
fig, ax = plt.subplots(1)
  
ax.set_axis_off()
# Display the image
ax.imshow(outimg)

rectleftup = (50, 120)
rectwidth = 260
rectheight = 220
linewidth = 2

# Create a Rectangle patch
# https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Rectangle.html
rect = patches.Rectangle(rectleftup, rectwidth, rectheight, linewidth=linewidth,
                         edgecolor='b', fill = False)
  
# Add the patch to the Axes
_ = ax.add_patch(rect)
```

<sup>_[Check out the code in Jupyter Notebook](https://github.com/codenamewei/technical-posts/blob/main/jupyter/post1_displaying-image-in-jupyter-notebook/show_image.ipynb)_</sup>


Stay tuned for the next post on **Part 2: Displaying Video in Jupyter Notebook.**

- [Github Repository](https://github.com/codenamewei/technical-posts)
- [Profile](https://github.com/codenamewei/technical-posts)

Thanks for reading.