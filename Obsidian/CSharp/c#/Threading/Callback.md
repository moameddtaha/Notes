---
tags:
  - Threading
---

# Callback
---

![[Tasks/img/27.png]]

![[Tasks/img/28.png]]

![[Tasks/img/29.png]]
## Example
---

>[!info]- Alternative way (Old)
> ```CSharp
> // Create callback method
> Action/<long/> callback = (sum) =>
> {
> 	Console.WriteLine($"Return value from Count Up Thread is {sum}");
> };
> // Create first thread
> ThreadStart threadStart1 = new ThreadStart(() =>
> {
> 	numbersUpCounter.CountUp(callback);
> });
> ```


```CSharp
using System;
using System.Threading;
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
			Console.ForegroundColor = ConsoleColor.Green;
			Console.Write($"i = {i}, ");
			Thread.Sleep(100); // In milliseconds
		}
		
		Thread.Sleep(1000);
		Console.WriteLine(" \n Count up method completed");
		
		callback(sum);
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
	
		// Join
		
		thread1.Join();
		thread2.Join();
	}
}
```








