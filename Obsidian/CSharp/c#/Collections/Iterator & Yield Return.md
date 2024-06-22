---
tags: 
Links:
  - "[[IEnumerable & IEnumerator]]"
---

# Iterator
---

![[Pasted image 20231231222125.png]]

![[Pasted image 20231231222142.png]]

## Example
---

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.

> [!question]- Sample Class
> ```CSharp
> using System;
> using System.Collections.Generic;
> 
> namespace IteratorExample
> {
> 	public class Sample
> 	{
> 		public List/<double/> Prices { get; set; } = new List/<double/>() { 90, 34, 12, 80 };
> 		//Iterator method
> 		public IEnumerable/<double/> Method()
> 		{
> 			double sum = 0;
> 			foreach (double price in Prices)
> 			{
> 				sum += price;
> 				yield return sum; //90, 124, 136, 216
> 			}
> 		}
> 	}
> }
> ```

> [!question] Main Method
> ```CSharp
> using System;
> using System.Collections.Generic;
> 
> namespace IteratorExample
> {
> 	class Program
> 	{
> 		static void Main()
> 		{
> 			Sample s = new Sample();
> 			var prices_enumerable = s.Method();
> 			/*
> 			var prices_enumerator = prices_enumerable.GetEnumerator();		
> 			prices_enumerator.MoveNext();
> 			Console.WriteLine("Total price up to first product: " + prices_enumerator.Current); //90
> 			Console.WriteLine("Some more code....");
> 			
> 			prices_enumerator.MoveNext();
> 			Console.WriteLine("Total price up to second product: " + prices_enumerator.Current); //124
> 			Console.WriteLine("Some more code....");
> 			*/
> 			foreach (var item in prices_enumerable)
> 			{
> 				Console.WriteLine(item);
> 			}
> 			
> 			Console.ReadKey();
> 		}
> 	}
> }
> ```






























