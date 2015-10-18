---
layout: post
title: "Problem 8_9[CTCI]"
modified:
categories: /ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-10-16T16:03:59-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_8/8_9)

###Q:
Explain the data structures and algorithms that you would use to design an in-memory file system. Illustrate with an example in code where possible.

###A:
Basically, we need a file class and a directory class where one directory class can contain other directory classes.

The given solution uses a class called Entry which we inherit properties from.


[Directory.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_9/Directory.java)

```java
import java.util.ArrayList;
public class Directory extends Entry
{
	protected ArrayList<Entry> contents;

	public Directory(String n, Directory p)
	{
		super(n,p);
		contents = new ArrayList<Entry>();
	}

	public int size()
	{
		//Must do this since directories can contain directories.
		int size = 0;
		for (Entry e: contents)
		{
			size +=e.size();
		}
		return size;
	}
	public int numberOfFiles()
	{
		int count = 0;
		for (Entry e : contents)
		{
			if (e instanceof Directory)
			{
				count++;
				Directory d = (Directory) e;
				count+=d.numberOfFiles();
			}
			else if(e instanceof File)
			{
				count++;
			}
		}
		return count;
	}
	public boolean deleteEntry(Entry e)
	{
		return contents.remove(e);
	}
	public void addEntry(Entry e)
	{
		contents.add(e);
	}
	protected ArrayList<Entry> getContents()
	{
		return contents;
	}
}
```

[Entry.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_9/Entry.java)

```java
public abstract class Entry
{
	protected Directory parent;
	protected long created;
	protected long lastUpdated;
	protected long lastAccessed;
	protected String name;

	public Entry(String n, Directory p)
	{
		name = n;
		parent = p;
		created = System.currentTimeMillis();
		lastUpdated = System.currentTimeMillis();
		lastAccessed = System.currentTimeMillis();
	}

	public boolean delete()
	{
		if(parent == null)
		{
			return false;
		}
		return parent.deleteEntry(this);
	}
	public abstract int size();
	public String getFullPath()
	{
		if(parent == null)
		{
			return name;
		}
		return parent.getFullPath() + "/" + name;
	}

	public long getCreationTime()
	{
		return created;
	}
	public long getLastUpdatedTime()
	{
		return lastUpdated;
	}
	public long getLastAccessedTime()
	{
		return lastAccessed;
	}
	public void changeName(String n)
	{
		name = n;
	}
	public String getName()
	{
		return name;
	}
}
```

[File.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_8/File.java)

```java
public class File extends Entry
{
	private String content;
	private int size;

	public File(String n,Directory p, int s)
	{
		super(n,p);
		size = s;
	}

	public int size()
	{
		return size;
	}
	public String getContent()
	{
		return content;
	}
	public void setContents(String c)
	{
		content = c;
	}
}
```