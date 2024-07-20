---
tags:
  - TPL
---

# Task Cancellation
---

> [!hint] Handling Task Cancellation
> `ThrowIfCancellationRequested` is a special method that throws an `OperationCanceledException` when cancellation is requested. This exception causes the task status to be `Canceled`, unlike other exceptions which set the task status to `Faulted`.
> 
> Unlike other exceptions, `ThrowIfCancellationRequested` does not crash the task; instead, it gracefully handles cancellation by setting the task status to `Canceled`.

> [!info] Managing Task Cancellation
> Each task requiring independent cancellation should be associated with its own unique cancellation token.

![[Tasks/img/32.png]]

## Example
---

```CSharp
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Threading.Tasks;

namespace Tasks
{
    public class UpCounter
    {
        public long CountUp(int count, CancellationToken token)
        {
            long sum = 0;
            System.Console.WriteLine("\nCount Up starts");
            for (int i = 1; i <= count; i++)
            {
                token.ThrowIfCancellationRequested(); // Throw new OperationCanceledException

                System.Console.Write($"i= {i}, ");
                sum += i;
                Task.Delay(300).Wait();
            }
            System.Console.WriteLine("\nCount Up ends");

            //throw new Exception("Unable to generate sum in CountUp method");

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

            // Create CancellationTokenSource class object (used to cancel a task)
            CancellationTokenSource cts = new CancellationTokenSource();

            // Create and start task

            // Create a new continuation task object that gets executed (starts automatically) when the antecedent (preceding) task is completed (either successfuly or with an exception)
            Task.Run(() =>
            {
                return upCounter.CountUp(20, cts.Token);
            }, cts.Token).ContinueWith((antecedent) =>
            {
                // antecedent refers to the preceding task (task1)

                if (antecedent.Status == TaskStatus.Canceled)
                {
                    Console.WriteLine("Count Up Task Canclled");
                    return -1;
                }
                if (antecedent.Status == TaskStatus.Faulted)
                {
                    Console.WriteLine($"Exception occured {antecedent.Exception.InnerExceptions.First().Message}");
                    return -1;
                }
                else if (antecedent.Status == TaskStatus.RanToCompletion)
                {
                    return antecedent.Result; // Passing the result to the next continuation since we can't directly access the original task there.
                }
                else
                {
                    return -1;
                }
            }).ContinueWith((antecedent) =>
            {
                if (antecedent.Result != -1)
                    Console.WriteLine($"Result for Count Up: {antecedent.Result}");
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

            // Cancel the task1
            Task.Delay(5000).Wait();
            cts.Cancel();

            System.Console.WriteLine("End of main thread");

            System.Console.ReadKey(); // To not let the main method end before the tasks (use Async and Await instead)
        }
    }

    public class SumData
    {
        public long Sum { set; get; }
    }
}
```













































