# CS5293 Spring 2020 Project 2
# Text Summarizer
### BY Abilash Ramesh
-------
## Contents
* Introduction
* Deep dive
* How to run
-------
## Introduction:
This project is designed to collect multiple text files, perform unsupervised clustering on the text files and assign them to a text file, summarizer the text of files belonging to each cluster and provide an output as a markdown file. The files given to the program as input are in the format .json. 

## Deep Dive:
We first begin by giving the program a path and the percentage of files that need to be taken as input. The function will select a random set of files and use them for the summarization process. The files are then uploaded into a dataframe for easier classification. 

Once this process is done, we proceed to normalize the text by removing any special charecters in the abstract text since that will be used for the clustering. The abstract is comparatively smaller in size which makes it easier to cluster and it surprisingly performs better than clustering with the body text. Once this process of data cleansing is done, we input the clusters into the TF-IDF vectorizer to get the sparse matrix. I choose the TF-IDF due to the ease of hyperparameter tuning to obtain better clusters. Once the sentences are vectorized, the matrix is passed onto the clustering algorithm. We have taken the number of clusters by the following formula:
![equation](http://www.sciweavers.org/upload/Tex2Img_1587968682/render.png)
Where **n** is the number of files taken. 







------
# Reference:
* https://github.com/MaksimEkin/COVID19-Literature-Clustering
* https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge
* https://developers.google.com/machine-learning/clustering/algorithm/advantages-disadvantages
* https://towardsdatascience.com/comparing-text-summarization-techniques-d1e2e465584e
* https://www.analyticsvidhya.com/blog/2018/11/introduction-text-summarization-textrank-python/
* https://towardsdatascience.com/k-means-clustering-algorithm-applications-evaluation-methods-and-drawbacks-aa03e644b48a
* 
