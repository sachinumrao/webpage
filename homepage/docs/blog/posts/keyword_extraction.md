---
draft: false
title: Keyword Extraction Methods
description: A short guide on keyword extraction in python
date:
    created: 2019-08-15
    updated: 2019-08-15
tags:
    - NLP
---

# Keyword Extraction

![keyword extraction](./../../assets/keyword_extraction.jpeg)
*Image Credit: www.adaringadventure.com*

### Keyword Extraction using RAKE

#### 1. Why perform keyword extraction?

* Reduces the dimensionality of text 
* Find summery of text (_What this documents is about?_)
* Fetch similar documents in _Information Retrieval_ System
* Classify Documents when there are large number of categories

#### 2. How to perform keyword extraction?

    I. Candidate Selection
    
    II. Property Calculation
    
    III. Scoring of potential keywords and final selection

#### 3. Rapid Automatic Keyword Extraction (RAKE)

*  Use punctuations and stopwords as boundaries. Keyword phrases are assumed to be lying between these boundaries (_in ideal case tokens should be stemmed as well before this step_). These words are often called **Candidate Words/Phrases**.

*  RAKE computes the properties of each candidate, which is the sum of score for each word in phrase. The words are scored according to their frequency and typical length of candidate phrase in which they appear.

*  Rank keywords based on RAKE score

#### 4. Error Estimation

* Match keywords obtained from model with keywords hand assigned to the document.

* Precision : Percentage of correct keywords among those extracted

* Recal : Percentage of correctly extracted keywords among all correct ones


### Additional Notes

#### Advantages of RAKE

    I. Doamin Independence
    
    II. Good Precision

#### Scoring in RAKE

Score(word) = Degree(word) / Frequency(word)

Frequency(word) = Number of times word occurs in document

Degree(word) = Similar to degree of node in a graph. It is number of times a certain word co-occurs with other candidate keyword 