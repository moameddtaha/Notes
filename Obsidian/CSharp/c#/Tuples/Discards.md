---
tags:
  - Tuples
Links:
  - "[[Deconstruction]]"
---

# Discards
---

![[Pasted image 20240202155324.png]]

# Example
---

```CSharp
using System;
namespace ClassLibrary1
{
	public class Customer
	{
		public (int customerID, string customerName, string email) GetCustomerDetails()
		{
			return (101, "Scott", "scott@gmail.com");
		}
	}
	class Program
	{
		static void Main()
		{
			//create object
			Customer customer = new Customer();
			//get details
			(int customerID, _, string email) = customer.GetCustomerDetails();
			
			Console.WriteLine(cust.customerID);
			Console.WriteLine(cust.email);
		}
	}
}
```










