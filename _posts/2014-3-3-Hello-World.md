---
layout: post
title: Ideas from a caffienated neural network.
---

With AI becoming the latest buzzword in the Computer Science community, it is becoming important, in all areas of computer science, to incorporate concepts from Machine Learning into our workspace. New use cases are emerging for applications of Aritificial Intelligence in biomedical industries, pedestrian detection systems, synthesizing music, etc. How do we construct a neural network that performs a new task?

__What is a neural network?__  
A neural network is the crux of any Machine Learning architecture. It works by learning a decision boundary that separates the input data into some number of classes. For example, the inputs could be a pair of binary digits and the output (learnt) could be the binary output of an OR gate (0 or 1).   
A neural network typically involves a sequence(2 or more) of layers starting from the input layer and making transitions through the hidden layers, till the final output layer. For a mathematical representation of how networks learn a decision boundary, I couldn't recommend something better than Christopher Olah's [blog post on Manifolds](http://colah.github.io/posts/2014-03-NN-Manifolds-Topology/).  

To have "learnable parameters", the weights in a neural network, is like teaching a child to slowly learn and recognize the objects and environment around it. Or, a more related mathematical anology would be to have a blind man walk down a mountain range (called the error surface) and reach the lowest point (the point of ~~no return~~ least error).  

__What is the intuition for coming up with a new neural network architecture?__  
The intuition I wanted to convey being that, neural networks store all the ***information about the input***, that we would like it to remember when its making a decision about a new input in the future. And this information is stored as weights. Weights hold the memory representative and power of a network.    
This maybe relatively straightforward when we are considering a network learning for a particular task, but how do we come up with an architecture for a new task at hand? How do we choose the number of weights and layers that are sufficient to classify points in a new dataset? 

As an example, consider a Language processing task. Suppose that we were given a sentence in German and asked to predict the correct corresponding sentence in English. How would we like your network to interpret the input sentence?  

1. Look at it as a constitutional build - Letters --> Words --> Sentences --> Paragraphs --> so on.
2. View it as a time series input of the sequence of words.  

In order to generate the correct corresponding sentence in English, we would like the network to remember not just the work and its predicted translation, but also the context in which the word appeared, in some of which cases, the translated sentence might change significantly. Hence, we need a system where the output of the previous predictions are "remembered" by the network and passed down when making successive predictions.  

This is used in the architecture for Recurrent Neural Networks (RNNs). In RNNs, the prediction at one instant of time is connected to the successive layers through weights. These weights learn the context of the word in a sentence. 
For a better understanding of RNNs and LSTMs (A form of RNNs), you can also read up Christopher Olah's [blog post on LSTMs](http://colah.github.io/posts/2015-08-Understanding-LSTMs/).

The concept can be extended to deciding architectures for other fields like Computer Vision as well.


