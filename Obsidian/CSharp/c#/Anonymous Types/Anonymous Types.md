---
tags:
  - Anonymous_Types
Links:
---

# Anonymous Types (Object)
---

> [!NOTE] NOTE
> In C#, equality comparison on anonymous types is performed based on the values of their properties. Anonymous types automatically generate `Equals` and `GetHashCode` methods that compare the property values for equality.
> 
> Here's an example of how you can perform equality comparison on anonymous types in C#:
> 
> ```CSharp
> var person1 = new { Name = "John", Age = 30 };
> var person2 = new { Name = "John", Age = 30 };
> var person3 = new { Name = "Alice", Age = 25 };
> 
> bool isEqual1 = person1.Equals(person2); // true
> bool isEqual2 = person1.Equals(person3); // false
> ```
> 
> That the Equals method generated for anonymous types performs a deep comparison of the property values, meaning that it compares the values of all properties in the anonymous type, not just the reference to the object.

![[Pasted image 20240119180254.png]]
![[Pasted image 20240119180343.png]]
![[Pasted image 20240119180415.png]]

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
			var person = new { PersonName = p.GetPersonName(), Age = p.GetPersonAge() };
			
			//print
			Console.WriteLine(person.PersonName);
			Console.WriteLine(person.Age);
			
			Console.ReadKey();
		}
	}
}
```
















