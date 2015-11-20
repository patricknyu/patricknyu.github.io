---
layout: post
title: "Problem 1_4 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-19T23:29:07-08:00
---
### Q:
Write a method to replace all spaces in a string with '%20'.  You many assume that the string has sufficient space at the end of the sting to hold the additional characters, and that you are given the "true" length of the string.

### A:
This was my first approach.

First I split up my string to a character array.  I added each character to a StringBuilder.  Every time I encountered a space, I inserted a '%20'.

When I was using Python, I was able to just put my strings into a list and then join the list.

I also created a more standard implementation where I counted the spaces, created an empty array of the original length plus space length multiplied by 3.  Then I iterated through my character array and inserted '%20' when I encountered spaces.

Neither of these solutions are in place.  My java solution was in place.

[Java for Problem 1.4](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/1_4)

[replaceSpace.py](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/Python/1_4)

```python
import fileinput
def replaceSpace(s):
	charArr = list(s)
	charArrAns = []
	for i in charArr:
		if(ord(i)==32):
			charArrAns.append('%20')
		elif(i != '\n'):
			charArrAns.append(i)
	return ''.join(charArrAns)

# Python makes this a bit too easy.  I'll try to rewrite it so it's more java like

def replaceSpace2(s,length):
	charArr = list(s)
	emptySpaces = 0
	for i in charArr:
		if(ord(i)==32):
			emptySpaces+=1
	answerArr = ['' for i in range(0,length+emptySpaces*3)]
	j =0
	for i in charArr:
		if(ord(i)==32):
			answerArr[j] = '%'
			answerArr[j+1] = '2'
			answerArr[j+2] = '0'
			j+=3
		elif(i !='\n'):
			answerArr[j] = i
			j+=1
	return ''.join(answerArr)
if __name__ == "__main__":
	for line in fileinput.input():
		print(line)
		print(replaceSpace(line))
		print(replaceSpace2(line,len(str(line))-1))
```
