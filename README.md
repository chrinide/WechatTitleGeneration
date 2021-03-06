# Generate Wechat title from given content

The objective of this project is to generate wechat title from the given content.  We use the start-of-the-art seq2seq model to build the summarizer.  This model is based on RNN and LSTM.  In the current literature, this method is much better than previous abstractive summarization methods.  To build this model, we refer to many existing methods, e.g., Google's model of text summarization with RNN, and Siraj's video and code on text summarization with deep learning. We will use collected Wechat articles(contents and titles) to train and test the model we are going to build. 

## Phases  
This project is divided into a few phases.  

* Phase I:  We will use the basic seq2seq model with RNN to build the summarizer and train it with Wechat articles accumulated
* Phase II:  We want to add the attention module into this. 
* Phase III: We want to add more words(not only in the input vocabulary, but also in the neighborhood of the input vocabulary
* Phase IV:  We want to classify wechat article titles into different categories.  We want to generate different styles of article title.  

Now, we are in Phase I, i.e., we are going to initialize the project and build the basic seq2seq model.  

## Preprocessing of the dataset. 
* Input:  
    1. Wechat file content and title, 
    2. Word embedding file(access link/overall file) 
* Output:   
    1. Vocabulary of the input： ordered by frequency desc. This is a list
    2. word2ind: position of each word in the vocabulary list.  This is a dictionary. 
    3. ind2word: word in the index of the list.  This is a dictionay.  It has be replaced by accessing the vocabulary array directly.  
    4. embedding matrix: this is a N x D matrix.  We are going to shrink it to the size of the input vocabulary.  In this way, we don't need to use a lot of memory to store unrelated words for this task.  
    5. ind2embedding: for each word in the vocabulary, find its index in the embedding matrix.  
    
## Generate the training/test data.  
In this step, we first build the overall feature matrix(X) and the target vector(Y).  Please note that both X and Y are composed of integer arrays.  For example, X[0] = [10, 1, 32, 8, 54, ... ], Y[0] = [10, 32, 6, ...].  Each integer represents the word in the vocabulary. 

Based on percentage given, we split the X and Y correspondingly into X_train, X_test and Y_train, Y_test.  

## Build the sequence to sequence model. 

1. Initialize the network configuartion. 
2. Build the encoder: RNN, n layers. 
3. Build the decoder: RNN, n layers. 

## Train the model 
4. Add the cost function and gradient method. 
5. Train the model 

## Test the model 
6. Use beam search to generate a summarization sentence.  Compare the predicted title with the actual title. 


# References to Siraj's github project

# How_to_make_a_text_summarizer
This is the code for "How to Make a Text Summarizer - Intro to Deep Learning #10" by Siraj Raval on Youtube

# Coding Challenge - Due Date - Thursday, March 23rd at 12 PM PST

The challenge for this video is to make a text summarizer for a set of articles with Keras. You can use any textual dataset to do this. By doing this you'll learn more about encoder-decoder architecture and the role of attention in deep learning. Good luck!

## Overview

This is the code for [this](https://youtu.be/ogrJaOIuBx4) video on Youtube by Siraj Raval as part of the Deep Learning Nanodegree with Udacity. We're using an [encoder-decoder](https://www.tensorflow.org/tutorials/seq2seq) architecture to generate a headline from a news article.

## Dependencies

* [Tensorflow](https://www.tensorflow.org/versions/r0.10/get_started/os_setup.html) or [Theano](http://deeplearning.net/software/theano/install.html)
* Keras 
* python-Levenshtein (pip install python-levenshtein)

Use [pip](https://pypi.python.org/pypi/pip) to install any missing dependencies 

## Basic Usage

### Data
The video example is made from the text at the start of the article, which I call description (or `desc`),
and the text of the original headline (or `head`). The texts should be already tokenized and the tokens separated by spaces.
[This](http://research.signalmedia.co/newsir16/signal-dataset.html) is a good example dataset. You can use the 'content' as the 'desc' and the 'title' as the 'head'. 

Once you have the data ready save it in a python pickle file as a tuple:
`(heads, descs, keywords)` were `heads` is a list of all the head strings,
`descs` is a list of all the article strings in the same order and length as `heads`.
I ignore the `keywrods` information so you can place `None`.

[Here](http://opendata.stackexchange.com/questions/4981/dataset-of-major-newspapers-content) is a link on how to get similar datasets

### Build a vocabulary of words
The [vocabulary-embedding](./vocabulary-embedding.ipynb)
notebook describes how a dictionary is built for the tokens and how
an initial embedding matrix is built from [GloVe](http://nlp.stanford.edu/projects/glove/)

### Train a model
[train](./train.ipynb) notebook describes how a model is trained on the data using [Keras](http://keras.io/)

### Use model to generate new headlines
[predict](./predict.ipynb) generate headlines by the trained model and
showes the attention weights used to pick words from the description.
The text generation includes a feature which was
not described in the original paper, it allows for words that are outside
the training vocabulary to be copied from the description to the generated headline.

## Examples of headlines generated
Good (cherry picking) examples of headlines generated
![cherry picking of generated headlines](./cherry_picking.png)
![cherry picking of generated headlines](./cherry_picking1.png)

## Examples of attention weights
![attention weights](./attention_weights.png)

## Credits
The credit for this code goes to [udibr](https://github.com/udibr) i've merely created a wrapper to make it easier to get started. 
