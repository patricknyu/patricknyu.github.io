---
layout: post
title: "Problem 1_6 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-19T23:50:15-08:00
---
### Q:

Given an image represented by an NxN matrix, where each pixel in the image is 4 bytes, write a method to rotate the image by 90 degrees.  Can you do this in place?

### A:

This is actually a cool problem.  It requires you to keep track of a lot of things at once when creating your algorithm.

Essentially you want to go layer by layer through the matrix.  You iterate starting at layer 0 to layer n/2.  Then you have another loop where you take part of each layer you are at and rotate them. Storing one section at a time.  It's easiest to understand if you read through the code.

[Java for Problem 1.6](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/1_6)

[rotate.py](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/Python/1_6)

```python
def rotate(matrix):
	for layer in range(0,len(matrix)/2):
		first = layer
		last = len(matrix)-1-layer
		for i in range(first,last):
			offset = i - first
			top = matrix[first][i]
			matrix[first][i] = matrix[last-offset][first]
			matrix[last-offset][first] = matrix[last][last-offset]
			matrix[last][last-offset] = matrix[i][last]
			matrix[i][last] = top
	return matrix

a = [[1,2,3],[4,5,6],[7,8,9]]
print(rotate(a))
```
