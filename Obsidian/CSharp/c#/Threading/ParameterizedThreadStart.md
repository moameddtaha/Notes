---
tags:
  - Threading
Links:
  - "[[Thread Parameters]]"
  - "[[Custom Thread Object]]"
---

# ParameterizedThreadStart
---

![[Tasks/img/24.png]]

![[Tasks/img/25.png]]

## Example
---

### Pass one argument

```CSharp
using System;
using System.Threading;

class NumbersCounter
{
	public void CountUp(object? count)
	{
		Console.WriteLine("Count up method started");
		Thread.Sleep(100); // In milliseconds
		
		 // i = 1 to 100
		int? countInt = (int?)count;
		for (int i = 1; i <= countInt; i++)
		{
			Console.ForegroundColor = ConsoleColor.Green;
			Console.Write($"i = {i}, ");
			Thread.Sleep(100); // In milliseconds
		}
		
		Thread.Sleep(1000);
		Console.WriteLine(" \n Count up method completed");
	}
}

class Program
{
	static void Main()
	{
		// Note: Console colors may not appear as expected due to parallel execution.
		Thread mainThread = Thread.CurrentThread;
		mainThread.Name = "Main Thread";
		Console.WriteLine(mainThread.Name + " started"); // Main Thread
		NumbersCounter numbersCounter = new NumbersCounter();
		
		// Create first thread
		ParameterizedThreadStart threadStart1 = new ParameterizedThreadStart(numbersCounter.CountUp); // We are gonna pass the parameter when calling the Start() method.
		
		Thread thread1 = new Thread(threadStart1) { Name = "Count up thread", Priority = ThreadPriority.Highest }; // Object initializer
		
		thread1.Start(100); // if no value specified it will pass null.
		
		Console.WriteLine($"{thread1.Name} ({thread1.ManagedThreadId}) is {thread1.ThreadState}"); // Running
		
		
		// Join
		
		thread1.Join();
		thread2.Join();
	}
}
```


### Pass multiple arguments

```CSharp
using System;
using System.Threading;

class MaxCount
{
	public int Count { get; set; }
}

class NumbersCounter
{
	public void CountUp(object? count)
	{
		Console.WriteLine("Count up method started");
		Thread.Sleep(100); // In milliseconds
		
		// i = 1 to 100
		MaxCount? maxCount = (MaxCount?)count;
		if (maxCount == null)
		{
			return;
		}
		
		for (int i = 1; i <= maxCount.Count; i++)
		{
			Console.ForegroundColor = ConsoleColor.Green;
			Console.Write($"i = {i}, ");
			Thread.Sleep(100); // In milliseconds
		}
		
		Thread.Sleep(1000);
		Console.WriteLine(" \n Count up method completed");
	}
}

class Program
{
	static void Main()
	{
		// Note: Console colors may not appear as expected due to parallel execution.
		Thread mainThread = Thread.CurrentThread;
		mainThread.Name = "Main Thread";
		Console.WriteLine(mainThread.Name + " started"); // Main Thread
		
		NumbersCounter numbersCounter = new NumbersCounter();
		
		// Create first thread
		
		ParameterizedThreadStart threadStart1 = new ParameterizedThreadStart(numbersCounter.CountUp); // We are gonna pass the parameter when calling the Start() method.
		
		Thread thread1 = new Thread(threadStart1) { Name = "Count up thread", Priority = ThreadPriority.Highest }; // Object initializer
		
		// Invoke CountUp
		
		MaxCount maxCount1 = new MaxCount() {Count = 100}; // Object initializer
		thread1.Start(maxCount1); // if no value specified it will pass null.
		Console.WriteLine($"{thread1.Name} ({thread1.ManagedThreadId}) is {thread1.ThreadState}"); // Running
		
		// Join
		
		thread1.Join();
		thread2.Join();
	}
}
```








































