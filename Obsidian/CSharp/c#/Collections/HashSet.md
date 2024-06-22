---
tags:
  - Collection
  - Generic
Links:
  - "[[Lambda Expressions#Inline Lambda Expressions]]"
---

# HashSet
---

![[Pasted image 20231223150351.png]]

![[Pasted image 20231223150406.png]]

![[Pasted image 20231223150415.png]]

# Example(s)
---

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.

>[!Example]- Add, Remove, RemoveWhere, Contains
>
>```CSharp
>
>using System;
>using System.Collections.Generic;
>
>namespace HashSetExample
>{
>	class Program
>	{
>		static void Main()
>		{
>			//create an object of HashSet
>			HashSet\<string> messages = new HashSet\<string>()
>			{
>				"Good Morning", "How Are You", "Have a good day"
>			};
>			//Add
>			messages.Add("Good Luck");
>			
>			//Remove
>			messages.Remove("Have a good day");
>			
>			//Remove
>			messages.RemoveWhere(m => m.EndsWith("You"));
>			
>			//Search
>			bool b = messages.Contains("Good Morning");
>			Console.WriteLine("Contains: " + b);
>			
>			//Count
>			Console.WriteLine("Count: " + messages.Count);
>			
>			//foreach
>			foreach (string message in messages)
>			{
>				Console.WriteLine(message);
>			}
>		}
>	}
>}
>```

>[!Example]- UnionWith
>
>```CSharp
>
>using System;
>using System.Collections.Generic;
>
>namespace HashSetExample2
>{
>	class Program{
>		static void Main()
>		{
>			//create two HashSet's
>			HashSet\<string> employees2021 = new HashSet\<string>() { "Amar", "Akhil", "Samareen" };
>			HashSet\<string> newEmployees2022 = new HashSet\<string>() { "John", "Scott", "Smith", "David" };
>			
>			//Union
>			employees2021.UnionWith(newEmployees2022);
>			foreach(string item in employees2021)
>			{
>				Console.WriteLine(item);
>			}
>		}
>	}
>}
>
>```

>[!Example]- IntersectWith
>
>```CSharp
>
>using System;
>using System.Collections.Generic;
>
>namespace HashSetExample2
>{
>	class Program{
>		static void Main()
>		{
>			//create two HashSet's
>			HashSet\<string> employees2021 = new HashSet\<string>() { "Amar", "Akhil", "Samareen" };
>			HashSet\<string> newEmployees2022 = new HashSet\<string>() { "John", "Scott", "Amar", "Akhil", "Smith", "David" };
>			
>			//IntersectWith
>			employees2021.IntersectWith(newEmployees2022);
>			foreach(string item in employees2021)
>			{
>				Console.WriteLine(item);
>			}
>		}
>	}
>}
>
>```





























