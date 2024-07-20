---
tags:
  - TPL
---

# Task.Delay
---


> [!info] Difference Between `Task.Delay` and `Thread.Sleep`
> `Task.Delay(int millisecondsDelay)` creates and returns a new `Task` that represents a delay or pause in the execution of tasks without blocking the calling thread. It sets up a timer, and the task completes after the specified delay period. This allows the calling thread to continue executing other code during the delay. Essentially, `Task.Delay` creates a new task that delays for the specified amount of time only; if you need to wait for that delay, you can use `await`.
> 
> In contrast, `Thread.Sleep(int millisecondsTimeout)` directly keeps the current working thread in a WaitSleepJoin state, meaning the calling thread will not be able to execute any other code until the specified amount of time has elapsed. This makes `Thread.Sleep` blocking, while `Task.Delay` is non-blocking and more suitable for asynchronous operations.
> 
> **Key Points:**
> - **Task Creation**: `Task.Delay(int millisecondsDelay)` creates and returns a new `Task` that represents a delay of the specified number of milliseconds.
> - **Non-blocking**: The method returns immediately, allowing the calling thread to continue executing other code. The actual delay is handled asynchronously.
> - **Awaiting the Task**: If you use the `await` keyword with `Task.Delay`, the calling method will asynchronously wait for the delay to complete without blocking the calling thread.
> - **Blocking with `.Wait()`**: If you call `.Wait()` on the task returned by `Task.Delay`, it will block the calling thread until the delay task completes.


![[Tasks/img/24.png]]

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
















