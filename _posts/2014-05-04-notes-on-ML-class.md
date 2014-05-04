---
layout: post
title:  "Notes on Andrew Ng's Machine Learning Class"
categories: machine learning
---

============================================

I've been taking Andrew Ng's Machine Learning class on Coursera and have found it to be a great course so far. In addition to learning about algorithms that I hadn't tried before (ie. Neural Networs and SVMs), though, Professor Ng does a great job of putting everything together and looking at the big picture beyond specific ML methods. 
One of my favorite topics was last week's when, instead of going over a new ML algorithm he talked his general approach to modeling, how to diagnose problems in your models and what strategies you can use to improve them. So here are my notes on the topic.

General Approach
----------------

+ Take out a portion of your data to be used as a test set and doen't touch until you are comfortable with your models.
+ Use a simple algorithm (something quick to implement) and test it on a cross-validation set.
+ Look at error rates and learning curves to decide if more data or more features are likely to help
+ Use error analysis to see if there are systematic trends in you errors
+ Add features/implement more complicated models if needed
+ Altenately look for more samples and repeat


Deciding What to Try Next
-------------------------
Whenever you want to improve the performance of a predictive model you have a few options you can consider. As exmaples you can:

+ Get more data to train on
+ Try smaller sets of features
+ Try additional/completely new features
+ Try creating more features with transformations (polynomial terms, interactions)
+ Increasing/decreasing the lambda or other complexity paremeters in the model

Instead of wasting your time trying random things out, learning curves can help diagnose the problem and point you to what to try next.

### The Variance/Bias Tradeoff

A good question to ask is whether your model suffers from high variance or high bias. As a reminder:

+ High Bias models vary little depending on the data sample but don't predict the correct value because they are too simplistic (ie. underfit the data)
+ High Variance models fit the data very closely so they tend to vary a lot with changes in the sample. This can lead to overfitting the data.

Learning curves can be used to identify high variance from high bias problems.

### Learning Curves

Learning curves plot the erro of the model as you increase the seize of the training set. As you increase the size of the set, the error rate on the training set is likely to increase (because even simple models can perfectly fit the data in small enough samples) but the error rate on the validation sample is likely to very high models trained on small samples and should decrease gradually as the size increases.

![Learning Curve](/images/LearnngCurve.PNG "Learning Curve")

High bias models are characterized by high error rates in both traning and validation sets but the the errors may approximate each other (since there is no overfitting).

![Learning Curve](/images/HighBias.PNG "High Bias Curve") 

High variance models usually have low training error but higher than desired validation error (with a large gap between them) which are signs of overfitting. Getting a larger sample size will ameliorate overfitting and improve validation error.

![Learning Curve](/images/HighVariance.PNG "High Variance Curve")

Error Analysis
-------------- 

Error analysis, as the name implies, means taking a look at your errors (manually) and identifying systematic trends in what kind of misclassifications the algorithm is making. Looking at the data this way could help you identify new features you can use to improve the model. For example, if a spam filter model tends to miss pharmaceutical advertisements as spam you may need to add features for terms that are regularly used in those types of ads.

Cross-Validation
----------------
As allways, if you are trying to compare models after making changes, use cross-validation error(instead of training sample error) to evaluate them. This let's you try different variations of your model or features. For example should you stem words before runing the model?

