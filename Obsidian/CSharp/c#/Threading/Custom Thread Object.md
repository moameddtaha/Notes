---
tags:
  - Threading
Links:
  - "[[Thread Parameters]]"
  - "[[ParameterizedThreadStart]]"
---

# Custom Thread Object
---

![[Tasks/img/26.png]]

## Example
---

```CSharp
using System;
using System.Threading;

class NumbersUpCounter
{
	public int Count { get; set; }
	public void CountUp()
	{
		Console.WriteLine("Count up method started");
		Thread.Sleep(100); // In milliseconds
		
		// i = 1 to 100
		for (int i = 1; i <= Count; i++)
		{
			Console.ForegroundColor = ConsoleColor.Green;
			Console.Write($"i = {i}, ");
			Thread.Sleep(100); // In milliseconds
		}
		
		Thread.Sleep(1000);
		Console.WriteLine(" \n Count up method completed");
	}
}

class NumbersDownCounter
{
	public int Count { get; set; }
	public void CountDown()
	{
		Console.WriteLine("Count down method started");
		Thread.Sleep(100); // In milliseconds
		
		// i = 100 to 1
		for (int? j = Count; j >= 1; j--)
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
		
		// Create first thread
		NumbersUpCounter numbersUpCounter = new NumbersUpCounter() {Count = 100};
		
		ThreadStart threadStart1 = new ThreadStart(numbersUpCounter.CountUp);
		
		Thread thread1 = new Thread(threadStart1) { Name = "Count up thread", Priority = ThreadPriority.Highest }; // Object initializer
		
		// Invoke CountUp
		thread1.Start(); // if no value specified it will pass null.
		Console.WriteLine($"{thread1.Name} ({thread1.ManagedThreadId}) is {thread1.ThreadState}"); // Running
		
		// Create second thread
		NumbersDownCounter numbersDownCounter = new NumbersDownCounter() {Count = 100};
		
		ThreadStart threadStart2 = new ThreadStart(numbersDownCounter.CountDown);
		
		Thread thread2 = new Thread(threadStart2) { Name = "Count down thread", Priority = ThreadPriority.BelowNormal };
		
		// Invoke CountDown
		thread2.Start();
		Console.WriteLine($"{thread2.Name} ({thread2.ManagedThreadId}) is {thread2.ThreadState}"); // Running
		
		// Join
		
		thread1.Join();
		thread2.Join();
	}
}
```


























