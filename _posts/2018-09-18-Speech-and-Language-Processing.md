---
layout: post
title: "Speech and Language Processing"
date: 2018-09-18
categories: [Machinelearning]
tags: [NLP, machine learning, deep learning]
use_math: true
---
## 4. Language Modeling with N-grams
Probabilities are essential in any task in which we have to identify words
in noisy, ambiguous input, like speech recognition or handwriting recognition.

Models that assign probabilities to sequences of words are called __language
models__ or __LMs__.

In this chapter we introduce the simplest model that assigns probabilities
to sentences and sequences of words, the __N-gram__. An N-gram is a sequence of
N words.

In a bit of terminological ambiguity, we usually drop the word “model”, and thus
the term N-gram is used to mean either the word sequence itself or the predictive
model that assigns it a probability.

### 4.1 N-Grams
The intuition of the N-gram model is that instead of computing the probability
of a word given its entire history, we can approximate the history by just the
last few words.

The assumption that the probability of a word depends only on the previous word
is called a Markov assumption.

How do we estimate these bigram or N-gram probabilities? An intuitive way to
estimate probabilities is called __maximum likelihood estimation__ or __MLE__.
$$
\begin{align}
    \begin{split}
        P(w_n|w_{n-1}) &= \frac{C(w_{n-1}w_n)}{\sum_wC(w_{n-1}w)} \\
                       &= \frac{C(w_{n-1}(n))}{C(w_{n-1})} 
    \end{split}
\end{align}
$$
                  

