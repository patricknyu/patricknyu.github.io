---
layout: post
title: "Chapter 1 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-18T22:22:00-08:00
---

I'm starting from the beginning.  I've done most of these problems and for the most part, they aren't too dificult.  I'm rewriting them in Python which feels like cheating sometimes.

#Chapter 1

##Arrays and Strings

###HashTables
- Contains an underlying array and a hash function.
- Underlying data structure can also be a binary search tree.
- In this case look up time is O(log(n)) due to balancing.
- Otherwise, insert, search, delete are all O(1) in the average case and O(n) in the worst

###ArrayList
- Array without a set length.
- Each time we run out of space, the array doubles.
- Double takes O(n) time but it rarely happens, so it is still O(1).
- Lookup is O(1)

###StringBuffer
- This is so useful.  It's an efficient way to concatenating strings.
- Pretty much puts the string in an array.
