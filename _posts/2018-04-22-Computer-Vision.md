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

