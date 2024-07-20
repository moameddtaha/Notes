---
tags:
  - Threading
---

# Threading
---

![[Tasks/img/3.png]]
![[Tasks/img/4.png]]

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
	Console.WriteLine(mainThread.Name);
	Method1();
	}
	static void Method1(){
		System.Console.WriteLine("Method 1");
	}
}
```

