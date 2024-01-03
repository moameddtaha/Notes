---
tags:
  - non-generic
---

# `IComparable`
---

> [!info]- The benefit of  `IComparable`
> `IComparable` is a powerful interface in C# that allows custom classes to define their own natural ordering. This is particularly valuable when dealing with collections of objects, such as a `List`, and enables the use of sorting algorithms like `Sort()`.
> - **Comparison for Sorting:**
> 	  - By implementing the `IComparable` interface, a class provides a consistent and meaningful way to compare its instances.
> 	- The `IComparable` interface defines a single method, `CompareTo`, where the class specifies how instances should be ordered relative to each other.
> - **Usage in Sorting Algorithms:**
> 	  - When a custom class implements `IComparable`, it becomes sortable using sorting methods like `List.Sort()` or other algorithms that rely on comparisons.
> 	- This facilitates the organization of collections, ensuring a predictable and intentional order based on the logic defined in the `CompareTo` method.

![[Pasted image 20240102224434.png]]

![[Pasted image 20240102224445.png]]

## Example(s)
---

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.

> [!example] Employee Class
> 
> ```CSharp
> 
> using System;
> using System.Collections.Generic;
> using System.Collections;
> 
> namespace IComparableExample
> {
> 	// Model Class
> 	class Employee: IComparable
> 	{
> 		public int EmpID { get; set; }
> 		public string EmpName { get; set; }
> 		public string Job { get; set; }
> 		
> 		/*
> 		Sort by EmpID (int)
> 		public int CompareTo(object other)
> 		{
> 			Employee otherEmp = (Employee)other;
> 			Console.WriteLine(this.EmpID + ", " + otherEmp.EmpID);
> 			return this.EmpID - otherEmp.EmpID;  //returns 0, -1 or 1
> 		}
> 		*/
> 		
> 		//Sort by EmpName (string)
> 		public int CompareTo(object other)
> 		{
> 			Employee otherEmp = (Employee)other;
> 			Console.WriteLine(this.EmpName + ", " + otherEmp.EmpName);
> 			return this.EmpName.CompareTo(otherEmp.EmpName);  //returns 0, -1 or 1
> 		}
> 	}
> }
> 
> ```

> [!example]- Main Method
> 
> ```CSharp
> 
> using System;
> using System.Collections.Generic;
> using System.Collections;
> 
> namespace IComparableExample
> {
> 	class Program
> 	{
> 		static void Main()
> 		{
> 			//list of employees
> 			List\<Employee> employees = new List\<Employee>()
> 			{
> 				new Employee() { EmpID = 104, EmpName = "Mary", Job = "Designer" },
> 				new Employee() { EmpID = 102, EmpName = "Alexa", Job = "Manager" },
> 				new Employee() { EmpID = 101, EmpName = "Steven", Job = "Consultant" },
> 				new Employee() { EmpID = 103, EmpName = "Jade", Job = "Analyst" }
> 			};
> 			
> 			employees.Sort();
> 			
> 			foreach (Employee item in employees)
> 			{
> 				Console.WriteLine(item.EmpID + ", " + item.EmpName + ", " + item.Job);
> 			}
> 		}
> 	}
> }
> 
> ```







































































