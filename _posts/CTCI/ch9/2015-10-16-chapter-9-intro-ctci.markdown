---
layout: post
title: "Chapter 9 Intro[CTCI]"
modified:
categories: /ctci/ch9
excerpt:
tags: []
image:
  feature:
date: 2015-10-16T16:29:32-07:00
---
## Recursion and Dynamic Programming

#### Approach

When trying to solve f(n), we have to look at f(n-1) first.

There are two types of recursive approaches that are pretty basing.

The first is bottom up recursion, which is the one we normally think about.  You start with solving the simple case and then work your way up to the full solution.

The second is top down recursion, which is a bit more complicated.  You need to divide the full case to sub problems.

Dynamic programming is a powerful way to solve problems.  There was a time when I was very good at it.

The example of dynamic programming provided by the book is the Fibonnaci sequence.

```java
public int fib(int i)
{
	if(i==0)
	{
		return 0;
	}
	if(i==1)
	{
		return 1;
	}
	return fib(i-1) + fib(i-2);
}
```

A big difficulty with dynamic programming is runtime analysis.  

For example, see that for this Fibonnaci sequence has a very bad time complexity of O(2<sup>n</sup>).

Here is an easy way to speed it up.

```java
int[] fib = new int[max];

int fibonnaci(int i)
{
  if (i == 0)
  {
    return 0;
  }
  if(i==1)
  {
    return 1;
  }
  if(fib[i]!=0)
  {
    return fib[i];
  }
  fib[i] = fibonnaci(i-1)+fibonnaci(i-2);
  return fib[i];
}
```

This allows us to cache the results and get O(n) time.

### Recursive vs Iterative

Recursion is slow.  Remember that.
