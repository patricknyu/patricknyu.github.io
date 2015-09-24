---
layout: post
title: "Problem 7_4[CTCI]"
modified:
categories: CTCI
excerpt:
tags: [coding, ctci]
image:
  feature:
date: 2015-09-23T22:50:43-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_7/7_4)

###Q:
Write methods to implement the multiply, subtact, and divide operations for the integers.  Use only the add operator.

###A:
This is actually more difficult than I originally thought!

I included some basic tests that I did.

```java
public class operations
{
	public int multiply(int a,int b)
	{
		if(a<b)
		{
			return multiply(b,a);
		}
		int sum = 0;
		int count = 0;
		while(count < b)
		{
			sum +=a;
			count++;
		}
		if(b < 0)
		{
			sum = negate(sum);
		}
		return sum;
	}
	//Subtract will require a negate helper method

	public int negate(int a)
	{
		int neg = 0;
		int d;
		if (a < 0)
		{
			d = 1;
		}
		else
		{
			d = -1;
		}
		while (a !=0)
		{
			neg +=d;
			a +=d;
		}
		return neg;
	}
	public int subtract(int a, int b)
	{
		return a + negate(b);
	}
	//This division will be a/b
	//This assumes it is divisible
	public int divide(int a, int b)
	{
		int count = 0;
		int current = 0;
		int absa = abs(a);
		int absb = abs(b);

		while (current+absb<=absa)
		{
			current +=absb;
			count++;
		}
		if (( a<0 && b > 0) || (a > 0 && b <0))
		{
			count = negate(count);
		}
		return count;
	}
	public int abs(int a)
	{
		if (a < 0)
		{
			return negate(a);
		}
		return a;
	}
	public static void main(String args[])
	{
		operations inst = new operations();
		System.out.println("9-3");
		System.out.println(inst.subtract(9,3));
		System.out.println("abs(-9)");
		System.out.println(inst.abs(-9));
		System.out.println("9/3");
		System.out.println(inst.divide(9,3));
		System.out.println("9*3");
		System.out.println(inst.multiply(9,3));
		System.out.println("abs(9)");
		System.out.println("-9");
		System.out.println(inst.negate(9));
	}
}
```