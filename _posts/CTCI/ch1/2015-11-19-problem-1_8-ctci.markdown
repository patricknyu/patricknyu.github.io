---
layout: post
title: "Problem 1_8 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-19T23:58:37-08:00
---
### Q:
Assume you have a method isSubstring which checks if one word is a substring of another.  Given two strings, s1 and s2, write code to check if s2 is a rotation of s1 using only one call to isSubstring.

### A:
I think this problem is really cool.

What you do is use one of the strings and create a string that is that string twice.  For example, if your two strings are "racecar" and "ecarrac", you take the first string and create a new string, "racecarracecar".  Then you run isSubstring("racecarracecar","ecarrac").

Super cool solution.

[Java for Problem 1.8](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/1_8)

[rotation.py](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/Python/1_8)

```Python
import fileinput
import re

def rotation(s1,s2):
	if(len(s1)!=len(s2) or len(s1)==0):
		return False
	return True if (s2 in s1+s1) else False

if __name__ == "__main__":
	for line in fileinput.input():
		s = re.split('\s+', line)
		print(s[0])
		print(s[1])
		print(rotation(s[0],s[1]))
```
