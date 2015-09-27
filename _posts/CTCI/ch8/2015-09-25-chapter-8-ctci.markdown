---
layout: post
title: "Chapter 8[CTCI]"
modified:
categories: /ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-09-25T16:18:16-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/readme.md)

##Object-Orientated Design

####Steps to Solve

1. Handle Ambiguity
	* OOD questions are intentionally very vague.  It's importatnt to ask questions and not make assumptions.
	* We have to ask who, what when, where, why, and how

2. Define the Core Objects
	* We need to know know what the core objects are.
	* My favorite example in OOD is the restaurant example.  Core objects in this example could be Employee, Food, Customer.

3. Analyze Relationships
	* We need to notice which objects are members of other objects.  Do we have inheritance properties?
	* Do we have many to many or one to many relationship.

Example 1: An example of a one to many relationship is a when we are describing families.  A Mother may have many biological children, however a child can only have one biological mother.

Example 2: An example of a many to many relationship is when we describe books.  A book can be written by many authors as a joint effort.  In a similar light, a author can write many books.

4. Investigate Actions
	* Consider the actions that the objects can take.  You need to double check your program here and ensure you didn't miss anything.

####Singleton Class
- This ensures that a class has only one instance and ensures access to the instance through the application.
- It is useful in cases where you have a global object with only one instance.
- The example below implements the Restaurant class so that there is only one instance of Restaurant allowed.

```java
public class Restaurant
{
	private static restaurant _instance = null;
	protected Restaurant()
	{
	}
	public static Restaurant getInstance()
	{
		if(_instance == null)
		{
			_instance = new Restaurant();
		}
		return _instance;
	}
}
```

####Factory Method
- Offers an interface for creating an instance of a class.
- The sublcasses decide which class to instantiate.
- You can do this with the creator class being abstract, or you could have the creator class be a concrete class that provides an implementation.
- The below example takes a paramter which represents which class we want to instantiate.

```java
public class CardGame
{
	public static CardGame createCardGame(GameType type)
	{
		if(type==GameType.Poker)
		{
			return new PokerGame();
		}
		else if (type == GameType.BlackJack)
		{
			return new BlackJackGame();
		}
		return null;
	}
}
```

####4 Pillars of OOD
1. Abstraction
	* The basic idea behind abstraction is to hide the complexities of your program.  Someone using your design doesn't necessarily need to know all the nitty gritty details behind it.
	* Example : If you have a car, you know that you need keys, how to press the gas pedal, and how to steer.  However, you probably don't need to know how the engine works with the cylinders and the gear change.

2. Encapsulation
	* The idea for this is security.  You can make some of the variables in your design private, allowing to keep some data safe.
	* An example of this is a backpack.  You put your school stuff inside of it and nobody can access it other than you.

3. Polymorphism
	* This is the ability for an object to take many forms.
	* Method overloading goes here.
	* This means that we can have objects with the same name that are different since they have different parameters.

4. Inheritance
	* This is the ability for an object to inherity the qualities of another object.
	* Example : We have a cat object which has properties ```has_claws = true;``` and ```legs = 4;```.  Lion can inherit cat at keep those properties.  Panther can also inherit cat and keep those qualities too.