---
layout: post
title: "Problem 7_1[CTCI]"
modified:
categories: CTCI
excerpt:
tags: [coding,ctci]
image:
  feature:
date: 2015-09-23T22:47:43-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_7/7_1)

###Q:
You have a basketball hoop and someone says that you can play one of two games.

Game 1: You get one shot to make the hoop.
Game 2: You get three shots and you have to make two of three shots.

If p is the probability of making a particular shot, for which values of p should you pick one game or the other?

###A:
Let A be the even that you win game 1.  Let B be the event where you win game 2.

By definition, we know that:

P(A) = p

There are three ways two get 2 in while missing one (TTF,TFT,FTT) and one way to get three in (TTT), so we get

P(B) = 3p<sup>2</sup>(1-p) + p<sup>3</sup> = 3p<sup>2</sup> - 3p<sup>3</sup> + p<sup>3</sup> = 3p<sup>2</sup> - 2p<sup>3</sup>

Now when we compare P(A) and P(B), we see that we play game 1 when:

P(A) > P(B)

p > 3p<sup>2</sup> - 2p<sup>3</sup>

1 > 3p - 2p<sup>2</sup>

We factor and get

(2p-1)(p-1)>0

Since p < 1, we know that p - 1 < 0.

That means that in order to keep this positive, we must keep 2p-1 negative as well.

2p-1 < 0

p < .5

So we play game 1 when p < .5.  We also see that when p = 0,.5,1 P(A) = P(B).  When p > .5, we choose game 2.