---
layout: post
title: "Problem 1_1 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-18T22:24:27-08:00
---
###Q
Implement an algoirthm to determine if a string has all unique characters.  What if you cannot use additional data structures?

###A

Here's the Java solution.

[Java for Problem 1.1](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/1_1)

Here's the Python one.

[Python for Problem 1.1](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/Python/1_1)

```python
import fileinput

def unique(s):
	charArr = list(s)
	charIdx = [0]*26
	#print(charArr)
	for i in charArr:
		if(i=='\n'):
			continue
		if(charIdx[ord(i)-97] == 1):
			return False
		else:
			charIdx[ord(i)-97]+=1
	return True

if __name__ == "__main__":
	for line in fileinput.input():
		print(line)
		print(unique(str(line)))
```

I'm not going to do 1.2 since it is a C++ problem.  My C++ is nowhere near strong enough to do difficult problems.