---
tags: 
Links:
  - "[[Anonymous Types]]"
---

# Nested Anonymous Types
---

![[Pasted image 20240119180616.png]]

## Example
---

```CSharp
using System;
namespace ClassLibrary1
{
	public class Person
	{
		public string GetPersonName()
		{
			return "Smith";
		}
		public int GetPersonAge()
		{
			return 25;
		}
	}
}
```

```CSharp
using System;
using ClassLibrary1;
namespace AnonymousObjectsExample
{
	class Program
	{
		static void Main()
		{
			//create object of Person class
			Person p = new Person();
			
			//call Methods
			var person = new { PersonName = p.GetPersonName(), Age = p.GetPersonAge(), Address = new { Street = "abc", City = "xyz"  } 
			};
			
			//print
			Console.WriteLine(person.PersonName);
			Console.WriteLine(person.Age);
			Console.WriteLine(person.Address.City);
			Console.WriteLine(person.Address.Street);
			
			Console.ReadKey();
		}
	}
}
```










