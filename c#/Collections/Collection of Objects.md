---
tags:
  - Collection
---

# Collection of Objects
---
![[Pasted image 20231225145336.png]]

## Example(s)
---

>[!info]
>
>In C#, we use XML Comments **to create documentation of classes and their members**. XML Documentation helps other programmers or developers to use your code (classes, functions and their members) easily by providing some useful information. [Recommended XML tags for C# documentation comments - Microsoft Page](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/recommended-tags)
>
>![[Pasted image 20231225151304.png]]
>

>[!error]
> In the following example(s) you need to remove the character `\` that is located before most of the `<` character(s) to not get any error.

>[!Example]- Product Class
>
>```CSharp
>
>using System;
>namespace ECommerce
>{
>	/// \<summary>
>	/// Represents a Product in ECommerce application
>	/// \</summary>
>	
>	public class Product
>	{
>		//properties
>		public int ProductID { get; set; }
>		public string ProductName { get; set; }
>		public double Price { get; set; }
>		public DateTime DateOfManufacture { get; set; }
>	}
>}

>[!Example] Main Method
>
>```CSharp
>
>using System;
>using ECommerce;
>using System.Collections.Generic;
>
>namespace CollectionOfObjectsExample
>{
>	class Program
>	{
>		static void Main()
>		{
>			 //create an empty collection
>			 List\<Product> products = new List\<Product>();
>			 
>			 //loop to read data from user
>			 string choice;
>			 do
>			 {
>				 Console.Write("Enter Product ID: ");
>				 int pid = int.Parse(Console.ReadLine());
>				 Console.Write("Enter Product Name: ");
>				 string pname = Console.ReadLine();
>				 Console.Write("Enter Price: ");
>				 double unitPrice = double.Parse(Console.ReadLine());
>				 Console.Write("Enter Date of Manufacture (yyyy-MM-dd): ");
>				 DateTime dom = DateTime.Parse(Console.ReadLine());
>				 
>				 //Create a new object of Product class
>				 Product product = new Product() { ProductID = pid, ProductName = pname, Price = unitPrice, DateOfManufacture = dom };
>				 
>				 //Add Product object to the collection
>				 products.Add(product);
>				 
>				 //Ask the user to continue
>				 Console.WriteLine("Product Added.\n");
>				 Console.WriteLine("Do you want to continue to next product? (Yes/No)");
>				 choice = Console.ReadLine();
>			 
>			 } while (choice != "No" && choice != "no" && choice != "n" && choice != "N");
>			 
>			 //foreach
>			 Console.WriteLine("\nProducts:");
>			 foreach (Product item in products)
>			 {
>				 Console.WriteLine(item.ProductID + ", " + item.ProductName + ", " + item.Price + ", " + item.DateOfManufacture.ToShortDateString());
>			 }
>			 
>			 Console.ReadKey();
>		 }
>	 }
> }
> ```








