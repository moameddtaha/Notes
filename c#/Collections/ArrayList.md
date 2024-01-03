---
tags:
  - Collection
  - non-generic
---

# ArrayList
---

![[Pasted image 20231224153343.png]]

![[Pasted image 20231224153357.png]]

![[Pasted image 20231224153407.png]]

# Example
---

>[!Example]- Sample Class
>
>```CSharp
>
>using System;
>using System.Collections;
>
>namespace ArrayListExample
>{
>	class Sample
>	{
>		public int GetNumber()
>		{
>			return 10;
>		}
>		public double GetAnotherNumber()
>		{
>			return 10.7;
>		}
>		public string GetMessage()
>		{
>			 return "Hello";
>		}
>		public Employee GetEmployee()
>		{
>			return new Employee() { EmployeeName = "Scott" };
>		}		
>	}
>}
>
>```

>[!Example]- Employee Class
>
>```CSharp
>
>using System;
>using System.Collections;
>
>namespace ArrayListExample
>{
>	class Employee
>	{
>		public string EmployeeName { get; set; }
>	}
>}
>
>```

>[!Example] Main Method
>
>```CSharp
>
>using System;
>using System.Collections;
>
>namespace ArrayListExample
>{
>	class Program
>	{
>		static void Main()
>		{
>			//Create object of ArrayList class
>			ArrayList arrayList = new ArrayList() { 100, 'A' };
>			
>			Sample s = new Sample();
>			
>			//Add
>			arrayList.Add(s.GetNumber());
>			arrayList.Add(s.GetAnotherNumber());
>			arrayList.Add(s.GetMessage());
>			arrayList.Add(s.GetEmployee());
>			
>			//foreach
>			foreach (var item in arrayList)
>			{
>				if (item is Employee emp)
>				{
>					Console.WriteLine(emp.EmployeeName);
>				}
>				else
>				{
>					Console.WriteLine(item);
>				}
>			}
>		}
>	}
>}
>
>```




























































