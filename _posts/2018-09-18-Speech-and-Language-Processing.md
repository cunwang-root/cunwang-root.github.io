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
    P(w_n|w_{n-1}) = \frac{C(w_{n-1}w_n)}{\sum_wC(w_{n-1}w)} = \frac{C(w_{n-1}(n))}{C(w_{n-1})} 
\end{align}
$$

We always represent and compute language model probabilities in log format
probabilities log as __log probabilities__.
Since probabilities are (by definition) less than or equal to 1,
the more probabilities we multiply together, the smaller the product becomes.
Multiplying enough N-grams together would result in numerical underflow.
By using log probabilities instead of raw probabilities, we get numbers
that are not as small.

### 4.2 Evaluating Language Models
The best way to evaluate the performance of a language model is to embed it in
an application and measure how much the application improves.
Such end-to-end evaluation is called __extrinsic evaluation__.

An __intrinsic evaluation__ metric is one that measures the quality of a model
independent of any application.

In practice we don’t use raw probability as our metric for evaluating language
models, but a variant called __perplexity__.

The perplexity (sometimes called PP for short) of a language model on a test
set is the inverse probability of the test set, normalized by the number of
words. For a test set $W = w_1w_2 \ldots w_N$,:
$$
\begin{align}
    PP(W) &= P(w_1w_2 \ldots w_n)^{-\frac{1}{N}} \\
          &= \sqrt[N]{\frac{1}{P(w_1w_2 \ldots w_N)}}
\end{align}
$$
                  
There is another way to think about perplexity: as the __weighted average
branching factor__ of a language. The branching factor of a language is the number
of possible next words that can follow any word.

An (intrinsic) improvement in perplexity does not guarantee an (extrinsic)
improvement in the performance of a language processing task like speech
recognition or machine translation. Nonetheless, because perplexity often
correlates with such improvements, it is commonly used as a quick check on
an algorithm.

### 4.3 Generalization and Zeros
These __zeros__—things that don’t ever occur in the training set but do occur in
the test set—are a problem for two reasons.
1. Their presence means we are underestimating the probability of all sorts of
words that might occur, which will hurt the performance of any application
we want to run on this data.
1. If the probability of any word in the test set is 0, the entire probability
of the test set is 0.

Unknown Words

In a __closed vocabulary__ system the test set can
only contain words from a lexicon, and there will be no unknown words.

In other cases we have to deal with words we haven’t seen before, which we’ll
call __unknown__ words, or __out of vocabulary (OOV)__ words.
There are two common ways to train the probabilities of the unknown word
model \<UNK\>.
The first one is to turn the problem back into a closed vocabulary one
by choosing a fixed vocabulary in advance.
The second alternative, in situations where we don’t have a prior vocabulary in
advance, is to create such a vocabulary implicitly, replacing words in the
training data by \<UNK\> based on their frequency.

### 4.4 Smoothing
What do we do with words that are in our vocabulary (they are not unknown words)
but appear in a test set in an unseen context (for example they appear after a
word they never appeared after in training)?

To keep a language model from assigning zero probability to these unseen events,
we’ll have to shave off a bit of probability mass from some more frequent
events and give it to the events we’ve never seen.
This modification is called __smoothing__ or __discounting__.

__Laplace Smoothing__

The simplest way to do smoothing is to add one to all the bigram counts, before
we normalize them into probabilities.

__Add-k smoothing__

One alternative to add-one smoothing is to move a bit less of the probability
mass from the seen to the unseen events.

__Backoff and Interpolation__

Sometimes using less context is a good thing, helping to generalize more for
contexts that the model hasn’t learned much about. 
In __backoff__, we use the trigram if the evidence is sufficient, otherwise we
use the bigram, otherwise the unigram.
In other words, we only “back off” to a lower-order N-gram if we have zero
evidence for a higher-order N-gram.
By contrast, in __interpolation__, we always mix the probability estimates
from all the N-gram estimators, weighing and combining the trigram, bigram, and
unigram counts.

In order for a backoff model to give a correct probability distribution, we have
to __discount__ the higher-order N-grams to save some probability mass for the lower
order N-grams. 

This kind of backoff with discounting is also called Katz backoff.

### 4.5 Kneser-Ney Smoothing
