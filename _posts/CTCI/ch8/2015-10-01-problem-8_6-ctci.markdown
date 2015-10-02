---
layout: post
title: "Problem 8_6[CTCI]"
modified:
categories: ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-10-01T20:00:47-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_8/8_6)
###Q:
Implement a jigsaw puzzle.  Design the data structures and explain an algorithm to solve the puzzle.  You can assume that you have a fitsWith method which, when passed two puzzle pieces, returns true if the two pieces belong together.

###A:
This is a difficult problem.  My general idea was to use a boolean n dimensional array to represent the board.  My implementation was simplistic, so I will use theirs.

They use the idea of absolute position along with relative position.  Absolute position refers to when we know exactly where our piece goes.  Relative positions is ues to know it is next to another piece.

This is a really tough problem.  I'll replicate most of the code.

[Edge.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_6/Edge.java)

```java
public class Edge
{
	public enum Type
	{
		inner, outer, flat
	}
	Piece parent;
	Type type;
	int index;
	Edge attached_to;

	public boolean fitsWidth(Edge edge)
	{
		return false;
	}
}
```

[Piece.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_6/Piece.java)

```java
public class Piece
{
	Edge[] edges;
	public boolean isCorner()
	{
		return false;
	}
}
```

[Puzzle.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_6/Puzzle.java)

```java
public class Puzzle
{
	Piece[] pieces;
	Piece[][] solutions;
	
	//The three types of pieces.
	Edge[] inners, outers, flats;
	Piece[] corners;

	//Start with the edges
	public void sort()
	{
		for each Piece p in pieces
		{
			if (//p has two flat edges)
			{
				//add p to corners
			}
			for each edge in p.edges
			{
				if (//edge is an inner edge)
				{
					//add to inners
				}
				if (//edge is an outer edge)
				{
					//add to outers
				}
			}
	}

	//We want to start with a corner.  Then we find an open edge on the corner and try to match it with an open piece.  Once finding the match, we attach the edge, remove the edge from our list of edges and find the next open edge.

	//The next open edge refers to the one that is directly opposite our current edge, given that is available.  If it is not available, then the next edge can be any edge.  This makes a spiral.
	public void solve()
	{
		Edge currentEdge = getExposedEdge(corner[0]);

		while (currentEdge != null)
		{
			//Get opposites
			Edge[] oppoisites = currentEdge.type == inner? outers : inners;
			//Loop through opposites
			for each Edge fittingEdge in opposites
			{
				//If the opposite fits
				if (currentEdge.fitsWith(fittingEdge))
				{
					attachEdges(currentEdge, fittingEdge);
					removeFromList(currentEdge);
					removeFromList(fittingEdge);
					currentEdge = nextExposedEdge(fittingEdge);
					break;
				}
			}
		}
	}
	public void removeFromList(Edge edge)
	{
		//We don't deal with flats
		if(edge.type == flat)
		{
			return;
		}
		//Chooses which list to remove from
		Edge array[] = (currentEdge.type == inner) ? inners : outers;
		array.remove(edge);
	}
	
	//This will get the opposite edge if it is expose, if not it will just get the next exposed one.
	public Edge nextExposedEdge(Edge edge)
	{
		int edge_idx = (edge.index + 2)%4;
		Edge next_edge = edge.parent.edges[edge_idx];
		if(isExposed(next_edge))
		{
			return next_edge;
		}
		return getExposedEdge(edge.parent);
	}
	
	public void attechEdges(Edge e1, Edge e2)
	{
		e1.attached_to(e2);
		e2.attached_to(e1);
	}
	

	//An exposed edge occurs when we don't have a flat edge and it is attached to nothing.
	public boolean isExposed(Edge edge)
	{
		return (edge.type != flat) && (edge.attached_to == null);
	}

	public Edge getExposedEdge(Piece p)
	{
		//loop to find next exposed edge
		for each Edge edge in p.edges
		{
			if(isExposed(edge))
			{
				retun edge;
			}
		}
		return null;
	}
}
```

