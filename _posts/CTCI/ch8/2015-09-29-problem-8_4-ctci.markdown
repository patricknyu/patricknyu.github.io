---
layout: post
title: "Problem 8_4[CTCI]"
modified:
categories: /ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-09-29T11:39:07-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_8/8_4)

###Q:
Design a parking lot using object-oriented principles

###A:
I'm going to think of this as a parking structure with many levels.

I'll represent it as a 2d array.  I need a class for the structure, a class for cars, and a class for spaces.

[Car.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_4/Car.java)

```java
public class Car
{
	private String make;
	private String model;
	private int year;
	public boolean parked;

	public Car(String ma,String mo, int y, boolean p)
	{
		make = ma;
		model = mo;
		year = y;
		parked = p;
	}

	public int getYear()
	{
		return year;
	}
	public String getMake()
	{
		return make;
	}
	public String getModel()
	{
		return model;
	}
	public void message()
	{
		System.out.println("This is a " + make + model + " from " + year);
	}

}
```

[Spot.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_4/Spot.java)

```java
public class Spot
{
	public boolean hasCar;
	public Car currentCar;

	public Spot(Car c, boolean in)
	{
		currentCar = c;
		hasCar = in;
	}

	public Car getCar()
	{
		return currentCar;
	}
}
```

[ParkingStructure.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_4/ParkingStructure.java)

```java
public class ParkingStructure
{
	public int levels;
	public int spotsPerLevel;
	public Car[][] struct;

	public ParkingStructure(int l, int spl)
	{
		struct = new Car[l][spl];
	}
	//returns false if car is there	
	public boolean insertCar(Car c, int level, int spot)
	{
		if(struct[level][spot] == null)
		{
			struct[level][spot] = c;
			c.message();
			return true;
		}
		else
		{
			return false;
		}
	}
}
```