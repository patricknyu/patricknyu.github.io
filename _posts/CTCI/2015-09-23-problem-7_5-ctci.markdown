---
layout: post
title: "Problem 7_5[CTCI]"
modified:
categories: CTCI
excerpt:
tags: [coding, ctci]
image:
  feature:
date: 2015-09-23T22:54:11-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_7/7_5)

###Q:
Given two squares on a two-dimensional plane, find a line that would cut these two squares in half. Assume that the top and the bottom sides of the square run parallel to the x-axis.

###A:
So what we have to do is is find the middle point of both squares.  We know that in order for our line to cut both squares in half, the line would have to go through the middle point of each square.

Finding the middle should be easy given the corners of the squares as (x,y) coordinates.  Given one middle point as (x1,y1) and (x2,y2), we can apply this to the points y - y1 = (y2-y1)/(x2-x1)*(x-x1).  This should give us the line.
