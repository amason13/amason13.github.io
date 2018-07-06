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
The dataset for this project was collected from taking photos of students from our class, each holding a unique ID number. 
_Note: as I don't have permission from my peers to include their photos in this blog post, I've hidden everyone's face (except my own) with a smiley emoji :)_

Each of the 'mugshots'  - I affectionally refer to them as mugshots as we look like prisoners holding our ID numbers - were taken using apple live photo which takes a short ~3 second video around the photo so you can play it like a gif. The benefit of this was that I was able to generate lots of training image data from the individual frames of the videos. I took every 14th frame of each video which gave me about 20 images per photo. With around 5-6 live photos per person, this gave me ~100 photos per person (before augmentation) to train on which is plenty for the scope of this task. Once I had the dataset, I set some aside for validation. The testing images had already been set aside by our Prof. and we didn't have access to them.

#### ID detection
Let's look at the optical character recognition (OCR) task of identifying the 2 digit IDs first. 

The way I see it, this task can be split into 3 steps. 

The first step is one of image segmentation. That is, capturing the desired regions where the ID number is situated.

The second step is using these desired regions to train a classifier to return the correct number for each image. 

The final step is bringing this all together in a function which takes an image or video as input. 


Each person is holding a white piece of paper with a black 2 digit number printed on it. The white paper is held in front of a black object so it stands out from the rest of the image. Each person is holding the ID number in roughly the same position. 

There are a number of ways to approach step 1. 

Observing that the ID numbers were printed on white paper, backed against a black object, my first thought was to apply a method of edge or corner detection on the image. Edge detection works by applying a filter over the image and pixels where the result is greater than a user-defined threshold form edges. In basic terms, corner detection seeks to identify where two edges meet. The relavence of white on black is that this should result in stronger edges/corners. A black to white edge is much more salient to the human eye than a grey to white edge, and this is captured in the mathematical formulation of edge/corner strength. I played around with the both edge and corner detection methods on a small subset of images, changing the strength threshold, in an attempt to capture the desired region. However, I found that whenever I changed the threshold so the desired region was captured in one image, it would throw another one out of sync. These 2 images show how different clothing patterns, camera angles, background objects, etc can produce vastly different results when the same algorithm is applied to 2 different images.

<center><img src="https://artificiallyintelligent.ml/images/me.png" width="250"><img src="https://artificiallyintelligent.ml/images/2.png" width="250"></center>

A possible way around this might be to restrict the search space to a central region of the image. However, in the interest of creating a more robust and generalisabile function, I decided against that at this stage. 


[transfer learning](https://www.mathworks.com/help/nnet/examples/transfer-learning-using-alexnet.html)
