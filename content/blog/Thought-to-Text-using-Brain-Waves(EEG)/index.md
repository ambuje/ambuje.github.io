---
title: "Converting Feeling/Thought to Text using Brain Waves(EEG)"
date: 2019-10-08
draft: false
summary: "Converting Feeling/Thought to Text using Brain Waves(EEG)"
tags: ["Machine Learning","EEG","LSTM"]
categories: ["Machine Learning", "NLP"]
cover:
  alt: "Converting Feeling/Thought to Text using Brain Waves(EEG)"
  caption: "Converting Feeling/Thought to Text using Brain Waves(EEG)"
---

In this article, I will show how you can convert feelings to text i.e if you think forward, forward will come and same for backward left and right. Let me tell you it is a personalized thing as you may think differently from me, for example, thinking forward, one might think he is going and crashing to the wall in front of him :P, one might think he is driving a car. Both are different. It’s still a research project and accuracy achieved is not up to satisfaction. We’ll be working on 4 channel EEG device muse.

> Here I need you to understand and acknowledge how big is this project and it is in research phase, It’s like controlling things with your thoughts, and moreover it’s still human-centric.

![EEG!EEG!EEG!](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*4je6UbIDkl2Ob3W2atPbYA.png)

Imagine you sitting and just thinking of going forward and you actually move forward, isn’t it interesting?

Hardware
--------

We’ll use a 4 channel EEG device muse for doing this task.

![Muse](https://miro.medium.com/v2/resize:fit:778/format:webp/1*6WCw4L1oM0iVdGZjALOo0w.png)

For real time purpose you’ll need a muse monitor app in your mobile from where you can extract the data from your phone to PC through OSC streaming and then feed it to your model and that results can be send to any micro controller to run the motors to move on the specified direction you thought.

### Application

It has a wide variety of application for example movement of wheel chair for people suffering from Locked in Syndrome or full body paralysis. It has a wider research opportunities for thought to text and voiceless communication.

### Information about values EEG device extracts

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*H6q4w43Op9xB8YgNcZ-gjg.png)

It collects data from 4 nodes of our brain, TP9,AF7,AF8,TP10. By extracting the features from muse monitor it gives lot of values, there are 20 relevant values. Delta_TP9, Theta_TP9, Alpha_TP9, Beta_TP9,Gamma_TP9. These 5 values are given and 4 of the nodes give these values, so 4*5=20 features. We consider average of all of them and use 4 features.

### Dataset

We’ll here look into the dataset.

![captionless image](https://miro.medium.com/v2/resize:fit:1020/format:webp/1*SBYkGqMnIk4xhCOUwQeelg.png)

These ch1,ch2,ch3 and ch4 are the nodes mentioned above. Tag is what I am thinking at that moment.I capture **2500 values** which consist of 4 tags i.e F,B,L,R.

### Data pre-processing

Many pre-processing techniques were implemented but result deteriorated.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Zzgp-_NdF3PaI44MhnnxcQ.png)

Importing important libraries and a view of a dataset

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*sQAPCM2w5V8XCoRztV3w7w.png)

1.  Differentiation independent and dependent variables
2.  As tags are F,B,L,R we need to convert it into numbers for processing ,label encoder is used for that and after that one-hot encoding/categorical is done. From now we’ll talk in 0,1,2,3 not in F,B,L,R. For your reference B=0, F=1, L=2, R=3. Label encoder encodes data in alphabetical manner.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*izN9jxAV0RRD-fvTnBQ9Wg.png)

Here the dataset is split in 80/20 ratio.

**Classification** **Techniques**
---------------------------------

I’ll quickly explain you the techniques I tried and will display their results.

1.  **Decision Tree**
2.  **Random Forest**
3.  **KNN**
4.  **Neural Networks — LSTM**

For evaluation purpose we’ll be using confusion matrix and metrics for confusion matrix and it’s related terms refer -

