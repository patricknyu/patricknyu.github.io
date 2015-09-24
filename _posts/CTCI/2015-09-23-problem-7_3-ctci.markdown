---
layout: post
title: "Problem 7_3[CTCI]"
modified:
categories: CTCI
excerpt:
tags: [coding, ctci]
image:
  feature:
date: 2015-09-23T22:50:03-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_7/7_3)

###Q:
Given two lines on a Cartesian plane, determine whether the two lines would intersect.

###A:
Mathematically, two lines, by the true definition of a line, would always intersect unless their slopes were the same and their y-intercept were different.

The solution provided by the book involves creating a line class.  It seems to be just an example question to show how to ask questions.

I'll replicate the line class here.

```java
public class Line
{
	static double epsilon = 0.000001;
	public double slope;
	public doulbe yintercept;

	public Line(double s, double y)
	{
		slope = s;
		yintercept = y;
	}

	public boolean intersect(Line line2)
	{
		return Math.abs(slope-line2.slope)>epsilon || Math.abs(yintercept - line2.intercept)<epsilon;
	}
}
```

Personally, my intercept method would look a little different.

```java
public boolean intersect2(Line line2)
{
	if(Math.abs(slope-line2.slope)<epsilon && Math.abs(yintercept - line2.yintercept) >epsilon)
	{
		return true;
	}
	return false;
}
```


