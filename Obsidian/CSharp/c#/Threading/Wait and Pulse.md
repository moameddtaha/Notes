---
tags:
  - Threading
  - Thread_Signaling
  - Synchronization
  - TPL
---

# Wait and Pulse
---

![[52.png]]

![[53.png]]

![[54.png]]

![[55.png]]

## Example
---

```CSharp

static class Shared
{
	public static object LockObject = new object(); // Lock object to be used by both Producer and Consumer threads
	
	public static Queue<int> Buffer = new Queue<int>(); // Buffer to store int data values
	
	public const int BufferCapacity = 5;
	
	public static void Print()
	{
		Console.Write("Buffer: ");
		foreach (int item in Buffer)
		{
			Console.Write($"{item}, ");
		}
		Console.WriteLine();
	}
}



class Producer
{
	public void Produce()
	{
		for (int i = 1; i <= 10; i++)
		{
			lock (Shared.LockObject)
			{
				Console.WriteLine($"Producer: Generating Data");	
				Thread.Sleep(7000);
				
				if (Shared.Buffer.Count == Shared.BufferCapacity)
				{
					Console.WriteLine("Buffer is full. Waiting for signal from consumer.");	
					Monitor.Wait(Shared.LockObject);
				}
				
				Shared.Buffer.Enqueue(i);
				
				Console.WriteLine($"Producer produced: {i}");
				Shared.Print();
				
				Monitor.Pulse(Shared.LockObject);
			}
		}
		Console.WriteLine($"Production Completed");
	}
}

class Consumer
{
	public void Consume()
	{
		Console.WriteLine($"Consumer Started");
		
		for (int i = 0; i < 10; i++)
		{
			lock (Shared.LockObject)
			{
				if (Shared.Buffer.Count == 0)
				{
					Console.WriteLine("Buffer is empty. Waiting for signal");
					Monitor.Wait(Shared.LockObject);
				}
			}
			
			Console.WriteLine("Consumer: Processing Data");
			Thread.Sleep(2500);
			
			lock (Shared.LockObject)
			{
				int val = Shared.Buffer.Dequeue();
				
				Console.WriteLine($"Consumer consumed: {val}");
					
				// Signal the producer that there is a space in te buffer	
				Monitor.Pulse(Shared.LockObject);
			}
		}	
		Console.WriteLine($"Consumption Completed");
	}
}

public class Program3
{
	public static void Main()
	{
		Producer producer = new Producer();
		Consumer consumer = new Consumer();
		
		// Cread object of Thread class
		Thread producerThread = new Thread(producer.Produce) { Name = "Producer Thread" };
		Thread consumerThread = new Thread(consumer.Consume) { Name = "Consumer Thread" };
		
		// Start threads
		producerThread.Start();
		consumerThread.Start();
		
		// Join
		producerThread.Join();
		consumerThread.Join();
	}
}
```






