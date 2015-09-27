---
layout: post
title: "Problem 8_2[CTCI]"
modified:
categories: ctci/ch8
excerpt:
tags: []
image:
  feature:
date: 2015-09-27T15:39:32-07:00
---
[Github Source](https://github.com/patricknyu/CtCInterview/tree/master/ch_8/8_2)

###Q:
Imagine you have a call center with three levels of employees: respondent, manager, and director. An incoming telephone call must be first allocated to a respondent who is free. If the respondent can't handle the call, he or she must escalate the call to a manager. If the manager is not free or not able to handle it, then the call should be escalated to a director. Design the classes and data structures for thisproblem. Implement a method dispatchCall() which assigns a call to the first available employee.

###A:
I want to create a class for employees.  Then we have a respondent class which extends employee, a manager class which extends respondent, and a director class which extends manager. 

Their solution was a way better than mine. They have a Call, Rank, and CallHandler class in addition to the one's I suggested.

The call and rank classes are pretty cool.  The rank class uses the enum feature.  The CallHandler is where most of the stuff runs.  It works well.

I'm going to recreate some of them since I liked their solution so much.


[Call.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/Call.java)

```java
public class Call
{
	//This decides the minimal rank of the employee.
	private Rank rank;

	//This tells me who is calling
	private Caller caller;

	//This tells me which employee is taking care of the call.
	private Employee handler;

	public Call(Caller c)
	{
		//This just puts the rank as the lowest rank we have.
		rank = Rank.Respondent;
		//Sets the caller as the inputed c
		caller = c;
	}
	
	//Sets handler to imputed employee.
	public void SetHandler(Employee e)
	{
		handler = e;
	}

	//How to talk to the customer
	public void reply(String message)
	{
		System.out.println(message);
	}

	//returns the call's lowest rank
	public Rank getRank()
	{
		return rank;
	}
	
	//changes the rank
	public void setRank(Rank r)
	{
		rank = r;
	}

	public Rank incrementRank()
	{
		if (rank == Rank.Respondent)
		{
			rank = Rank.Manager;
		}
		else if(rank == Rank.Manager)
		{
			rank = Rank.Director;
		}
		return rank;
	}

	//Ends the call
	public void disconnect()
	{
		reply("Bye");
	}
}
```

[Rank.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/Rank.java)

```java
//Uses enum
public enum Rank
{
	Respondent (0),
	Manager (1),
	Director (2);

	private int value;

	Rank(int v)
	{
		value = v;
	}

	public int getValue()
	{
		return value;
	}
}
```

[Caller.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/Caller.java)

```java
public class Caller{
	private String name;
	private int userId;
	public Caller(int id,String nm)
	{
		name = nm;
		userId = id;
	}
}
```

[Employee.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/Employee.java)

```java
abstract class Employee
{
	private Call currentCall = null;
	protected Rank rank;

	public Employee()
	{
	}

	public Rank getRank()
	{
		return rank;
	}

	public void receiveCall(Call call)
	{
		currentCall = call;
	}

	public boolean isFree()
	{
		return (currentCall == null);
	}

	public boolean assignNewCall()
	{
		if(isFree())
		{
			return false;
		}
		return CallHandler.getInstance().assignCall(this);
	}

	public void escalateAndResassign()
	{
		if(currentCall !=null)
		{
			currentCall.incrementRank();
			CallHandler.getInstance().dispatchCall(currentCall);

			currentCall = null;
		}
		assignNewCall();
	}

	public void CallCompleted()
	{
		if(currentCall != null)
		{
			currentCall.disconnect();
			currentCall = null;
		}
		assignNewCall();
	}
}
```

[Respondent.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/Respondent.java)

```java
public class Respondent extends Employee
{
	public Respondent()
	{
		rank = Rank.Respondent;
	}
}
```

[Manager.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/Manager.java)

```java
public class Manager extends Employee
{
	public Manager()
	{
		rank = Rank.Manager;
	}
}
```

[Director.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/Director.java)

```java
public class Director extends Employee
{
	public Director()
	{
		rank = Rank.Director;
	}
}
```

[CallHandler.java](https://github.com/patricknyu/CtCInterview/blob/master/ch_8/8_2/CallHanlder.java)

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

//We are going to define this as a singleton class
public class CallHandler
{
	public static CallHandler instance;
	
	//only 3 levels
	private final int LEVELS = 3;

	//Giving 10 respondents, 4 managers, and 2 directors
	private final int NUM_RESPONDENTS = 10;
	private final int NUM_MANAGERS = 4;
	private final int NUM_DIRECTORS = 2;

	List<List<Employee>> employeeLevels;

	List<List<Call>> callQueues;

	protected CallHandler()
	{
		employeeLevels = new ArrayList<List<Employee>>(LEVELS);
		callQueues = new ArrayList<List<Call>>();
	
		//Create 10 respondents
		ArrayList<Employee> respondents = new ArrayList<Employee>(NUM_RESPONDENTS);
		for (int i = 0;i<NUM_RESPONDENTS-1;i++)
		{
			respondents.add(new Respondent());
		}
		employeeLevels.add(respondents);

		//Create 4 managers
		ArrayList<Employee> managers = new ArrayList<Employee>(NUM_MANAGERS);
		for (int i = 0;i<NUM_MANAGERS-1;i++)
		{
			managers.add(new Manager());
		}
		employeeLevels.add(managers);
		
		//Create 2 directors
		ArrayList<Employee> directors = new ArrayList<Employee>(NUM_DIRECTORS);
		for (int i = 0;i<NUM_DIRECTORS-1;i++)
		{
			directors.add(new Director());
		}
		employeeLevels.add(directors);

	}

	//Instance of singleton class
	public static CallHandler getInstance()
	{
		if (instance == null)
		{
			instance = new CallHandler();
		}
		return instance;
	}

	//Gives the first available employee at the lowest level
	public Employee getHandlerForCall(Call call)
	{
		//Goes level by level
		for(int level = call.getRank().getValue(); level < LEVELS-1;level++)
		{
			//List of employees at the current level
			List<Employee> employeeLevel = employeeLevels.get(level);
			//Iterate through employees at this level
			for(Employee e: employeeLevel)
			{
				//Use previously created isFree() method.
				if(e.isFree())
				{
					return e;
				}
			}
		}
		return null;
	}
	//This is in case they input a caller
	public void dispatchCall(Caller caller)
	{
		Call call = new Call(caller);
		dispatchCall(call);
	}

	//dispatchCall will either find a available employee and give them the call or add the call to the queue.
	public void dispatchCall(Call call)
	{
		//From earlier in this program
		Employee e = getHandlerForCall(call);
		if(e != null)
		{
			//written in the employee class.
			e.receiveCall(call);
			//written in the call class.
			call.SetHandler(e);
		}
		else
		{
			call.reply("Waiting Tune -- Probably elevator music");
			//Adds the call the necessary ranked queue.
			callQueues.get(call.getRank().getValue()).add(call);
		}
	}
	
	//We use this if a employee is newly free and we need to reassign them.
	public boolean assignCall(Employee e)
	{
		for(int rank = e.getRank().getValue();rank >=0;rank--)
		{
			//Gets the calls of the current rank
			List<Call> queue = callQueues.get(rank);
			if(queue.size()>0)
			{
				Call call = queue.remove(0);
				if (call != null)
				{
					e.receiveCall(call);
					return true;
				}
			}
		}
		return false;
	}
}
```