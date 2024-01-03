---
tags:
  - Collection
---

# Object Relation
---

![[Pasted image 20231225154545.png]]

![[Pasted image 20231225154601.png]]

## Example(s)
---

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.


### One-to-One Relation
---

>[!Example]- Student Class
>
>```CSharp
>
>using System;
>
>namespace College
>{
>	public class Student
>	{
>		public int RollNo { get; set; }
>		public string StudentName { get; set; }
>		public string Email { get; set; }
>		public Branch branch { get; set; } //contains reference to object of Branch class, that represents the branch that the current student belongs to.
>	}
>}
>
>```

>[!Example]- Main Method
>
>```CSharp
>
>using System;
>using College;
>
>namespace OneToOneExample
>{
>	class Program
>	{
>		static void Main()
>		{
>			//Student class's object
>			Student student = new Student();
>			student.RollNo = 123;
>			student.StudentName = "Scott";
>			student.Email = "scott@gmail.com";
>			
>			//one-to-one relation
>			student.branch = new Branch();
>			student.branch.BranchName = "Computer Science Engineering";
>			student.branch.NoOfSemesters = 8;
>			
>			//display
>			Console.WriteLine(student.RollNo);
>			Console.WriteLine(student.StudentName);
>			Console.WriteLine(student.Email);
>			Console.WriteLine(student.branch.BranchName)
>			Console.WriteLine(student.branch.NoOfSemesters);
>			
>			Console.ReadKey();
>		}
>	}
>}
>
>```


### One-to-Many Relation
---

>[!Example]- Examination Class
>
>```CSharp
>
>using System;
>
>namespace College
>{
>	/// \<summary>
>	/// Represents examination attempted by the student
>	/// \</summary>
>	
>	public class Examination
>	{
>		public string ExaminationName { get; set; }
>		public int Month { get; set; }
>		public int Year { get; set; }
>		public int MaxMarks { get; set; }
>		public int SecuredMarks { get; set; }
>	}
>}
>
>```

>[!Example]- Student Class
>
>```CSharp
>
>using System;
>
>namespace College
>{
>	/// \<summary>
>	/// Represents a student
>	/// \</summary>
>	
>	public class Examination
>	{
>		public int RollNo { get; set; }
>		public string StudentName { get; set; }
>		public string Email { get; set; }
>		public List\<Examination> examinations { get; set; }
>	}
>}
>
>```

>[!Example]- Main Method
>
>```CSharp
>
>using System;
>using System.Collections.Generic;
>using College;
>
>namespace OneToManyExample
>{
>	class Program
>	{
>		static void Main()
>		{
>			//Create object of Student class
>			Student student = new Student();
>			student.RollNo = 1;
>			student.StudentName = "Allen";
>			student.Email = "allen@gmail.com";
>			student.examinations = new List\<Examination>();
>			
>			student.examinations.Add(new Examination() { ExaminationName = "Module Test 1", Month = 5, Year = 2021, MaxMarks = 100, SecuredMarks = 87 });
>			student.examinations.Add(new Examination() { ExaminationName = "Module Test 2", Month = 7, Year = 2022, MaxMarks = 100, SecuredMarks = 70 });
>			student.examinations.Add(new Examination() { ExaminationName = "Final Test", Month = 3, Year = 2024, MaxMarks = 100, SecuredMarks = 91 });
>			
>			//print
>			Console.WriteLine("Roll No: " + student.RollNo);
>			Console.WriteLine("Student Name: " + student.StudentName);
>			Console.WriteLine("Email: " + student.Email);
>			Console.WriteLine("EXAMINATIONS:");
>			foreach (Examination exam in student.examinations)
>			{
>				Console.WriteLine(exam.ExaminationName + ", " + exam.Year + "-" + exam.Month + ", " + exam.SecuredMarks + "/" + exam.MaxMarks);
>			}
>			Console.ReadKey();
>		}
>	}
>}
>
>```


### Many-to-Many Relation
---

>[!Example]- Department Class
>
>```CSharp
>
>using System;
>
>namespace Company
>{
>	/// \<summary>
>	/// Represents a department of the organization
>	/// \</summary>
>	
>	public class Department
>	{
>		public int DepartmentID { get; set; }
>		public string DepartmentName { get; set; }
>	}
>}
>
>```

>[!Example]- Employee Class
>
>```CSharp
>
>using System;
>using System.Collections.Generic;
>
>namespace Company
>{
>	/// \<summary>
>	/// Represents a employee of the organization
>	/// \</summary>
>	
>	public class Employee
>	{
>		public int EmployeeID { get; set; }
>		public string EmployeeName { get; set; }
>		public string Email { get; set; }
>		public Department dept { get; set; }
>	}
>}
>
>```

>[!Example]- Main Method
>
>```CSharp
>
>using System;
>using System.Collections.Generic;
>using Company;
>
>namespace ManyToOneExample
>{
>	/// \<summary>
>	/// Represents a employee of the organization
>	/// \</summary>
>	
>	class Program
>	{
>		static void Main()
>		{
>			//Three employees in same department
>			Employee employee1 = new Employee() { EmployeeID = 1, EmployeeName = "Scott", Email = "scott@gmail.com" };
>			Employee employee2 = new Employee() { EmployeeID = 2, EmployeeName = "Allen", Email = "allen@gmail.com" };
>			Employee employee3 = new Employee() { EmployeeID = 3, EmployeeName = "Smith", Email = "smith@gmail.com" };
>			
>			//create object of Department class
>			Department department = new Department() { DepartmentID = 10, DepartmentName = "Accounting" };
>			
>			employee1.dept = department;
>			employee2.dept = department;
>			employee3.dept = department;
>			
>			//print
>			Console.WriteLine("FIRST EMPLOYEE:");
>			Console.Write("Employee ID: " + employee1.EmployeeID);
>			Console.Write("Employee Name: " + employee1.EmployeeName);
>			Console.Write("Email: " + employee1.Email);
>			Console.Write("Department ID: " + employee1.dept.DepartmentID);
>			Console.Write("Department Name: " + employee1.dept.DepartmentName)
>			Console.WriteLine("\nSECOND EMPLOYEE:");
>			Console.Write("Employee ID: " + employee2.EmployeeID);
>			Console.Write("Employee Name: " + employee2.EmployeeName);
>			Console.Write("Email: " + employee2.Email);
>			Console.Write("Department ID: " + employee2.dept.DepartmentID);
>			Console.Write("Department Name: " + employee2.dept.DepartmentName)
>			Console.WriteLine("\nTHIRD EMPLOYEE:");
>			Console.Write("Employee ID: " + employee3.EmployeeID);
>			Console.Write("Employee Name: " + employee3.EmployeeName);
>			Console.Write("Email: " + employee3.Email);
>			Console.Write("Department ID: " + employee3.dept.DepartmentID);
>			Console.Write("Department Name: " + employee3.dept.DepartmentName);
>			
>			Console.ReadKey();
>		}
>	}
>}
>
>```






