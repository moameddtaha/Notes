---
tags:
  - Generic
---

# IComparer \<T>
---

![[Pasted image 20240102233544.png]]
![[Pasted image 20240102233504.png]]
![[Pasted image 20240102233522.png]]

## Example(s)
---

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.

> [!example]- Employee Class
> 
> ```CSharp
> 
> using System;
> using System.Collections.Generic;
> 
> namespace IComparableExample
> {
> 	class Employee
> 	{
> 		public int EmpID { get; set; }
> 		public string EmpName { get; set; }
> 		public string Job { get; set; }
> 	}
> }
> 
> ```

> [!example]- enum SortBy
> 
> ```CSharp
> 
> using System;
> using System.Collections.Generic;
> 
> namespace IComparableExample
> {
> 	public enum SortBy
> 	{
> 		EmpID, EmpName, Job
> 	}
> }
> 
> ```

> [!example] CustomComparer Class
> 
> ```CSharp
> 
> using System;
> using System.Collections.Generic;
> 
> namespace IComparableExample
> {
> 	class CustomComparer : IComparer\<Employee>
> 	{
> 		/*
> 		// Sort by EmpID
> 		public int Compare(Employee x, Employee y)
> 		{
> 			return x.EmpID - y.EmpID;
> 		}
> 		*/
> 		
> 		/*
> 		//Sort by EmpName
> 		public int Compare(Employee x, Employee y)
> 		{
> 			return x.EmpName.CompareTo(y.EmpName);
> 		}
> 		*/
> 		
> 		/*
> 		//Sort By Job, EmpName
> 		public int Compare(Employee x, Employee y)
> 		{
> 			int result = 0;
> 			if (x.Job != null)
> 			{
> 				result = x.Job.CompareTo(y.Job); //first sorting column
> 			}
> 			if (result == 0)
> 			{
> 				if (x.EmpName != null)
> 				{
> 					result = x.EmpName.CompareTo(y.EmpName); //second sorting column
> 				}
> 			}
> 			return result;
> 		}
> 		*/
> 		
> 		//Sort by selected column
> 		public int Compare(Employee x, Employee y)
> 		{
> 			int result = 0;
> 			switch (this.sortBy)
> 			{
> 				case SortBy.EmpID:
> 					result = x.EmpID - y.EmpID; 
> 					break;
> 				case SortBy.EmpName:
> 					result = (x.EmpName != null) ? x.EmpName.CompareTo(y.EmpName) : 0; 
> 					break;
> 				case SortBy.Job:
> 					result = (x.Job != null) ? x.Job.CompareTo(y.Job) : 0; 
> 					break;
> 				default:
> 					result = 0; 
> 					break;
> 			}
> 			return result;
> 		}
> 		public SortBy sortBy { get; set; }		
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
> 
> namespace IComparableExample
> {
> 	class Program
> 	{
> 		static void Main()
> 		{
> 			//collection of objects
> 			List\<Employee> employees = new List\<Employee>()
> 			{
> 				new Employee() { EmpID = 104, EmpName = "Mary", Job = "Designer"},
> 				new Employee() { EmpID = 102, EmpName = "Alexa", Job = "Manager"},
> 				new Employee() { EmpID = 101, EmpName = "Steven", Job = "Consultant"},
> 				new Employee() { EmpID = 103, EmpName = "Jade", Job = "Manager"},
> 				new Employee() { EmpID = 105, EmpName = "Sara", Job = null}
> 			};
> 			
> 			CustomComparer customComparer = new CustomComparer();
> 			customComparer.sortBy = SortBy.Job;
> 			
> 			employees.Sort(customComparer);
> 			//employees.Reverse();
> 			
> 			foreach (Employee emp in employees)
> 			{
> 				Console.WriteLine(emp.EmpID + ", " + emp.EmpName + ", " + emp.Job);
> 			}
> 		}
> 	}
> }
> 
> ```



















