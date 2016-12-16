---
title       : Next Word Predictor
subtitle    : 
author      : SJ Evans
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

This presentation explains my approach to complete the Data Science Capstone assingment to generate a 'Next Word Predictor' that accepts an ngram or phrase and predicts the next word. 

The project leveraged datasets from Swifkey containing sample text from blogs, news sources and twitter feeds to train the algorithms. The original training data can be found at:

https://d396qusza40orc.cloudfront.net/dsscapstone/dataset/Coursera-SwiftKey.zip

--- .class #id 

## General Strategy

1. Identify most frequent words that represent at least 90% of word usage.
2. Build a list of words that follow the most frequent words.
3. Build a correlation matrix of words that are associated in the training text.
4. Create an algorithm that uses that uses the last word in an ngram to create a list of possible words and the other words in the ngram to choose the best one.

---

## Detailed Strategy - Building Tables

1. Sampled 10% of blogs, news and twitter feeds.
2. Used NLP (tm package) to create corpus -> document term matrix -> word correlation matrix with correlation coeffecient for each word pair.
3. Also created list of words that followed each of the most frequent words and the percentage of time that each word was the next word to get a probablity table with most frequent words as columns and next words as rows.
4. Saved tables as inputs for the word predicting algorithm.

---

## Detailed Strategy - Next Word Algorithm

1. Create function that accepts a string (ngram) is input and strips stopwords, white space, numbers and punctuation using the tm package.
2. Use the last word in the ngram to subset the table of possible nextwords and capture the probabity of each nextword
3. Use all words in the ngram to subset the word correlation matrix and find the average correlations between all input words and each words from the subset next word table.
4. Multiply the probability of each word being the next word by the average correlation coefficients for that word with the input words and find the maximum value.

---

## Shiny App

The shiny app works by:

1. Loading the word correlation and next word tables into the background
2. Accepting a text string and plugging it into the algorithm function
3. Finding the word with the maximum probablilty based on the algorithm and returns that word.

*The algorithm will not return any word until the input string has at least one word that matches the most frequent word list, which contains 5,215 words that represent at least 90% of all word usage in the originally sampled data.

The app can be found at:

https://sjevans242.shinyapps.io/NextWordPredictor/





