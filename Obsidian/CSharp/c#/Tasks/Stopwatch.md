---
tags:
  - Classes
  - asynchronous
  - Threading
  - TPL
Links:
  - "[[CountDownEvent]]"
---

# Stopwatch
---

![[Tasks/img/13.png]]

![[Tasks/img/14.png]]

![[Tasks/img/15.png]]

![[Tasks/img/16.png]]

## Example
---

```CSharp
public class UpCounter
{
	public void CountUp(int count)
	{
	
		System.Console.WriteLine("\nCount Up starts");
		
		for (int i = 1; i <= count; i++)
		{
			System.Console.Write($"i= {i}, ");
		}
		
		System.Console.WriteLine("\nCount Up ends");
	
	}
}


public class DownCounter
{

	public void CountDown(int count)
	{
	
		System.Console.WriteLine("\nCount Down starts");
		
		for (int j = count; j >= 1; j--)
		{
			System.Console.Write($"j= {j}, ");
		}
		
		System.Console.WriteLine("\nCount Down ends");
	}
}


public class Program1
{

	public static void Main()
	{
	
		Stopwatch stopwatch = new Stopwatch();
		
		// Tasks
		
		stopwatch.Start();
		
		WithTasks();
		
		stopwatch.Stop();
		
		long timeTakenForTasks = stopwatch.ElapsedMilliseconds;
		
		System.Console.WriteLine($"\nTasks - Time taken: {timeTakenForTasks} ms");
		
		// Threads
		
		stopwatch.Restart();
		
		WithThreads();
		
		stopwatch.Stop();
		
		long timeTakenForThreads = stopwatch.ElapsedMilliseconds;
		
		System.Console.WriteLine($"\nThreads - Time taken: {timeTakenForThreads} ms");
		
		
		if (timeTakenForTasks < timeTakenForThreads)
		{
			System.Console.WriteLine("TPL is faster");
		}
		else if (timeTakenForTasks > timeTakenForThreads)
		{
			System.Console.WriteLine("Threading is faster");
		}
		else
		{
			System.Console.WriteLine("Both TPL and Threading are equal");
		}
		
		System.Console.WriteLine("Done");
	}


	public static void WithTasks()
	{
	
		// Create objects for counter classes
		
		UpCounter upCounter = new UpCounter();
		
		DownCounter downCounter = new DownCounter();
		
		CountdownEvent countdownEvent = new CountdownEvent(2);
		
		// Create and start task
		
		Task task1 = Task.Run(() =>
		{
		
			upCounter.CountUp(20);
			
			countdownEvent.Signal();
		
		});
		
		Task task2 = Task.Run(() =>
		{
		
			downCounter.CountDown(20);
			
			countdownEvent.Signal();
			
		});
		
		countdownEvent.Wait();
	
	}
	
	
	public static void WithThreads()
	{
	
	// Create objects for counter classes
	
		UpCounter upCounter = new UpCounter();
		
		DownCounter downCounter = new DownCounter();
		
		CountdownEvent countdownEvent = new CountdownEvent(2);
		
		
		// Create and start task
		
		Thread thread1 = new Thread(() =>
		{
		
			upCounter.CountUp(20);
			
			countdownEvent.Signal();
			
		});
		
		Thread thread2 = new Thread(() =>
		{
		
			downCounter.CountDown(20);
			
			countdownEvent.Signal();
		
		});
		
		
		thread1.Start();
		
		thread2.Start();
		
		countdownEvent.Wait();
	}
}
```








