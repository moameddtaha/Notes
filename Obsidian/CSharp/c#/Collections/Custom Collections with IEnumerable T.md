---
tags:
  - Generic
---

# Custom Collections with `IEnumerable <T>`
---

![[Pasted image 20240101232205.png]]
## Example
---

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.

> [!info]- Note
> In the context of implementing the `IEnumerable` interface in the custom collection class, there's a crucial distinction between two specific functions within the code.
> 
> The initial function:
> 
> ```CSharp
> //implementing IEnumerable.GetEnumerator()
> IEnumerator IEnumerable.GetEnumerator()
> {
> 	return this.GetEnumerator();
> }
> 
> ```
> 
> This function is vital to prevent compilation errors. However, the function that is invoked during iteration is:
> 
>  ```CSharp
>  //implementing IEnumerable\<T>.GetEnumerator()
> public IEnumerator\<Customer> GetEnumerator()
> {
> 	for (int i = 0; i < customers.Count; i++)
> 	{
> 		yield return customers[i]; //return and pause
> 	}
> }
> 
> ```
> 
> The latter function, `IEnumerable<T>.GetEnumerator()`, is called as we implement `IEnumerable<Customer>`, enabling the enumeration of `Customer` objects.
> 
> Notably, this distinction is essential for the correct operation of the custom collection class.
> 

> [!example]- TypeOfCustomer
> ```CSharp
> using System;
> using System.Collections.Generic;
> using System.Collections;
> 
> namespace CustomCollections
> {
> 	public enum TypeOfCustomer
> 	{
> 		RegularCustomer, VIPCustomer
> 	}
> }
> ```

> [!example]- Customer Class
> ```CSharp
> using System;
> using System.Collections.Generic;
> using System.Collections;
> 
> namespace CustomCollections
> {
> 	public class Customer
> 	{
> 		public string CustomerID { get; set; }
> 		public string CustomerName { get; set; }
> 		public string Email { get; set; }
> 		public TypeOfCustomer CustomerType { get; set; }
> 	}
> }
> ```

> [!example] Custom collection with IEnumerable T
> ```CSharp
> using System;
> using System.Collections.Generic;
> using System.Collections;
> 
> namespace CustomCollections
> {
> 	//custom collection class
> 	public class CustomersList: IEnumerable\<Customer>
> 	{
> 		//private collection as a field
> 		private List\<Customer> customers = new List\<Customer>();
> 		
> 		//implementing IEnumerable.GetEnumerator()
> 		 IEnumerator IEnumerable.GetEnumerator()
> 		{
> 			return this.GetEnumerator();
> 		}
> 		
> 		//implementing IEnumerable\<T>.GetEnumerator()
> 		public IEnumerator\<Customer> GetEnumerator()
> 		{
> 			for (int i = 0; i < customers.Count; i++)
> 			{
> 				yield return customers[i]; //return and pause
> 			}
> 		}
> 			
> 		//Add with validations
> 		public void Add(Customer cust)
> 		{
> 			if (cust.CustomerID.StartsWith("A") || cust.CustomerID.StartsWith("a"))
> 			{
> 				customers.Add(cust);
> 			}
> 			else
> 			{
> 				Console.WriteLine("Invalid Customer ID");
> 			}
> 		}
> 	}
> }
> ```

> [!example]- Main Method
> ```CSharp
> using System;
> using System.Collections.Generic;
> using System.Collections;
> 
> namespace CustomCollections
> {
> 	class Program
> 	{
> 		static void Main()
> 		{
> 			CustomersList customersList = new CustomersList() {
> 			new Customer() { CustomerID = "A101", CustomerName = "James", Email = "james@example.com", CustomerType = TypeOfCustomer.RegularCustomer },
> 			new Customer() { CustomerID = "A201", CustomerName = "Bob", Email = "bob@example.com", CustomerType = TypeOfCustomer.VIPCustomer },
> 			new Customer() { CustomerID = "A301", CustomerName = "Alice", Email = "alice@example.com", CustomerType = TypeOfCustomer.VIPCustomer }
> 			};
> 			
> 			//Add
> 			Customer new_cust = new Customer() { CustomerID = "A456", CustomerName = "Jacob", Email = "jacob@example.com", CustomerType = TypeOfCustomer.VIPCustomer };
> 			customersList.Add(new_cust);
> 			
> 			foreach(Customer customer in customersList)
> 			{
> 				Console.WriteLine(customer.CustomerID + ", " + customer.CustomerName + ", " + customer.Email + ", " + customer.CustomerType);
> 			}
> 		}
> 	}
> }
> ```




























































