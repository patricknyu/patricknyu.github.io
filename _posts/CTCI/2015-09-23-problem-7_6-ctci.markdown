---
layout: post
title: "Problem 7_6[CTCI]"
modified:
categories: CTCI
excerpt:
tags: [coding, ctci]
image:
  feature:
date: 2015-09-23T22:54:44-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_7/7_6)

###Q:
Given a two-dimensional graph with points on it, find a line which passes the most number of points.

###A:
Apparently the best solution runs in O(n<sup>2</sup>) time.  What you need to do is to create a line segment from each of the n points to every other point.  Then you iterate through the points and find out the line that gives the most collisions using a hashtable. However, there is an issue here with the fact that floating points cannot be represented in binary.  That means we will have to use a epsilon to check equality.  We need a method to round our slope down to the nearest epsilon then compare the slope, slope + epsilon , and slope - epsilon.

###Line Class
```java
public class Line
{
	//The epsilon we choose
	public static double epsilon = .0001;
	public double slope, intercept;
	//Infinite slope boolean
	private boolean infinite_slope = false;

	public Line(Graphpoint p, Graphpoint q)
	{
		//This is if the slope is the same.
		if (Math.abs(p.x-q.x) > epsilon)
		{
			slope = (p.y-q.y)/(p.x-q.x);
			intercept = p.y - slope*p.x;
		}
		//if the slope is different
		else
		{
			infinite_slope = true;
			intercept = p.x;
		}
	}
	//Floor function
	public static double floorToNearestEpsilon(double d)
	{
		int r = (int) (d/epsilon);
		return ((double r) * epsilon;
	}
	//Equivalent
	public boolean isEquivalent(double a, double b)
	{
		return (Math.abs(a-b)<epsilon);
	}
	
	//Line equivalency --I don't think that's a word.
	public boolean isEquivalent(Object o)
	{
		Line l = (Line) o;
		if (isEquaivalent(l.slope,slope) && isEquivalent(l.intercept,intercept) && (infinite_slope == l.infinite_slope))
		{
			return true;
		}
		return false;
	}
}
```
###Some Line Methods
```java
public class LineMethods
{
	public Line findBestLine(GraphPoint[] points)
	{
		Line bestLine = null;
		int bestCount = 0;
		HashMap<Double, ArrayList<Line>> linesBySlope = new HashMap<Double,ArrayList<Line>>();

		for (int i = 0; i < points.length;i++)
		{
			for (int j = 0;j < points.length;i++)
			{
				Line line = new Line(points[i],points[j]);
				insertLine(linesBySlope,line);
				int count = countEquivalentLines(linesBySlope,line);
				if (count > bestCount)
				{
					bestLine = line;
					bestCount = count;
				}
			}
		}
		return bestLine;
	}

	public int countEquivalentLines(ArrayList<Line> lines, Line line)
	{
		if (lines == null)
		{
			return 0;
		}
		int count = 0;
		for( Line parallelLine : lines)
		{
			if(parrallelLine.isEquivalent(line))
			{
				count++;
			}
		}
		return count;
	}

	public int countEquivalentLines(HashMap<Double, ArrayList<Line>> linesBySlope, Line line)
	{
		double key = Line.floorToNearestEpsilon(line.slope);
		double eps = Line.epsilon;
		int count = countEquivalentLines(linesBySlope.get(key),line) + countEquivalentLines(linesBySlope.get(key-eps),line) + countEquivalentLines(linesBySlope.get(key+eps),line);
		return count;
	}
	public void insertLine(HashMap<Double,ArrayList<Line>> linesBySlope, Line line)
	{
		ArrayList<Line> lines = null;
		double key = Line.floorToNearestEpsilon(line.slope);
		if(!linesBySlope.containsKey(key))
		{
			lines = new ArrayList<Line>();
			linesBySlope.put(key,lines);
		}
		else
		{
			lines = linesBySlope.get(key);
		}
		lines.add(line);
	}
}
```