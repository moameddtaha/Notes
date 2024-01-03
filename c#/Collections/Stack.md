---
tags:
  - Collection
  - Generic
---

# Stack
---

![[Pasted image 20231225111048.png]]

![[Pasted image 20231225111059.png]]

![[Pasted image 20231225111111.png]]

# Example(s)
---

```CSharp
using System;
using System.Collections.Generic;
namespace StackExample
{
	class Student
	{
		public int Marks { get; set; }
		public int Rank { get; set; }
	}
	class Program
	{
		static void Main()
		{
			 //create object of Stack
			 Stack<Student> marks = new Stack<Student>();
			 
			 //Add
			 marks.Push(new Student() { Marks = 45 });
			 marks.Push(new Student() { Marks = 61 });
			 marks.Push(new Student() { Marks = 80 });
			 
			 //Pop
			 Student stu1 = marks.Pop();
			 Console.WriteLine("Pop: " + stu1.Marks);
			 
			 //Peek
			 Student stu2 = marks.Peek();
			 Console.WriteLine("Peek: " + stu2.Marks);
			 
			 //foreach
			 int r = 1;
			 foreach (Student item in marks)
			 {
				 item.Rank = r;
				 Console.WriteLine(item.Marks + ", " + item.Rank);
				 r++;
			}
		}
	}
}

```


















































