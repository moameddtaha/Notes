---
tags:
  - Array
Links:
  - "[[Anonymous Types]]"
---

# Anonymous Arrays
---

![[Pasted image 20240119180714.png]]

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
			var persons = new[ ] {
			new { PersonName = "Scott", Email = "scott@gmail.com" },
			new { PersonName = "Smith", Email = "smith@gmail.com" },
			new { PersonName = "Allen", Email = "allen@gmail.com" },
			new { PersonName = "Jones", Email = "jones@gmail.com"  }
			};
			
			//foreach
			foreach (var item in persons)
			{
				Console.Write(item.PersonName);
				Console.Write(", ");
				Console.WriteLine(item.Email);
			}
			
			Console.ReadKey();
		}
	}
}
```












