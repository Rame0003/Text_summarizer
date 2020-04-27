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

### 1. File reader:

**Function input -> readfiles(file path, % of files)**

We first begin by giving the program a file path and the percentage of files that need to be taken as input. The function will select a random set of files and use them for the summarization process. The files are then uploaded into a dataframe for easier classification. The files are picked in random by generating a number between the range of 0 to the number of files. Once the file indices are generated, the files are uploaded to a list and the list is passed onto a function that reads the data from the json files and uploads into a dataframe. 

The data that we extract are mainly the filename/paper ID, text from the body and text from abstract. 

**Function input -> createDB(filenames)**

Once the list of files have been passed onto the function, the function returns the dataframe and the dataframe is used to perform the indexing and further operations. I chose to upload the text into a dataframe as it is easier to group the cluster when the indices of the files are known to us. Once this is done, we preprocess the text to perform further analysis.

### 2. Text tokenizer:

Once this process is done, we proceed to normalize the text by removing any special charecters in the abstract text since that will be used for the clustering. The abstract is comparatively smaller in size which makes it easier to cluster and it surprisingly performs better than clustering with the body text. Since the abstract represents each paper/article that has been published, we do not perform any tokenization and hence we pass on the value as such into the vectorizer. For the process of removing stopwords and converting the sentences to lower case, we use the following function:

**Function input -> normalize(text)**

Once this process of data cleansing is done, we input the array of summaries into the TF-IDF vectorizer to get the sparse matrix. I choose the TF-IDF due to the ease of hyperparameter tuning to obtain better clusters. I have set my n_gram range to 2 to 4 words as most of the words that I had explored during topic modeling studies were detected better when 2-grams were allowed. I tried to also set the max_df parameter but understood that it was not as effective as the value provided by the use of n-grams. We have also mentioned the use of English stopwords. Since we have already normalized our text, we will take this only as a precautionary step. 

### 3. KMeans Clustering:

Once the sentences are vectorized, the matrix is passed onto the clustering algorithm. We have taken the number of clusters by the following formula:

![equation](http://www.sciweavers.org/upload/Tex2Img_1587968682/render.png)

Where **n** is the number of files taken (Twinandilla et al, 2018). 

The cluster labels are attained once the clustering is done. These labels allow us to group the files by clusters 
The text is grouped by cluster and a new dataframe is created. This new dataframe will contain the text from the clustered files. Once the data is loaded, we proceed to normalize (stopword/special charecters removal only) the text and proceed to the summarization portion. We use the lexrank algorithm to perform the summarization process. 

The summarized text is then written into a markdown file labelled **output_#.md** denoting the cluster number #'s output. Additionally, the markdown file will have the first line denoting the cluster that it belongs to. 







------
# Reference:
* https://github.com/MaksimEkin/COVID19-Literature-Clustering
* https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge
* https://developers.google.com/machine-learning/clustering/algorithm/advantages-disadvantages
* https://towardsdatascience.com/comparing-text-summarization-techniques-d1e2e465584e
* https://www.analyticsvidhya.com/blog/2018/11/introduction-text-summarization-textrank-python/
* https://towardsdatascience.com/k-means-clustering-algorithm-applications-evaluation-methods-and-drawbacks-aa03e644b48a
* https://www.sciencedirect.com/science/article/pii/S1877050918315138#abs0001
