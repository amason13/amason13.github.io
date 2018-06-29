---
layout: post
title: Machine Learning
---

### Project Brief:
In teams of 2, implement 2 different machine learning models to the task and dataset of your choice, compare and contrast and display your findings in a poster. 

### Our Approach:
I worked with my friend, [Sergio](https://github.com/sergiorozada12), on this one. It was the first project of the course and so, inexperienced and naive, we thought we would accurately predict football scorelines with this fantastic new thing we were learning about called machine learning... we were soon disabused of that notion. 
The data set we were using was a [European Football](https://www.kaggle.com/jangot/ligue1-match-statistics/version/2) dataset from kaggle, which had ~9k observations of 92 dimensional data. Our approach was a 70:20:10 split of training to validation to testing data and we choose to compare logistic regression to a random forest. 
We played around with a a few different variations of task. Starting out thinking we could use match stats to correctly predict exact scorelines, to binning all possible scorelines into a smaller set of categories, and with the necessary wrangling and pre-processing of our data for each task, we got terrible results every time. We had fast learnt that, given the data we had selected, we were biting off way more than we could chew. The accuracy of the models was unimportatnt for this project as far as the marking scheme goes, but we still needed some level of accuracy whereby we could properly compare the two methods. We finally settled on the following task, a binary classification of whether or not the home team would win the match, given the half time stats. 
In the end, after filtering the data to be fit for purpose, removing linearly dependent features, using half time stats only, and generating more relevent features out of existing ones, we had ~8k observations of 37 dimensional data (36 features and one target). We applied our two models and found the accuracy to in the region of 75%, good enough to complete the task. 
We found that the most indicative half time stats were possesion, dribble success, and _...wait for it..._ half time goal difference. How's that for a crazy bit of insight! The team with the most goals at half time has a better chance of winning the match at full time. Three cheers for machine learning!
But seriously, this project was a good introduction to machine learning and some of its challenges - wrangling, pre-processing, data quality, the curse of dimensionality etc. I enjoyed my first delve into ML, and for anyone interested, the final poster is available [here](amason13.github.io/images/ML CW (1).pdf).
