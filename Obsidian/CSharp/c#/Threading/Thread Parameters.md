---
tags:
  - Threading
Links:
  - "[[ParameterizedThreadStart]]"
  - "[[Custom Thread Object]]"
---

# Thread Parameters
---

![[Tasks/img/23.png]]

## Example
---

```CSharp
using System;
using System.Threading;

class NumbersCounter
{
	public void CountUp(int count)
	{
		Console.WriteLine("Count up method started");
		Thread.Sleep(100); // In milliseconds
		
		for (int i = 1; i <= count; i++)
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
		ThreadStart threadStart1 = new ThreadStart(() =>
		{
			numbersCounter.CountUp(100);
		});
		
		Thread thread1 = new Thread(threadStart1) { Name = "Count up thread", Priority = ThreadPriority.Highest }; // Object initializer
		thread1.Start();
		Console.WriteLine($"{thread1.Name} ({thread1.ManagedThreadId}) is {thread1.ThreadState}"); // Running
		
		
		// Join
		
		thread1.Join();
		thread2.Join();
	}
}
```



























