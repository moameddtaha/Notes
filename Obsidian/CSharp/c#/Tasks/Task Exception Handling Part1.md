---
tags:
  - TPL
  - Parts
  - Task_Continuation
  - Exception_Handling
Links:
  - "[[Task Exception Handling Part2]]"
---

# Task Exception Handling
---

> [!info] Note: Difference between `Exception` and `AggregateException`
> The key difference between the `Exception` class and the `AggregateException` class is that `AggregateException` can contain multiple exceptions, allowing you to handle multiple errors in a single catch block.

![[Tasks/img/26.png]]

## Example
---

> [!info] info
> An example of `RanToCompletion` 

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
        Task<long> task1 = Task.Run(() =>
        {
            return upCounter.CountUp(20);
        });
        
        // Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
        Task continuationTask1= task1.ContinueWith((antecedent) => 
        {
            // antecedent refers to the preceding task (task1)
            
            if (antecedent.Status == TaskStatus.RanToCompletion)
            {
                System.Console.WriteLine($"Result for Count Up: {task1.Result}");
            }
            else if(antecedent.Status == TaskStatus.Faulted)
            {
                System.Console.WriteLine($"Exception occured {task1.Exception.InnerExceptions.First().Message}");
            }
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




































