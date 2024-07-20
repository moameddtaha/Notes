---
tags:
  - Threading
  - asynchronous
---

# Thread Class
---

![[Tasks/img/5.png]]
![[Tasks/img/6.png]]
![[Tasks/img/7.png]]
![[Tasks/img/8.png]]

### Details
---

![[Tasks/img/9.png]]
![[Tasks/img/10.png]]
![[Tasks/img/11.png]]

## Example
---
```CSharp
using System;
using System.Threading;
class Program
{
	static void Main(){
		Thread mainThread = Thread.CurrentThread;
		mainThread.Name = "Main Thread";
		ThreadPriority priority = mainThread.Priority;
		
		Console.WriteLine(mainThread.Name); // Main Thread
		Console.WriteLine(priority);    // Normal
		Console.WriteLine(mainThread.IsAlive);  // True
		Console.WriteLine(mainThread.IsBackground); // False (Default)
		
		ThreadState state =  mainThread.ThreadState;
		Console.WriteLine(state); // Running
	}
}
```










