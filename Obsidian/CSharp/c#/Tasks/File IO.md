---
tags:
  - TPL
  - asynchronous
  - FileIO
Links:
---

# File IO
---

![[Tasks/img/33.png]]

## Example
---


> [!NOTE] Potential Issue
> Sometimes the code will crash because `StreamReader` is being disposed before the `ReadToEndAsync` task completes.


```CSharp

internal class FileWriter
{
    public Task WriteFile(string fileName, string data)
    {
        StreamWriter writer = new StreamWriter(fileName);
        Task writerTask = writer.WriteAsync(data); // Internally creates a new task and returns the task instance to be executed asynchronously
        writer.Close();

        return writerTask;
    }
}

internal class FileReader
{
    public Task<string> ReadFile(string fileName)
    {
        Task<string>? readerTask = null;
        using (StreamReader reader = new StreamReader(fileName))
        {
            // Sometimes the code will crash because `StreamReader` is being disposed before the `ReadToEndAsync` task completes (remediation: await).

            readerTask = reader.ReadToEndAsync(); // Internally creates a new task and returns the task instance to be executed asynchronously
        } // Dispose is called automatically at the end of the using block

        return readerTask;
    }
}

public static class Program
{
    public static void Main(string[] args)
    {
        string fileName = "../../../Countries.txt";

        FileWriter fileWriter = new FileWriter();
        FileReader fileReader = new FileReader();

        // Write data to a file asynchronously
        Task writerTask = fileWriter.WriteFile(fileName, "There are 195 recognised countries in the world, according to the United Nations. 193 of these are member states of the UN.");

        writerTask.Wait(); // Block until the write operation completes.

        Console.WriteLine("File written.");

        // Read data from the file asynchronously
        Task<string> readTask = fileReader.ReadFile(fileName);
        readTask.Wait(); // Block until the read operation completes.

        Console.WriteLine("File read.");

        Console.WriteLine($"\n File content: {readTask.Result}");
        Console.ReadKey();
    }
}

```















