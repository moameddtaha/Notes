---
tags:
  - Threading
  - Synchronization
  - TPL
Links:
  - "[[Manual Reset Event]]"
  - "[[Auto Reset Event]]"
  - "[[Monitor]]"
  - "[[Wait and Pulse]]"
---

# Monitor vs ResetEvents (ManualResetEvent and AutoResetEvent)
---

![[56.png]]

![[57.png]]

> [!tip] Tip
> With shared resource use `Monitor` without shared resource use `ResetEvent`.

To implement thread signaling, you have two primary choices: using the `Monitor` class or using reset events (`ManualResetEvent` or `AutoResetEvent`). Here’s when to use each:

1. **Monitor Class:**
    
    - **Best For:** Scenarios involving shared resources like buffers, where both synchronization and signaling are needed.
    - **Advantages:**
        - Provides both thread synchronization and signaling within the CLR.
        - Allows fine-grained control over thread interactions using `Wait` and `Pulse` methods.
    - **Key Point:**
        - If your scenario involves shared resources and complex coordination between threads, `Monitor` class is suitable.
2. **Reset Events (`ManualResetEvent` and `AutoResetEvent`):**
    
    - **Best For:** Any scenario requiring independent thread signaling, with or without shared resources.
    - **Advantages:**
        - Simple signaling mechanism where one thread signals another to proceed.
        - Suitable even when no shared resources are involved.
    - **Key Point:**
        - Use `ManualResetEvent` or `AutoResetEvent` when you need straightforward thread signaling without complex synchronization requirements.

### Key Differences:

- **Implementation:**
    
    - `Monitor` class operates within the CLR, managing thread states without OS kernel involvement.
    - Reset events (`ManualResetEvent` and `AutoResetEvent`) utilize OS kernel events for signaling.
- **State Maintenance:**
    
    - Reset events maintain the signaled or unsignaled state, affecting thread wait behavior (`WaitOne`).
    - `Monitor` class does not maintain signal state; `Pulse` and `Wait` methods operate in the moment.
- **Thread Interaction:**
    
    - `Pulse` method in `Monitor` class releases only one waiting thread (or all with `PulseAll`), affecting threads currently waiting.
    - Reset events release threads based on their current state (`WaitOne` waits if unsignaled).

### Choosing Between Them:

- **Scenario-Specific:**
    
    - If you need robust synchronization with shared resources, choose `Monitor`.
    - For straightforward signaling between threads, especially without shared resources, opt for reset events.
- **Sequence Dependency:**
    
    - Use `Monitor` when you can ensure the sequence of `Wait` and `Pulse` operations.
    - Choose reset events if thread interaction order may vary.


# Monitor with ManualResetEvent
---

![[58.png]]

## Example
---

> [!tip] Tip
> Use Wait() and Pulse() inside Lock() and avoid using ResetEvent inside Lock.

```CSharp

static class Shared
{
	public static object LockObject = new object(); // Lock object to be used by both Producer and Consumer threads
	
	public static Queue<int> Buffer = new Queue<int>(); // Buffer to store int data values
	
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
			lock (Shared.LockObject)
			{
				Console.WriteLine($"Producer: Generating Data");
				
				Thread.Sleep(7000);
				
				if (Shared.Buffer.Count == Shared.BufferCapacity)
				{
					Console.WriteLine("Buffer is full. Waiting for signal from consumer.");
					Shared.ProducerEvent.Reset();
				}
			}
			
			Shared.ProducerEvent.WaitOne();
			
			lock (Shared.LockObject)
			{
				Shared.Buffer.Enqueue(i);
				
				Console.WriteLine($"Producer produced: {i}");
				
				Shared.Print();
				
				Shared.ConsumerEvent.Set(); // Sets the consumer event state as "signaled". It wakes-up the consumer thread.
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
					
					Shared.ConsumerEvent.Reset(); // Set the consumer event as "unsignaled"
				}
			}
			
			Shared.ConsumerEvent.WaitOne();
			
			Console.WriteLine("Consumer: Processing Data");
			//Thread.Sleep(2500);
			
			lock (Shared.LockObject)
			{
				int val = Shared.Buffer.Dequeue();
				
				Console.WriteLine($"Consumer consumed: {val}");
				
				// Signal the producer that there is a space in te buffer
				Shared.ProducerEvent.Set();
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

















