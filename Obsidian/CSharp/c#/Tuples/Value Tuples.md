---
tags:
  - Tuples
  - New
  - Stack
Links:
  - "[[Tuple Class]]"
---

# Value Tuples
---

![[Pasted image 20240131150422.png]]

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
			(int customerID, string customerName, string email) cust = customer.GetCustomerDetails();
			
			Console.WriteLine(cust.customerID);
			Console.WriteLine(cust.customerName);
			Console.WriteLine(cust.email);
		}
	}
}
```














