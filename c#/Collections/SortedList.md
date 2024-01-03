---
tags:
  - Collection
  - Generic
---

# SortedList
---

![[Pasted image 20231223131926.png]]

![[Pasted image 20231223131952.png]]

![[Pasted image 20231223132003.png]]

# Example
---
### Properties
---

>[!Example]- Get value based on key
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>
>//get value based on key
>string eName = employees[105];
>Console.WriteLine("\nEmployee name at 105: " + eName);
>
>```

>[!Example]- get keys
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>
>//get keys
>Console.WriteLine("\nKeys:");
>foreach (int item in employees.Keys)
>{
>	Console.WriteLine(item);
>}
>
>```

>[!Example]- get values
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>
>//get values
>Console.WriteLine("\nValues:");
>foreach (string item in employees.Values)
>{
>    Console.WriteLine(item);
>}
>
>```

### Methods
---

>[!Example]- Add element
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>//Add element
>employees.Add(106, "Anna");
>
>foreach (KeyValuePair<int, string> item in employees)
>{
>	Console.WriteLine(item.Key + ", " + item.Value);
>}
>```

>[!Example]- Remove element
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>//Remove element
>employees.Remove(103);
>
>foreach (KeyValuePair<int, string> item in employees)
>{
>	Console.WriteLine(item.Key + ", " + item.Value);
>}
>```

>[!Example]- search for specific key
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>
>//search for specific key
>bool k = employees.ContainsKey(105);
>Console.WriteLine("\n105 exists: " + k);
>
>```

>[!Example]- search for specific value
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>
>//search for specific value
>bool v = employees.ContainsValue("Scott");
>Console.WriteLine("\nScott exists: " + v);
>
>```

>[!Example]- index of specific key
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>
>//index of specific key
>int ki = employees.IndexOfKey(101);
>Console.WriteLine("\nIndex of 101: " + ki);
>
>```

>[!Example]- index of specific value
>
>```CSharp
>
>using System.Collections.Generic;
>
>//create a sortedlist
>SortedList<int, string> employees = new SortedList<int, string>()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" }
>};
>
>//index of specific value
>int vi = employees.IndexOfValue("Allen");
>Console.WriteLine("\n Index of Allen: " + vi);
>
>```






































