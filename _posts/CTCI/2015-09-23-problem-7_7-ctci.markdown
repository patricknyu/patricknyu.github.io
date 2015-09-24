---
layout: post
title: "Problem 7_7[CTCI]"
modified:
categories: CTCI
excerpt:
tags: [coding, ctci]
image:
  feature:
date: 2015-09-23T22:56:05-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_7/7_7)

###Q:
Design an algorithm to find the kth number such that the only prime factors are 3, 5, and 7.

###A:
This is a pretty difficult problem, especially if you're going for the optimal solution.

####Solution 1
Brute force.  We can multiply each number in a list of k-1 numbers by 3, 5, and 7 until we find the smallest number that is not already in the k-1 list.

####Solution 2
Each time we add a number to our list, we keep in mind 3, 5, and 7 multiplied by that number into a temporary list.

```java
public class getKthMagicNumber{
	//This helper method will remove and return the smallest value of the queue.
	public static int removeMin(Queue<Integer> q)
	{
		int min = q.peek();
		for (Integer v :q)
		{
			if (min > v) min = v;
		}
		while(q.contains(min))
		{
			q.remove(min);
		}
		return min;
	}

	public static void addProducts(Queue<Integer q, int v)
	{
		q.add(v*3);
		q.add(v*5);
		q.add(v*7);
	}

	public static int getKthMagicNumber(int k)
	{
		if (k < 0) return 0;

		int val = 1;
		Queue<Integer> q = new LinkedList<Integer>();
		addProducts(q,1);
		for(int i = 0; i < k;i++)
		{
			val = removeMin(q);
			addProducts(q,val);
		}
		return val;
	}
}
```

####Solution 3
This is the most optimal.  It involves three queues which took the numbers previously used multiplied by 3,5, and 7 respectively and not using duplicates.  We do this till we get our k numbers.

```java
public class getKthMagicNumberFaster
{
	public static int getKthMagicNumberFaster(int k)
	{
		if (k < 0) return 0;

		int val = 0;
		// Three queues for each set of multiples
		Queue<Integer> q3 = new LinkedList<Integer>();
		Queue<Integer> q5 = new LinkedList<Integer>();
		Queue<Integer> q7 = new LinkedList<Integer>();
		// Start with 3^0 * 5^0 * 7^0
		queue3.add(1);
		
		//Iterate through to find
		for(int i = 0; i < k;i++)
		{
			//Each queue's respective min
			int v3 = q3.size() > 0 ? q3.peek() : Integer.MAX_VALUE;
			int v5 = q5.size() > 0 ? q5.peek() : Integer.MAX_VALUE;
			int v7 = q7.size() > 0 ? q7.peek() : Integer.MAX_VALUE;
			
			//Overall min
			val = Math.min(v3,Math.min(v5,v7));
			if(val == v3)
			{
				q3.remove();
				q3.add(3*val);
				q5.add(5*val);
				q7.add(7*val);
			}
			else if (val == v5)
			{
				q5.remove();
				q5.add(5*val);
				q7.add(7*val);
			}
			else if(val == v7)
			{
				q7.remove();
				q7.add(7*val);
			}
		}
		return val;
	}
}
```
