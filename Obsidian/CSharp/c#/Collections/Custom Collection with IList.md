---
tags:
  - Generic
---

# Custom Collection with IList
---

![[Pasted image 20240102010451.png]]

## Example(s)
---

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.

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

> [!example] Custom collection with IList
> ```CSharp
> using System;
> using System.Collections.Generic;
> using System.Collections;
> 
> namespace CustomCollections
> {
> 	//custom collection class
> 	public class CustomersList : IList\<Customer>
> 	{
> 		//private collection as a field
> 		private List\<Customer> customers = new List\<Customer>();
> 		
> 		public int Count => customers.Count;
> 		
> 		public bool IsReadOnly => false;
> 		
> 		public Customer this[int index]
> 		{
> 			get => customers[index];
> 			set => customers[index] = value;
> 		}
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
> 		
> 		public void Clear()
> 		{
> 			customers.Clear();
> 		}
> 		
> 		public bool Contains(Customer item)
> 		{
> 			return customers.Contains(item);
> 		}
> 		
> 		public void CopyTo(Customer[] array, int arrayIndex)
> 		{
> 			customers.CopyTo(array, arrayIndex);
> 		}
> 		
> 		public bool Remove(Customer item)
> 		{
> 			return customers.Remove(item);
> 		}
> 		
> 		public Customer Find(Predicate\<Customer> match)
> 		{
> 			return customers.Find(match);
> 		}
> 		
> 		public List\<Customer> FindAll(Predicate\<Customer> match)
> 		{
> 			return customers.FindAll(match);
> 		}
> 		
> 		public int IndexOf(Customer item)
> 		{
> 			return customers.IndexOf(item);
> 		}
> 		
> 		public void Insert(int index, Customer item)
> 		{
> 			if (index < 0)
> 			{
> 				Console.WriteLine("Invalid index");
> 			}
> 			else
> 			{
> 				customers.Insert(index, item);
> 			}
> 		}
> 		
> 		public void RemoveAt(int index)
> 		{
> 			if (index < 0)
> 			{
> 				Console.WriteLine("Invalid index");
> 			}
> 			else
> 			{
> 				customers.RemoveAt(index);
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
> 			//Contains
> 			Console.WriteLine("Contains: " + customersList.Contains(new_cust));
> 			Console.WriteLine(customersList.Count + " customers found.");
> 			
> 			//Remove
> 			customersList.Remove(new_cust);
> 			foreach(Customer customer in customersList)
> 			{
> 				Console.WriteLine(customer.CustomerID + ", " + customer.CustomerName + ", " + customer.Email + ", " + customer.CustomerType);
> 			}
> 			
> 			//Find
> 			Customer matchingCustomer = customersList.Find(cust => cust.CustomerID == "A101");
> 			if (matchingCustomer != null)
> 			{
> 				Console.WriteLine(matchingCustomer.CustomerID + ", " + matchingCustomer.CustomerName);
> 			}
> 			
> 			//FindAll
> 			List\<Customer> vipcust = customersList.FindAll(cust => cust.CustomerType == TypeOfCustomer.VIPCustomer);
> 			Console.WriteLine("\nVIP customers:");
> 			foreach (Customer customer in vipcust)
> 			{
> 				Console.WriteLine(customer.CustomerID + ", " + customer.CustomerName + ", " + customer.Email + ", " + customer.CustomerType);
> 			}
> 			
> 			//IndexOf
> 			Console.WriteLine("IndexOf: " + customersList.IndexOf(new_cust));
> 			
> 			//Insert
> 			customersList.Insert(2, new_cust);
> 			
> 			//Indexer
> 			Console.WriteLine(customersList[2].CustomerID + ", " + customersList[2].CustomerName);
> 			
> 			customersList.Clear();
> 		}
> 	}
> }
> ```








































































