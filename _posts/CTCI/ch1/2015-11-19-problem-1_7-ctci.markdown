---
layout: post
title: "Problem 1_7 [CTCI]"
modified:
categories: /ctci/ch1
excerpt:
tags: []
image:
  feature:
date: 2015-11-19T23:54:41-08:00
---
### Q:
Write an algorithm such that if an element in an MxN matrix is 0, its entire row and column are set to 0.

### A:
This problem isn't to interesting to me personally.

You create an boolean array for rows sized at M and an boolean array for columns sized N.  You iterate through the matrix.  If you encounter a 0, you set the respective values in the boolean arrays to true.

Then you iterate through each array.  At every truth, call a helper method to set 0s.

[Java for Problem 1.7](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/1_7)

[setZeros.py](https://github.com/patricknyu/CtCInterview/tree/master/ch_1/Python/1_7)

```python
def setCol(matrix,col):
	numRows = len(matrix)
	numCols = len(matrix[0])
	for i in range(0,numRows):
		matrix[col][i] = 0
	return matrix
def setRows(matrix,row):
	numRows = len(matrix)
	numCols = len(matrix[0])
	for i in range(0,numCols):
		matrix[i][row] = 0
	return matrix
def setZeros(matrix):
	RowZeros = [False for i in range(0,len(matrix))]
	ColZeros = [False for i in range(0,len(matrix[0]))]
	for i in range(0,len(matrix)):
		for j in range(0,len(matrix[0])):
			if(matrix[i][j] == 0):
				RowZeros[i] = True
				ColZeros[i] = True
	for i in range(0,len(RowZeros)):
		if(RowZeros[i]):
			matrix = setCol(matrix,i)
	for i in range(0,len(ColZeros)):
		if(ColZeros[i]):
			matrix = setRows(matrix,i)
	return matrix

a = [[1,2,3],[4,0,6],[7,8,9]]
print(setZeros(a))
```
