---
tags:
  - Collection
  - Generic
---

# Dictionary
---

>[!hint]
> `for` loop can't be used to access Dictionary, only `forearch` loop can be used.

![[Pasted image 20231223092112.png]]

![[Pasted image 20231223092134.png]]

![[Pasted image 20231223092146.png]]

## Examples
---
### Properties
---

>[!Example]- foreach loop
>
>```CSharp
>
>using System.Collections.Generic;
>
>Dictionary<int, string> employees = new Dictionary<int, string>()
>{
>	{101,"Scott"},
>	{102, "Smith"},
>	{103, "Allen"}	
>};
>
>// foreach loop for dictionary
>foreach(KeyValuePair<int, string> item in employees)
>{
>	System.Console.WriteLine(item.Key + ", " + item.Value);
>}
>```

>[!Example]- Get value based on the key
>
>```CSharp
>
>using System.Collections.Generic;
>
>Dictionary<int, string> employees = new Dictionary<int, string>()
>{
>	{101,"Scott"},
>	{102, "Smith"},
>	{103, "Allen"}	
>};
>
>// Get value based on the key
>int key = 101;
>string s = employees[key];
>System.Console.WriteLine($"\n Value at {key}: {s} \n");
>
>```

>[!Example]- Get keys
>
>```CSharp
>
>using System.Collections.Generic;
>
>Dictionary<int, string> employees = new Dictionary<int, string>()
>{
>	{101,"Scott"},
>	{102, "Smith"},
>	{103, "Allen"}	
>};
>
>// Get keys
>System.Console.WriteLine("Kyes");
>
>Dictionary<int, string>.KeyCollection keys = employees.Keys;
>foreach(int item in keys)
>{
>	System.Console.WriteLine(item);
>}
>
>// Alternative way
>foreach(int item in employees.Keys)
>{
>	System.Console.WriteLine(item);
>}
>
>```

>[!Example]- Get Values
>
>```CSharp
>
>using System.Collections.Generic;
>
>Dictionary<int, string> employees = new Dictionary<int, string>()
>{
>	{101,"Scott"},
>	{102, "Smith"},
>	{103, "Allen"}	
>};
>
>// Get Values
>System.Console.WriteLine("Values");
>
>Dictionary<int, string>.ValueCollection values = employees.Values;
>foreach(string item in values)
>{
>	System.Console.WriteLine(item);
>}
>
>// Alternative way
>foreach(string item in employees.Values)
>{
>	System.Console.WriteLine(item);
>}
>```

















