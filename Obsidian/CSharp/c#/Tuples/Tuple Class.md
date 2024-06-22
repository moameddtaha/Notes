---
tags:
  - Tuples
  - Heap
Links:
  - "[[Anonymous Types]]"
---

# Tuple Class
---

![[Pasted image 20240131145803.png]]

![[Pasted image 20240131145846.png]]

# Example
---

```CSharp
using System;
namespace TupleExample
{
	class Sample
	{
		public Tuple<string, int> GetPersonDetails()
		{
			//create a new Tuple that stores person name and age
			Tuple<string, int> tuple = new Tuple<string, int>("Scott", 20);
			return tuple;
		}
	}
	class Program
	{
		static void Main()
		{
			Sample s = new Sample();
			Tuple<string, int> person = s.GetPersonDetails();
			
			//access values from tuple
			Console.WriteLine(person.Item1); //Scott
			Console.WriteLine(person.Item2); //20
		}
	}
}
```

















