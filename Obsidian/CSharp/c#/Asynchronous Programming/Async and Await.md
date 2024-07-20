---
tags:
  - asynchronous
  - TPL
  - AsyncAndAwait
---

# Async and Await
---

> [!info] Task Representation in Async Methods
> An `async` method automatically returns a `Task` representing the asynchronous operation. This `Task` encapsulates the overall operation, including any tasks awaited within it.

> [!info] Efficient Task Handling
> The same CPU resources can handle more tasks with the same number of threads due to the efficiency of asynchronous programming.

![[Asynchronous Programming/img/3.png]]

![[Asynchronous Programming/img/4.png]]

![[Asynchronous Programming/img/5.png]]

![[Asynchronous Programming/img/6.png]]

![[Asynchronous Programming/img/7.png]]

## Writing `async` and `await` code in better way
---

![[Asynchronous Programming/img/8.png]]


### Example
---

```CSharp
// This method returns a Task<string>, representing the asynchronous operation that will eventually return the file content as a string.
internal class FileReader
{
    public async Task<string> ReadFile(string fileName)
    {
        string content;

        using (StreamReader reader = new StreamReader(fileName))
        {
            // ReadToEndAsync initiates an asynchronous read operation and returns a task that represents the operation. 
            // 'await' asynchronously waits for the task to complete and retrieves the result.
            content = await reader.ReadToEndAsync(); 
            
        } // Dispose is called automatically at the end of the using block

        return content; // Returns the content read from the file as a string.
    }
}

internal class FileWriter
{
    public async Task WriteFile(string fileName, string data)
    {
        using (StreamWriter writer = new StreamWriter(fileName))
        {
            await writer.WriteAsync(data); // Starts the asynchronous write operation and returns a Task. The await keyword asynchronously waits for the Task to complete.

        } // Dispose is called automatically at the end of the using block
    }
}

public static class Program
{
    public static async Task Main(string[] args)
    {
        string fileName = "../../../Countries.txt";

        FileWriter fileWriter = new FileWriter();
        FileReader fileReader = new FileReader();

        // Write data to a file asynchronously
        // Asynchronously waits for the read operation to complete without blocking the calling thread, only the current async method.
        await fileWriter.WriteFile(fileName, "There are 195 recognised countries in the world, according to the United Nations. 193 of these are member states of the UN.");

        Console.WriteLine("File written.");

        // Read data from the file asynchronously
        // Waits asynchronously for the read operation to complete without blocking the calling thread, and assigns the resulting content to the string variable.
        string content = await fileReader.ReadFile(fileName); 
        

        Console.WriteLine("File read.");

        Console.WriteLine($"\nFile content: {content}\n");
        
    }
}
```




