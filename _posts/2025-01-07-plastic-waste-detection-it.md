---
layout: post
title: Non tutti i modelli pubblicati sono dei benchmark validi
lang: it
permalink: 2025/01/07/plastic-waste-detection
published: false
---

Training a model with deep leaning technics could be very complex if you don't know how to set up properly hyperparameters. 
To avoid headaches you can tune the hyperparameters and find the subset of values that will increase the performance of your model.
Or if you are short on time you could do a little research and look if somebody already do the tuning part.
You can register the hyperparameters configuration and also take others results as benchmark for your work.
The purpouse of doing that is to get a work direction in the first place, with a starting point for your tuning, and a benchmark to improve if possible.
This is what I wanted to do in one of the last projects that I did at university.

### Contesto del modello

My assignment was to train a model that is able to detect plastic waste in water surfaces like rivers and lakes. 
I worked with a friend of mine and both decided to use the YOLOv8 architecture and train it with a dataset that was aviable during our work.
We did some experiment without any particular result in performance.