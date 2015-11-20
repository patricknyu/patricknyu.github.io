---
layout: post
title: "Problem 1_3 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-19T23:25:33-08:00
---
###Q:
Given two strings, write a method to decide if one is a permuation of the other.

###A:
Essentially I chose to count the count of each character (assuming that we only were given alphabet lower case characters) and compare.

The runtime should be at O(n).

Here's the Java solution.

[Java for Problem 1.3](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/1_3)

Here's the Python one.

[Permutation.py](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/Python/1_3)


```python
import fileinput
import re

def permutation(s1,s2):
	if(len(s1)!=len(s2)):
		return False
	s1charArr = list(s1)
	s2charArr = list(s2)
	s1charCount = [0 for i in range(0,26)]
	s2charCount = [0 for i in range(0,26)]

	for i in range(0,len(s1)):
		if(s1[i] != '\n'):
			s1charCount[ord(s1[i])-97]+=1
		if(s2[i] != '\n'):
			s2charCount[ord(s2[i])-97]+=1
	for i in range(0,26):
		if(s1charCount[i] !=s2charCount[i]):
			return False
	return True

if __name__ == "__main__":
	for line in fileinput.input():
		s = re.split('\s+', line)
		print(s[0])
		print(s[1])
		print(permutation(s[0],s[1]))
```
