---
tags:
  - TPL
  - Parts
  - Task_Continuation
  - Exception_Handling
Links:
  - "[[Task Exception Handling Part1]]"
---

# Task Exception Handling
---

![[Tasks/img/27.png]]

![[Tasks/img/28.png]]

![[Tasks/img/29.png]]

![[Tasks/img/30.png]]

## Example
---

> [!NOTE]- Both are equal
> 
> ```CSharp
> // Create and start task 
> Task\<long> task1 = Task.Run(() => 
> { 
> 	return upCounter.CountUp(20);
> });
> 
> // Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
> Task continuationTask1= task1.ContinueWith((antecedent) => 
> {
> 	// antecedent refers to the preceding task (task1)
> 	if (antecedent.Status == TaskStatus.RanToCompletion)
> 	{
> 		System.Console.WriteLine($"Result for Count Up: {task1.Result}");
> 	}
> 	else if(antecedent.Status == TaskStatus.Faulted)
> 	{
> 		System.Console.WriteLine($"Exception occured {task1.Exception.InnerExceptions.First().Message}");
> 	}
> });
> ```
> 
> Instead you can use the `ContinueWith` method on top of `Task.Run` 
> 
> ```CSharp
> 
> // Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
> Task.Run(() =>
> {
> 	return upCounter.CountUp(20);
> }).ContinueWith((antecedent) =>
> {
> 	// antecedent refers to the preceding task (task1)
> 	
> 	if (antecedent.Status == TaskStatus.RanToCompletion)
> 	{
> 		System.Console.WriteLine($"Result for Count Up: {antecedent.Result}");
> 	}
> 	else if (antecedent.Status == TaskStatus.Faulted)
> 	{
> 		System.Console.WriteLine($"Exception occured {antecedent.Exception.InnerExceptions.First().Message}");
> 	}
> });
> ```

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

        throw new Exception("Unable to generate sum in CountUp method");

        //return sum;
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

        // Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
        Task.Run(() =>
        {
            return upCounter.CountUp(20);
        }).ContinueWith((antecedent) =>
        {
            // antecedent refers to the preceding task (task1)

            if (antecedent.Status == TaskStatus.RanToCompletion)
            {
                System.Console.WriteLine($"Result for Count Up: {antecedent.Result}");
            }
            else if (antecedent.Status == TaskStatus.Faulted)
            {
                System.Console.WriteLine($"Exception occured {antecedent.Exception.InnerExceptions.First().Message}");
            }
        });

        // Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
        Task.Factory.StartNew(() =>
        {
            return downCounter.CountDown(25);
        }).ContinueWith((antecedent) =>
        {
            // antecedent refers to the proceeding task (task2)
            System.Console.WriteLine($"Result for Count Down: {antecedent.Result.Sum}");
        });

        System.Console.WriteLine("End of main thread");

        System.Console.ReadKey(); // To not let the main method end before the tasks (use Async and Await instead)
    }
}

public class SumData
{
    public long Sum { set; get; }
}
```








