---
tags:
  - TPL
---

# Returning Complex Types

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
		}
		
		System.Console.WriteLine("\nCount Down ends");
		
		return new SumData(){Sum = sum};
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
		
		Task<SumData> task2 = Task.Factory.StartNew(() =>
		{
			return downCounter.CountDown(25);
		});
		
		Task.WaitAll(task1, task2);
		
		System.Console.WriteLine($"Result for Count Up: {task1.Result}");
		
		System.Console.WriteLine($"Result for Count Down: {task2.Result.Sum}");
		
		System.Console.WriteLine("Done");
	}
}

public class SumData
{
	public long Sum { set; get; }
}
```










