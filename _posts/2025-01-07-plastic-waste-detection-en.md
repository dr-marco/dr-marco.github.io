---
layout: post
title: Not every published model is a valid benchmark
lang: en
permalink: 2025/01/16/plastic-waste-detection
published: true
---

Training a model with deep leaning techniques could be very complex if you don't know how to set up properly hyperparameters. 
To avoid headaches you can tune them and find the subset of values that will optimize the performances of your model.
Or if you are short on time you could do a little research and look if somebody already did the tuning part.
You can register the hyperparameters configuration and also take others results as benchmark for your model.
The purpose of doing that is to get a starting point for your tuning and a benchmark to improve if possible.
This is in the end what I wanted to do in one of the last projects that I did at university.

### My assignment

My assignment was to train a model that is able to detect plastic waste in water surfaces like rivers and lakes. 
I worked with a friend of mine and both decided to use the YOLOv8 architecture and train it with a dataset that was available during our work.[^1]
We did some experiment without any particular result in performance so we have looked around searching for academic papers or some 
post on the internet that was somehow relevant.
We have bumped mostly in detection with dataset containing satellite images except one study published in early 2024[^2] that
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
same train set also as val set, as in the dataset which purpose is to validate the model? Spoiler: amazing results shown but same shitty model.

### Diving into details

The dataset used [^1] contains 3 different subsets, `train`, `val` and `test`, each designed for his specific purpose as mentioned before in the sarcastic question (the test set is used to test the model once the training phase is completed).
Inside each subset there are quite a lot different images labeled with 4 different kind of classes using the YOLO specification (see the [YOLO documentation](https://docs.ultralytics.com/datasets/detect/) to learn more about it).

In order to evaluate the goodness of the trained model many metrics are used like precision, recall and loss functions. 
In particular for object detection models the main loss functions are the `box_loss` and `cls_loss`, the latter tell us the misclassification rate and the former the error during the drawing of the box over the detected objects on the image.
But one of the best metric that can summarize how good the detection model really was is the `mAP50`: mean average precision over all classes used.
Again, for more details about the metrics that can be used in object detection models check the documentation [here](https://docs.ultralytics.com/guides/yolo-performance-metrics/).

For simplicity here I will comment only the mAP50: this percentage metric is better and better when it is higher and higher until 100%. 

With our tests we were able to reach an overall mAP50 of 39.1%. It wasn't very good since the model was good with a specific class, `PLASTIC_BOTTLE` and bad with the others. And as you can see in the following graphs there is no margine of improvements because the model with extra training could overfit.

![Loss functions and metrics of our trained model]({{site.baseurl}}/assets/images/plastic_detection/results_1.png)
*Loss functions and metrics of our trained model*

As you can see these metrics weren't as good as those in the paper. The authors claimed their model could reach 68.8%

![Loss functions and metrics of the paper model]({{site.baseurl}}/assets/images/plastic_detection/results_2.png){:width:"1440px" } 
*Loss functions and metrics of the paper model (sorry for bad image resolution)* 

![Loss functions and metrics matching paper model]({{site.baseurl}}/assets/images/plastic_detection/results_3.png){:width="1440px" }
*Quite the same behavior with the metrics* 

### Ok, why is it bad?

as you can see
overfitting
memorizing the dataset and not learning the detection function

Using the same subset of data for both training and validation in a machine learning model is problematic because it leads to overfitting 
and an inaccurate assessment of model performance. The model essentially "memorizes" the training data, resulting in artificially high accuracy 
during validation. This provides no indication of how the model will perform on unseen data, undermining its generalizability and real-world 
applicability. Proper validation requires a separate, unseen dataset to evaluate the model's ability to generalize beyond the training data.



[^1]: Dataset used: `plastic_in_river`. Unfortunately the dataset is not available anymore. [Here](http://web.archive.org/web/20240821170803/https://huggingface.co/datasets/kili-technology/plastic_in_river) the wayback machine archive linking dataset page from huggingface in August 2024.

[^2]: _Plastic Waste on Water Surfaces Detection Using Convolutional Neural Networks_: [Here](https://ceur-ws.org/Vol-3668/paper13.pdf) you can read the paper