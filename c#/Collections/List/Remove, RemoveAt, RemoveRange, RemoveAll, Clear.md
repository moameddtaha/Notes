---
tags:
  - Property
  - Method
Links:
  - "[[List]]"
---




# Remove()
---

>[!Hint]
>The methods returns a Boolean value indicating whether the value is removed or not, in case if the value founds it returns true and in case the value not found it return false.

![[Pasted image 20231219045439.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30};

// Remove 30
myList.Remove(30);
```

```CSharp
using System;
using System.Collections.Generic;

// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30};

// Remove 30 and cheking if it's exists.
bool check = myList.Remove(30);
if(check){
	Console.WriteLine("Exists");
}else{
	Console.WriteLine("Doesn't exist");
}
```


# RemoveAt()
---

>[!Hint]
>When you know the index of the value you want to remove.

![[Pasted image 20231219050527.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30,40,50};

// Remove at index 2 (30)
// It's always a good practice to check if the index exists before attempt to remove the element in it.
int index = 5;
if(index < myList.Count)
	myList.RemoveAt(index);
```


# RemoveRange()
---

![[Pasted image 20231219051046.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30,40,50};

// Remove range starts from index 1 and the count is 2 elements
myList.RemoveRange(1, 2) // List: 10,40,50

```

# RemoveAll()
---

>[!info] References
[[Lambda Expressions]] 
[[Predicate]] 

>[!Hint]
>It deletes the elements with condition and it returns an integer representing the number of elements that were removed from the `List<T>` based on the specified condition.

![[Pasted image 20231219051523.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30,40,50};

// Remove all numbers >= 30
// It will execute more than one time.
int removedCount = myList.RemoveAll(n => n >= 30);

if (removedCount > 0)
{
    Console.WriteLine($"{removedCount} elements were removed.");
}
else
{
    Console.WriteLine("No elements were removed.");
}
```


# Clear
---

>[!Hint]
>It deletes the elements without condition.

![[Pasted image 20231219052508.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>();

myList.Clear();
myList.Add(100);
myList.Add(200);
myList.Add(300);
```































