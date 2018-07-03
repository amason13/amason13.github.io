---
layout: post
title: Neural Computing
---

### Project Brief:
Working as a pair, implement 2 different Neural Network models to the task and dataset of your choice, compare and contrast and provide a (no more than 6 page) report of your findings. 

### Approach:
We decided to compare a Multi-Layer Perceptron (MLP) to a Convolutional Neural Network (CNN) to classify handwritten digits on a subset of the famous MNIST dataset. It is worth noting that we knew which model would be more accurate, CNNs go hand in hand with image classification tasks. They were biologically inspired by the way the different regions of the brain process images at different levels of abstraction for visual pattern recognition. Our task was not to cover new ground, but to gain experience implementing these models for ourselves and show our understanding of them. 

In our implementation of the MLP, we had an input layer, 2 hidden layers and an output layer. The input layer had 784 neurons - one for each pixel in the image - and the output layer had 10 neurons - one for each of the digits 0-9. As for the number of neurons in each hidden layer, that was one of the hyper-parameters we searched for in our grid search. 

The reason behind this is that increasing the number of layers or neurons in a Neural Network (NN) adds more complexity to the model. Data with simpler distributions might be accurately modeled by a NN with fewer neurons, however, in other cases, you might need to add more layers or neurons to model certain complexities in the data. So you might ask, why not just cram the NN full of layers, each with lots of neurons and surely you will be able to model whatever distribution is in your data? Well, this might be true, but the more complex you make your model, the less likely it is to generalise to previously unseen data. If your NN is too complex for the task at hand, you are in danger of the model just learning the exact data in the training set, not the reasons behind what makes an 8 an 8. (This is known as overfitting!)

The other hyper-parameters we searched for in our grid search were the learning rate, and the backpropogation momentum term to mitigate the risk of getting trapped in a local minimum when updating our weights. I won't go into the details of backpropogation here. If anyone is reading this as a learning tool, I'd highly recommend the [Deep Lizard](https://www.youtube.com/channel/UC4UJ26WkceqONNF5S26OiVw) video series on back propogation as that really cleared things up for me. 

In our implementation of the CNN, we structured the network as follows. Input layer, 5x5 convolution, ReLU, max pooling, 3x3 convolution, ReLU, max pooling, fully connected, ReLU, fully connected output layer. We performed a grid search over 3 hyper-parameters: learning rate, term of momentum and number of filters in the convolutional layers. If time and computational cost were no issue, we could have performed a much higher definition grid search in each of our models, but this was not necessary for the task at hand as it was the process we were being graded on rather than the results. 

It is no surprise that the CNN outperformed the MLP by some margin. The full report is available [here](artificiallyintelligent.ml/pdfs/Neural_Computing_Coursework.pdf) (beautifully co-written by the legendary data scientist F Miles.)
