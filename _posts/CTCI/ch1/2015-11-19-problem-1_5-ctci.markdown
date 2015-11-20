---
layout: post
title: "Problem 1_5 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-19T23:43:29-08:00
---

### Q:

Implement a method to perform basic string compression using the counts of repeated characters.  For example, the string aabcccccaaa would become a2b1c5a3.  If the "compressed" string would not become smaller than the original string, your method should return the original string.  You can assume the string has only upper and lower case letters (a-z).

### A:

This is an easy question if you use a StringBuilder/StringBuffer in Java.  It's just as easy in Python using a list.

First, write a method to check what the compressed length would be.  If not shorter, don't run your compression.

As far as the compression - you can iterate through a character array while carrying a count and last character.  Each time your current character is equal to the last character. You add 1 to count.  If they are not equal add the last character and the last character's count to your Python list/StringBuilder.  Then set last character to current one and set count to 1.

[Java for Problem 1.5](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/1_5)

[compressString.py](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/Python/1_5)

```python
import fileinput
def checkCompression(charArr):
	original = len(charArr)-1
	new = 0
	currentChar = ''
	for i in charArr:
		if(i == '\n'):
			continue
		if(currentChar == ''):
			currentChar = i
			new = 2
		if(i != currentChar):
			currentChar = i
			new+=2
	return new
def compress(s):
	charArr = list(s)
	if(checkCompression(charArr)>= len(charArr)-1):
		return s
	currentChar = ''
	currentCount = 0
	answer = []
	for i in charArr:
		if(i == '\n'):
			answer.append(currentChar)
			answer.append(currentCount)
		if(currentChar == '' and currentCount == 0):
			currentChar = i
			currentCount = 1
		if(currentChar ==i):
			currentCount+=1
		elif(i !=currentChar):
			answer.append(currentChar)
			answer.append(currentCount)
			currentChar = i
			currentCount = 1
	if(len(answer) < len(charArr)-1):
		return ''.join(str(i) for i in answer)
	return s

# This is a bit slow since we don't check for it being short till the end.
# if this was Java we should be using a StringBuilder


if __name__ == "__main__":
	for line in fileinput.input():
		print(line)
		print(compress(line))
```
