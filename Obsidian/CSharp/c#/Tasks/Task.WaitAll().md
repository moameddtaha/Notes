---
tags:
  - Synchronization
  - TPL
---

# Task.WaitAll
---

![[Tasks/img/20.png]]

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
	
		// Create objects for counter classes
		
		UpCounter upCounter = new UpCounter();
		
		DownCounter downCounter = new DownCounter();
		
		// Create and start task
		
		Task task1 = Task.Factory.StartNew(() =>
		{
			upCounter.CountUp(20);
		});
		
		Task task2 = Task.Factory.StartNew(() =>
		{
			downCounter.CountDown(20);
		});
		
		Task.WaitAll(task1, task2);
		
		System.Console.WriteLine("Done");
	}
}

```














