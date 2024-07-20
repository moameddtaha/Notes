---
tags:
  - Threading
  - Synchronization
  - TPL
Links:
  - "[[Thread Pool]]"
---

# CountDownEvent
---

> [!tip] tip
> Used with thread pool

![[88.png]]

![[89.png]]

![[90.png]]

![[91.png]]

## Example
---

```CSharp

public class Shared

{
	public static Mutex mutex { set; get; }
	
	public static string? FilePath { get; set; }
	
	public static int? ChunckSize { get; set; }
	
	public static int MinConcurrency { set; get; }
	
	public static int MaxConcurrency { set; get; }
	
	public static CountdownEvent Count { set; get; }
	
	static Shared()
	{
		mutex = new Mutex();
		
		FilePath = "../../../MOCK_DATA.csv";
		
		ChunckSize = 100;
		
		MaxConcurrency = 3;
		
		MinConcurrency = 3;
	}
}


public class DataProcessor
{
	public string? ChunkName { set; get; }
	
	public List<string>? Chunk { set; get; }
	
	public Dictionary<string, int> GenderCounts = new Dictionary<string, int>();
	
	public void ProcessChunk()
	{
		// e.g: 1,Carissa,Preuvost,cpreuvost0@noaa.gov,Female
		
		foreach (string line in Chunk)
		{
			if (string.IsNullOrEmpty(line))
				continue;
			
			string[] values = line.Split(',');
			
			if (values.Length >= 5)
			{
				string gender = values[4].Trim().ToLower();
				
				if (GenderCounts.ContainsKey(gender))
				{
					GenderCounts[gender]++;
				}
				else
				{
					GenderCounts.Add(gender, 1);
				}
			}
			
			// Simulate delay
			Random random = new Random();
			Thread.Sleep(100 * random.Next(2,5));
		}
	}
}



public class Program
{
	static void Main()
	{
	
	//  Read data from the file
	
	using (StreamReader sr = new StreamReader(Shared.FilePath))
	{
	
		string? line;
		
		int lineNumber = 0;
		
		// Create a chunk (an empty list of string)
		
		List<string> chunk = new List<string>();
		
		
		int threadCount = 0;
		
		// Create a semaphore to limit the number of concurrent threads
		
		Semaphore semaphore = new Semaphore(Shared.MinConcurrency, Shared.MaxConcurrency);
		
		
		
		// Read each line from the file
		
		while ((line = sr.ReadLine()) != null)
		{
			// Skip the iteration if the line is empty
			
			if (string.IsNullOrEmpty(line))
				continue;
			
			// Linq is not null (so increase the line count)
			
			lineNumber++;
			
			chunk.Add(line);
			
			// reached to end of chunk
			
			if (lineNumber % Shared.ChunckSize == 0)
			
			{
			
				// creat a duplicate copy of chunk
				
				List<string> chunkCopy = chunk.Select(temp => temp).ToList();
				
				
				
				// Creat chunk name
				
				threadCount++;
				
				string chunkName = $"Chunk {threadCount}";
				
				
				
				ThreadPool.QueueUserWorkItem((object? state) =>
				{
					// Wait for the semaphore to be available
					
					semaphore.WaitOne();
					
					try
					{
						InvokeDataProcessor(chunkName, chunkCopy);
					}
					catch (Exception ex)
					{
						Console.WriteLine(ex.Message);
					}
					finally
					{
						semaphore.Release();
					}
				}, chunkName);
				
				chunk.Clear();
			}
		}
		
		// prcess the last chunk (if any)
		
		if (chunk.Count > 0)
		{
			// Creat chunk name
			
			threadCount++;
			
			string chunkName = $"Chunk {threadCount}";
			
			ThreadPool.QueueUserWorkItem((object? state) =>
			{
			
				// Wait for the semaphore to be available
				
				semaphore.WaitOne();
				
				
				
				try
				{
					InvokeDataProcessor(chunkName, chunk);
				}
				catch (Exception ex)	
				{
					Console.WriteLine(ex.Message);
				}
				finally
				{
					semaphore.Release();
				}
			});
		}
		
		Shared.Count = new CountdownEvent(threadCount); // Initialize the intialCount and CurrentCount to 0
		
		Shared.Count.Wait(); // Wait for al threads to complete (until the CurrentCount becomes 0)
		
		};
		Console.WriteLine("\nAll CSV lines processed.");
	}
	
	
	
	// A method to invoke DataProcessor
	
	public static void InvokeDataProcessor(string chunkName, List<string> chunk)
	{
	
		// Create an object of DataProcessor
		
		DataProcessor dataProcessor = new DataProcessor() { Chunk = chunk, ChunkName = chunkName };
		
		Console.WriteLine($"Processing: {dataProcessor.ChunkName} of size: {chunk.Count}");
		
		dataProcessor.ProcessChunk();
		
		
		// Print output
		
		try
		{
			Shared.mutex.WaitOne();
			
			Console.WriteLine($"\nProcessed: {dataProcessor.ChunkName} of size: {chunk.Count}");
			
			Console.WriteLine($"{dataProcessor.ChunkName}");
			
			foreach (var gender in dataProcessor.GenderCounts)
			{
				Console.WriteLine($"{gender.Key}: {gender.Value}");
			}
		}
		catch (Exception e)
		{
			Console.WriteLine($"{e.Message}");
		}
		finally
		{
			Shared.Count.Signal(); // Signals that the thread is done (decrease the CurrentCount property by 1).
			
			Shared.mutex.ReleaseMutex();
		}
		
	}

}

```




