---
layout: post
title: Computer Vision
---

### Project Brief:
Task 1: Create a function which identifies and reads two digit ID numbers. The function should take an image or video as input and return a bounding box around the ID and display its number.

Task 2: Create a facial recognition function, the function should take an image of a group as input and return bounding boxes around any faces present, with their ID number.

### Approach: 

The dataset for this project was collected from photos taken of students from our class. Each volunteer had a number of apple live photos taken of them holding a unique ID number. The task was to use these images to train the classifiers which would be used in the functions. As I do not have permission from my peers to include their photos in this blog post, I have hidden everyone's faces with smiley face emojis, except my own! :)

#### Creating the dataset

<center><img src="https://artificiallyintelligent.ml/images/1.png" width="250"></center>

Each of these 'mugshot' photos taken were done with apple live photo which takes a short ~3 second video around the photo so you can play it like a gif. The benefit of this was that I was able to generate lots of training data from the frames of these short videos. I took every 14th frame of each video which gave me about 20 images per photo. With around 5-6 live photos per person, this gave me ~100 photos per person (before augmentation) to train on which is plenty for the scope of this task. Once I had the dataset, I set some aside for validation. The testing images had already been set aside by our prof and we didn't have access to them.
