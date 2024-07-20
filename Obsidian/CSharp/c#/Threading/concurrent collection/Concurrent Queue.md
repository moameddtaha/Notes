---
tags:
  - Threading
  - Synchronization
  - Concurrent
  - Collection
---

# Concurrent Queue
---

![[65.png]]

![[66.png]]

## Example
---

```CSharp
using System.Collections.Concurrent;


static class Shared

{

	public static ConcurrentQueue<int> Buffer = new ConcurrentQueue<int>(); // Buffer to store int data values
	
	public const int BufferCapacity = 5;
	
	public static ManualResetEvent ProducerEvent = new ManualResetEvent(true);
	
	public static ManualResetEvent ConsumerEvent = new ManualResetEvent(false);
	
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
			Console.WriteLine($"Producer: Generating Data");
			
			Thread.Sleep(2500);
			
			if (Shared.Buffer.Count == Shared.BufferCapacity)
			{
				Console.WriteLine("Buffer is full. Waiting for signal from consumer.");
				
				Shared.ProducerEvent.Reset();
			}
			
			Shared.ProducerEvent.WaitOne();
			
			Shared.Buffer.Enqueue(i);
			
			Console.WriteLine($"Producer produced: {i}");
			
			Shared.Print();

			Shared.ConsumerEvent.Set(); // Sets the consumer event state as "signaled". It wakes-up the consumer thread.
			
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
			if (Shared.Buffer.Count == 0)
			{
				Console.WriteLine("Buffer is empty. Waiting for signal");
				
				Shared.ConsumerEvent.Reset(); // Set the consumer event as "unsignaled"
			}
			
			Shared.ConsumerEvent.WaitOne();
			
			Console.WriteLine("Consumer: Processing Data");
			
			Thread.Sleep(3000);
			
			bool isSuccess = Shared.Buffer.TryDequeue(out int val);
			
			if (isSuccess)
			{
				Console.WriteLine($"Consumer consumed: {val}");
			}
			else
			{
				Console.WriteLine("Faild to read data from queue.");
			}
			
			// Signal the producer that there is a space in te buffer
			Shared.ProducerEvent.Set();
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















