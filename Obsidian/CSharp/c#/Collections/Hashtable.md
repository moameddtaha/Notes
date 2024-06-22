---
tags:
  - Collection
  - non-generic
---

# Hashtable
---

![[Pasted image 20231223141802.png]]

![[Pasted image 20231223141811.png]]

![[Pasted image 20231223141820.png]]


## Example
---
### Properties
---

>[!Example]- Get value based on key
>
>```CSharp
>
>using System.Collections;
>
>//create a Hashtable
>Hashtable employees = new Hashtable()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" },
>	{"hello", 10.934}
>};
>
>//get value based on key
>
>if(employees[105] is string)
>{
>	string value = Convert.ToString(employees[105]);
>	Console.WriteLine(value);
>}
>
>if(employees[105] is double)
>{
>	double value = Convert.ToDouble(employees[105]);
>	Console.WriteLine(value);
>}
>
>```

>[!Example]- get keys
>
>```CSharp
>
>using System.Collections;
>
>//create a Hashtable
>Hashtable employees = new Hashtable()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" },
>	{"hello", 10.934}
>};
>
>//get keys
>Console.WriteLine("\nKeys:");
>foreach (var item in employees.Keys)
>{
>	Console.WriteLine(item);
>}
>
>```

>[!Example]- get values
>
>```CSharp
>
>using System.Collections;
>
>//create a Hashtable
>Hashtable employees = new Hashtable()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" },
>	{"hello", 10.934}
>};
>
>//get values
>Console.WriteLine("\nValues:");
>foreach (var item in employees.Values)
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
>using System.Collections;
>
>//create a Hashtable
>Hashtable employees = new Hashtable()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" },
>	{"hello", 10.934}
>};
>//Add element
>employees.Add(106, "Anna");
>
>foreach (DictionaryEntry item in employees)
>{
>	Console.WriteLine(item.Key + ", " + item.Value);
>}
>```

>[!Example]- Remove element
>
>```CSharp
>
>using System.Collections;
>
>//create a Hashtable
>Hashtable employees = new Hashtable()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" },
>	{"hello", 10.934}
>};
>//Remove element
>employees.Remove(103);
>
>foreach (DictionaryEntry item in employees)
>{
>	Console.WriteLine(item.Key + ", " + item.Value);
>}
>```

>[!Example]- search for specific key
>
>```CSharp
>
>using System.Collections;
>
>//create a Hashtable
>Hashtable employees = new Hashtable()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" },
>	{"hello", 10.934}
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
>using System.Collections;
>
>//create a Hashtable
>Hashtable employees = new Hashtable()
>{   
>	{ 102, "Smith" },
>	{ 105, "James" },
>	{ 103, "Allen" },
>	{ 101, "Scott" },
>	{ 104, "Jones" },
>	{"hello", 10.934}
>};
>
>//search for specific value
>bool v = employees.ContainsValue("Scott");
>Console.WriteLine("\nScott exists: " + v);
>
>```













































































