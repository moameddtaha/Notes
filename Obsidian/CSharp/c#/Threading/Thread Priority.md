---
tags:
  - Threading
---

# Thread Priority
---

![[Tasks/img/16.png]]

![[Tasks/img/17.png]]

## Example
---

```CSharp
using System;
using System.Threading;

class NumbersCounter
{
	public void CountUp()
	{
		Console.WriteLine("Count up method started");
		Thread.Sleep(100); // In milliseconds
		
		// i = 1 to 100
		for (int i = 1; i <= 100; i++)
		{
		Console.ForegroundColor = ConsoleColor.Green;
		Console.Write($"i = {i}, ");
		Thread.Sleep(100); // In milliseconds
		}
		
		Thread.Sleep(1000);
		Console.WriteLine(" \n Count up method completed");
	}
	
	public void CountDown()
	{
		Console.WriteLine("Count down method started");
		Thread.Sleep(100); // In milliseconds
		
		// i = 100 to 1
		for (int j = 100; j >= 1; j--)
		{
			Console.ForegroundColor = ConsoleColor.Red;
			Console.Write($"j = {j}, ");
			Thread.Sleep(100); // In milliseconds
		}
		
		Thread.Sleep(1000);
		Console.WriteLine(" \n Count down method completed");
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
		
		// Create a thread
		ThreadStart threadStart1 = new ThreadStart(numbersCounter.CountUp);
		Thread thread1 = new Thread(threadStart1) { Name = "Count up thread", Priority = ThreadPriority.Highest }; // Object initializer
		thread1.Start();
		Console.WriteLine($"{thread1.Name} ({thread1.ManagedThreadId}) is {thread1.ThreadState}"); // Running
		
		ThreadStart threadStart2 = new ThreadStart(numbersCounter.CountDown);
		Thread thread2 = new Thread(threadStart2) { Name = "Count down thread", Priority = ThreadPriority.BelowNormal }; // Object initializer
		thread2.Start();
		Console.WriteLine($"{thread2.Name} ({thread2.ManagedThreadId}) is {thread2.ThreadState}"); // Running
		
		// Join
		thread1.Join();
		thread2.Join();
		
		Console.WriteLine(mainThread.Name + "Completed");
	}
}
```











































