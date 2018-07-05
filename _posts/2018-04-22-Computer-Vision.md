---
layout: post
title: Computer Vision
---

### Project Brief:
Task 1: Create a function which identifies and reads two digit ID numbers. The function should take an image or video as input and return a bounding box around the ID and display its number.

Task 2: Create a facial recognition function, the function should take an image of a group as input and return bounding boxes around any faces present, with their ID number.

### Approach: 
#### Choice of language
As always, there is a choice of which language to tackle this project in. I opted for MATLAB, despite the rarity of its use in commercial settings, because it was built for linear algebra (MATLAB stands for Matrix Laboratory) and computer vision is almost entirely linear algebra when it comes down to it.

#### The dataset
The dataset for this project was collected from taking photos of students from our class, each holding a unique ID number. A sample photo is shown below. 

<center><img src="https://artificiallyintelligent.ml/images/1.png" width="250"></center>

_Note: as I don't have permission from my peers to include their photos in this blog post, I've hidden everyone's face (except my own) with a smiley emoji :)_

Holding up ID numbers like this, it looked as though we'd all been arrested (aside from the smiley face), and were having our photo taken as we were being checked into prison, so we affectionally called these photos the 'mugshots.' Each of the mugshots were taken using apple live photo which takes a short ~3 second video around the photo so you can play it like a gif. The benefit of this was that I was able to generate lots of training image data from the individual frames of the videos. I took every 14th frame of each video which gave me about 20 images per photo. With around 5-6 live photos per person, this gave me ~100 photos per person (before augmentation) to train on which is plenty for the scope of this task. Once I had the dataset, I set some aside for validation. The testing images had already been set aside by our prof and we didn't have access to them.

#### Task 1
Let's look at the optical character recognition (OCR) task of identifying the 2 digit numbers first. 

The first step is one of image segmentation. That is, finding a way of automatically detecting the region in which the ID number is located for each image. But how? Well, what can we see?

Each person is holding a white piece of paper with a black 2 digit number printed on it. The white paper is held in front of a black object so it stands out from the rest of the image. Each person is holding the ID number in roughly the same position. Does this give you any ideas?

There are a number of ways to approach this. One approach is to run an edge detector on the image and filter out the weaker edges. Edge detection can be very simple in CV, you can run a linear filter over your image (eg. \[-1 0 1]) and where the values are above a certain user-defined threshold, the corresponding pixels form edges. The idea behind this is that edges in images form the boundary where adjacent pixels have different intensities, the greater the difference the stronger the edge. As humans, we see that a white to black edge is more salient than a white to grey edge and this is reflected in these linear filters. Extending this idea of changing pixel intensities, another method of edge detection is to take the derivative of pixel intensities in the horizontal and vertical directions and combining them to create an edge map but I won't go any further into that here. 

I played around with the edge detection method, changing the threshold, on a small subset of images to see if I could sucessfully filter for those edges binding ID. I found that whenever I changed the threshold so the right region was captured in one image, it would throw another image's region out of sync. I tried the same process with corner detection, hoping that the 

