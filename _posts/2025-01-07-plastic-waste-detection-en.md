---
layout: post
title: Not every published model is a valid benchmark
lang: en
permalink: 2025/01/07/plastic-waste-detection
published: false
---

Training a model with deep leaning techniques could be very complex if you don't know how to set up properly hyperparameters. 
To avoid headaches you can tune them and find the subset of values that will optimize the performances of your model.
Or if you are short on time you could do a little research and look if somebody already did the tuning part.
You can register the hyperparameters configuration and also take others results as benchmark for your model.
The purpouse of doing that is to get a starting point for your tuning and a benchmark to improve if possible.
This is in the end what I wanted to do in one of the last projects that I did at university.

### My assignment

My assignment was to train a model that is able to detect plastic waste in water surfaces like rivers and lakes. 
I worked with a friend of mine and both decided to use the YOLOv8 architecture and train it with a dataset that was available during our work.
We did some experiment without any particular result in performance so we have looked around searching for academic papers or some 
post on the internet that was somehow relevant.
We have bumped mostly in detection with dataset containing satellite images except one study published in early 2024 that
was related with the same our dataset and model, lucky us.
So reading the paper, we found out that we could reach good performance with a specific configuration. Nice!

Let's try if we can replicate those results and... nope, still bad output with high evaluation loss.
Maybe we did the training execution with some hyperparameter or other details different. Let's try again but with 
the very same values as hyperparameters. Nothing, performances don't want to improve.

### WTF?!

It seems reasonable to look for bugs or misconfigurations by our fault (after all I'm still a master student) but when no solution
is able to give better results some doubts come out.

Are we sure that the performances shown in the paper are legit? Is there any kind of catch in it?

So, to answer that question we have to do only one thing: find a method to replicate academic results even if it means to
make stupid assumptions on dataset, model or techniques. And we did it, we have made very poor configurations until we found out 
that the problem with the academic study wasn't in the hyperparameters values but with the use of the dataset. 

Trivia: what happens if you train a model with a train set, as in a dataset used for the training phase, and then you use the very
same train set also as val set, as in the dataset which purpouse is to validate the model? Spoiler: amazing results shown but same shitty model.

### Diving into details


