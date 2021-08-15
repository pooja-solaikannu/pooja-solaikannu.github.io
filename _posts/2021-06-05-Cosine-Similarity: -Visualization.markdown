---
layout: "post"
title: "Cosine Similarity: Visualization"
---

## Why do we need this blog?
For an ML researcher, the most desirable skill to have is storytelling with good visualizations. Even when we do the most amazing work with all the fantastic techniques available for ML/DL, all might go in vain if we can't convey the findings in the most simplest way possible.

So, This article is about a possible solution for understanding cosine similarity as simple as way.

>Note - This post does not talk about intricate details of cosine similarity's working. In case if you are here for it, please feel free to check out this link - [Cosine similarity - Understanding the Math]('https://en.wikipedia.org/wiki/Cosine_similarity')

## What does mean by cosine similarity?
Cosine similarity is a metric used to measure how similar the documents are irrespective of their size. Mathematically, it measures the cosine of the angle between two vectors projected in a multi-dimensional space. The smaller the angle, higher the cosine similarity.
```
image
```

## Problem statement
To begin with the solution, we need a problem statement. Since we are trying to undestand cosine similarity, we can check on semantic similarity of words in vector space. 

Vectors are the numerical representation of words in multi-dimensional vector space which helps to perform various manipulations with and around the data.

I have a list of words related to clinical domain to which we are going to work on semantic similarity using cosine distance.
```
List of words :: 
```
I'm using pre-trained model to get the vector representation of these words so that we can go ahead and find semantic similarity of them. I have chosen `ClinicalBERT` to find vectors for our example as it suits the data very much. 
You can check more on clinicalBERT Embeddings by following this [Paper]("https://arxiv.org/abs/1904.03323").

```
Code
```
```
image
```
## Correlation Plot

```
Correlation plot - data format
```

```
Code
```

```
Explanation of plot
```
