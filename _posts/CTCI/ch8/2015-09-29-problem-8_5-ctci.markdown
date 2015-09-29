---
layout: post
title: "Problem 8_5[CTCI]"
modified:
categories: ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-09-29T15:58:43-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_8/8_5)

###Q:
Design the data structures for an online book system.

###A:
This is a pretty vague description of a book system.  With all other OOD questions, we must ensure we ask enough questions to properly understand what we are asked to accomplish.

I'm going to assume this is a reader system which similar to a kindle, but is on a computer.

I'm going to create a Book, Kindle, and Library class.

[Book.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_5/Book.java)

```java
public class Book
{
	private int id;
	private String Author;
	private String Title;
	private String text;

	public Book(int i, String a, String ti, String te)
	{
		id = i;
		Author = a;
		Title = ti;
		text = te;
	}

	public int getID()
	{
		return id;
	}
	public void setID(int i)
	{
		id = i;
	}
	public String getAuthor()
	{
		return Author;
	}
	public void setAuthor(String a)
	{
		Author = a;
	}
	public String getTitle()
	{
		return Title;
	}
	public void setTitle(String ti)
	{
		Title = ti;
	}
	public String getText()
	{
		return text;
	}
	public void setText(String te)
	{
		text = te;
	}
}
```

[Library.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_5/Library.java)

```java
import java.util.Hashtable;

public class Library
{
	//Where we hold the books, book id will be the integer
	private Hashtable<Integer, Book> lib;

	//Adding books to our library
	public void addBook(Book b)
	{
		if(lib.containsKey(b.getID()))
		{
			System.out.println("We already have this book");
		}
		else
		{
			lib.put(b.getID(),b);
		}
	}

	//Getting rid of books from our library
	public void removeBook(Book b)
	{
		if(lib.containsKey(b.getID()))
		{
			lib.remove(b.getID());
		}
		else
		{
			System.out.println("We don't have this book.");
		}
	}
	
	//Grabbing books from our library.
	public Book get(Book b)
	{
		if(!lib.containsKey(b.getID()))
		{
			System.out.println("We don't have this book.");
		}
		else
		{
			return lib.get(b.getID());
		}
		return null;
	}
	public boolean containsBook(Book b)
	{
		return lib.containsKey(b.getID());
	}
}
```

[Kindle.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_5/Kindle.java)

```java
public class Kindle
{
	private int storage;
	private Library lib;
	private String username;
	private Book currentBook;

	public Kindle(String u, int s, Library l)
	{
		storage = s;
		username = u;
		lib = l;
	}

	public int getStorageSize()
	{
		return storage;
	}

	public String getUser()
	{
		return username;
	}

	public Book getCurrentBook()
	{
		return currentBook;
	}
	public void readBook(Book b)
	{
		if(currentBook != null)
		{
			System.out.println("You're already reading something else!  Finish that first!");
		}

		if (!lib.containsBook(b))
		{
			System.out.println("We don't have this book to read");
		}

		currentBook = b;
	}
	
	//There is probably a better way to implement this part.
	public void stopReading()
	{
		currentBook = null;
	}
}
```