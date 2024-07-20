---
tags:
  - asynchronous
  - TPL
Links:
  - "[[Task class]]"
---

# Task.Run
---

> [!info] info
> **Task.Run** is for simple task execution on the default thread pool, while **Task.Factory.StartNew** offers advanced control over task creation and scheduling options.

![[Tasks/img/12.png]]

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
		
		Task task1 = Task.Run(() =>
		{
			upCounter.CountUp(20);
		});
		
		Task task2 = Task.Run(() =>
		{
			downCounter.CountDown(20);
		});
		
		Console.ReadKey(); // Important to not let the program exit execution before tasks finish.
	
	}
}
```
