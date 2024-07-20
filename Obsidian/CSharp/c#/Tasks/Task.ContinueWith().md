---
tags:
  - TPL
  - Synchronization
  - Task_Continuation
---

# Task.ContinueWith
---

> [!info] Task Continuation
> `Task.ContinueWith` does not block the calling thread.

![[Tasks/img/25.png]]

## Example
---

```CSharp

public class UpCounter
{
	public long CountUp(int count)
	{
		long sum = 0;
		
		System.Console.WriteLine("\nCount Up starts");
		
		for (int i = 1; i <= count; i++)
		{
			System.Console.Write($"i= {i}, ");
			
			sum += i;
			
			Task.Delay(300).Wait();
		}
		
		System.Console.WriteLine("\nCount Up ends");
		
		return sum;
	}
}

public class DownCounter
{
	public SumData CountDown(int count)
	{
		long sum = 0;
		
		System.Console.WriteLine("\nCount Down starts");
		
		for (int j = count; j >= 1; j--)
		{
			System.Console.Write($"j= {j}, ");
			
			sum += j;
			
			Task.Delay(300).Wait();
		}
		
		System.Console.WriteLine("\nCount Down ends");
		
		return new SumData() { Sum = sum };
	}
}

public class Program1
{
	public static void Main()
	{
	
	// Create objects for counter classes
	
	UpCounter upCounter = new UpCounter();
	
	DownCounter downCounter = new DownCounter();
	
	// Create and start task
	
	Task<long> task1 = Task.Run(() =>
	{
		return upCounter.CountUp(20);
	});
	
	
	// Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
	Task continuationTask1= task1.ContinueWith((antecedent) =>
	{
		// antecedent refers to the preceding task (task1)
		
		System.Console.WriteLine($"Result for Count Up: {task1.Result}");
	});
	
	
	Task<SumData> task2 = Task.Factory.StartNew(() =>
	{
		return downCounter.CountDown(25);
	});
	
	// Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
	Task continuationTask2= task2.ContinueWith((antecedent) =>
	{
		// antecedent refers to the proceeding task (task2)
		
		System.Console.WriteLine($"Result for Count Down: {task2.Result.Sum}");
	});
	
	System.Console.WriteLine("End of main thread");
	System.Console.ReadKey();
	}
}

public class SumData
{
	public long Sum { set; get; }
}

```









