---
layout: post
title: "Effective C++"
date: 2018-09-19
categories: [Languages]
tags: [c++, program]
use_math: true
---

## Item 1: View C++ as a federation of languages
All the "proper usage" rules seem to have exceptions. How are we to make
sense of such a language?

The easiest way is to view C++ not as a single language but as a federation 
of related languages. Within a particular sublanguage, the rules tend to be
simple, straightforward, and easy to remember. 
1. C
1. Object-oriented C++
1. Template C++
1. The STL

Keep these four sublanguages in mind, and don't be surprised when you
encounter situations where effective programming requires that you change
strategy when you switch from one sublanguage to another.

## Item 2: Prefer consts, enums, and inlines to #defines