[Simplifying The Confusion Matrix
--------------------------------

### Knowing that the machine learning field is very vast and it has various concepts to understand in it, a very rare and…

medium.com](https://medium.com/datadriveninvestor/simplifying-the-confusion-matrix-aa1fa0b0fc35?source=post_page-----4ba8ba0565ac---------------------------------------)

For more about classification techniques

[Classification Algorithms in Machine Learning…
----------------------------------------------

### What is Classification?

medium.com](https://medium.com/datadriveninvestor/classification-algorithms-in-machine-learning-85c0ab65ff4?source=post_page-----4ba8ba0565ac---------------------------------------)

### 1 — Random Forest

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*XPryuCzYqE--ZjMVIaJFLw.jpeg)

> The [random forest](https://www.stat.berkeley.edu/~breiman/RandomForests/cc_home.htm) is a model made up of many decision trees. Rather than just simply averaging the prediction of trees (which we could call a “forest”), this model uses [two key concepts](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf) that gives it the name _random_:

1.  Random sampling of training data points when building trees
2.  Random subsets of features considered when splitting nodes

For more information about random forest regression

Decision Trees will be discussed after this

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*j3LgkKZLi7v1CApuDqGWiA.png)

Importing important libraries and we can here see the some results of y_test and y_pred. The results are coming like this because we converted into categorical.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ovp4SQpd10fb8YEXkEp-Vw.png)

So it has an accuracy of 0.28 and you can clearly see confusion matrix, precision recall and f1 score

For more information about Random forest:

[Understanding Random Forests
----------------------------

### One Algorithm at a Time- By Harshdeep Singh

medium.com](https://medium.com/@harshdeepsingh_35448/understanding-random-forests-aa0ccecdbbbb?source=post_page-----4ba8ba0565ac---------------------------------------)

### 2 — K Nearest Neighbor

![captionless image](https://miro.medium.com/v2/resize:fit:810/format:webp/1*ybPrsi-aZN1IgWSHZS9U1g.png)

> _An object is classified by a majority vote of its neighbors, with the object being assigned to the class most common among its k nearest neighbors (k is a positive_ [_integer_](https://en.wikipedia.org/wiki/Integer)_, typically small). If k = 1, then the object is simply assigned to the class of that single nearest neighbor._

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Q1DfWvXm3rwcrfpeJMBoWA.png)

Importing important libraries and we can here see the some results of y_test and y_pred.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*BpL92x6oVGc8DfgHxnp-Yg.png)

So it has an accuracy of 0.33 and you can clearly see confusion matrix, precision recall and f1 score

For more about KNN refer —

[Introduction to k-Nearest Neighbors: A powerful Machine Learning Algorithm (with implementation in…
---------------------------------------------------------------------------------------------------

### Note: This article was originally published on Oct 10, 2014 and updated on Mar 27th, 2018 Overview Understand k nearest…

www.analyticsvidhya.com](https://www.analyticsvidhya.com/blog/2018/03/introduction-k-neighbours-algorithm-clustering/?source=post_page-----4ba8ba0565ac---------------------------------------)

### 3 — Decision Tree

> A decision tree is a graph that uses a branching method to illustrate every possible outcome of a decision.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*j3LgkKZLi7v1CApuDqGWiA.png)

Importing important libraries and we can here see the some results of y_test and y_pred.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*nhTAZptBAzapidxuiVKw0A.png)

So it has an accuracy of 0.4 and you can clearly see confusion matrix, precision recall and f1 score

For more information regarding decision tree-

[Decision Trees — A simple way to visualize a decision
-----------------------------------------------------

### Introduction to Decision Trees :

medium.com](https://medium.com/greyatom/decision-trees-a-simple-way-to-visualize-a-decision-dc506a403aeb?source=post_page-----4ba8ba0565ac---------------------------------------)

### 4 — Neural Networks

I also tried deep learning i.e LSTM for this problem. I could achieved **55% accuracy** in that and am still working on it.

A good article on LSTM which would clear your concepts-

[Essentials of Deep Learning : Introduction to Long Short Term Memory
--------------------------------------------------------------------

### Introduction Sequence prediction problems have been around for a long time. They are considered as one of the hardest…

www.analyticsvidhya.com](https://www.analyticsvidhya.com/blog/2017/12/fundamentals-of-deep-learning-introduction-to-lstm/?source=post_page-----4ba8ba0565ac---------------------------------------)

In my LSTM code I used [**RAdam()**](https://medium.com/@lessw/new-state-of-the-art-ai-optimizer-rectified-adam-radam-5d854730807b) as an optimizer and categorical cross-entropy was used as a loss function.

### Accuracy

Why my accuracy is so low?

I have to find some ways of data pre-processing for my type of problem. Data pre-processing techniques applied till now-

1.  Min-Max scaler
2.  Standardization
3.  Mean normalization

No variety of data

I have to increase my dataset to make this a success.

**Thanks and happy learning :)**