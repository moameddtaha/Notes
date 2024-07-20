---
tags:
  - Threading
  - Shared-Resources
  - asynchronous
---

# Shared Resources
---

![[Tasks/img/30.png]]

![[34.png]]

![[Tasks/img/32.png]]

![[Tasks/img/33.png]]

![[35.png]]

![[36.png]]

![[37.png]]

## Example
---

> [!warning] Race Condition
> In the code below, a race condition occurs.

```CSharp
using System;
using System.Threading;

class Shared
{
	public static int SharedResource { get; set; } = 0;
}

class NumbersUpCounter
{
	public int Count { get; set; }
	
	public void CountUp(Action<long> callback)
	{
		long sum = 0;
		
		Console.WriteLine("Count up method started");
		
		Thread.Sleep(100); // In milliseconds
		
		// i = 1 to 100
		
		for (int i = 1; i <= Count; i++)
		{
			sum += i;
			Console.Write($"\n Shared Resource in Count Up: {Shared.SharedResource} ");
			Shared.SharedResource++;
			Console.ForegroundColor = ConsoleColor.Green;
			Console.Write($"i = {i}, ");
			Thread.Sleep(100); // In milliseconds
		}
		Thread.Sleep(1000);
		Console.WriteLine(" \n Count up method completed");
		callback(sum);
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
			Console.Write($"\n Shared Resource in Count Down: {Shared.SharedResource} ");
			Shared.SharedResource--;
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
	
	// Object of NumberUpCounter
	NumbersUpCounter numbersUpCounter = new NumbersUpCounter() { Count = 100 };
	
	// Create first thread
	ThreadStart threadStart1 = new ThreadStart(() =>
	{
		numbersUpCounter.CountUp((sum) =>
		{
		
			Console.WriteLine($"Return value from Count Up Thread is {sum}");
		
		});
	});
	
	Thread thread1 = new Thread(threadStart1) { Name = "Count up thread", Priority = ThreadPriority.Highest }; // Object initializer
	
	// Invoke CountUp
	
	thread1.Start(); // if no value specified it will pass null.
	
	Console.WriteLine($"{thread1.Name} ({thread1.ManagedThreadId}) is {thread1.ThreadState}"); // Running
	
	// Create second thread
	
	NumbersDownCounter numbersDownCounter = new NumbersDownCounter() { Count = 100 };
	
	ThreadStart threadStart2 = new ThreadStart(numbersDownCounter.CountDown);
	
	Thread thread2 = new Thread(threadStart2) { Name = "Count down thread", Priority = ThreadPriority.BelowNormal };
	
	// Invoke CountDown
	
	thread2.Start();
	
	Console.WriteLine($"{thread2.Name} ({thread2.ManagedThreadId}) is {thread2.ThreadState}"); // Running
	
	// Join
	
	thread1.Join();
	thread2.Join();
	
	Console.WriteLine($"\n Shared Resource: {Shared.SharedResource}"); // Expected 0
	
	Console.WriteLine(mainThread.Name + "Completed");
	
	}
}
```













