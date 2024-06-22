---
tags:
  - Property
  - Method
Links:
  - "[[List]]"
  - "[[Lambda Expressions]]"
  - "[[Predicate]]"
---

# Exists()
---

> [!example] Case Scenario
> You might use this in situations where you want to quickly check if there is any element in a list that satisfies a specific condition before performing further actions. For example, you might want to know if there is any number less than a certain threshold, and based on the result, you could decide to take different actions in your program.

![[Pasted image 20231219111851.png]]

```CSharp
// Create a List
List<int> marks = new List<int>() {40,95,74,23,50,81};

bool exists = marks.Exists(m => m < 35);

if(exists){
	Console.WriteLine("Failed in one or more subjects");
}
else{
	Console.WriteLine("Passed");
}
```

# Find()
---

> [!example] Case Scenario
> 1. **Locating an Element:** Use `Find` when you want to find the first element in a collection that matches a specific condition.
> 2. **Conditional Search:** If you need the first occurrence that satisfies a certain condition, `Find` can be more efficient than using other methods, especially if you only need to find one element.
> 3. **First Occurrence Check:** Determine if there is an element in the collection that meets a specific criterion and take appropriate action based on the result.

![[Pasted image 20231219112926.png]]

```CSharp
// Create a List
List<int> marks = new List<int>() {40,95,74,23,50,30,81};

// I want to get teh first matching element
int firstFind;

firstFind = marks.Find(m => m < 35);
Console.WriteLine($"{firstFind}"); // output: 23


firstFind = marks.Find(m => m < 10);
Console.WriteLine($"{firstFind}"); // output: 0 {The default value of int datatype}

```

# FindIndex()
---

![[Pasted image 20231219180326.png]]

```CSharp
// Create a List
List<int> marks = new List<int>() {40,95,74,23,50,30,81};

// I want to get teh first matching element
int firstFind;

firstFind = marks.FindIndex(m => m < 35);
Console.WriteLine($"{firstFind}"); // output: 3


firstFind = marks.Find(m => m < 10);
Console.WriteLine($"{firstFind}"); // output: -1

```


# FindLast()
---

![[Pasted image 20231219181250.png]]

```CSharp
// Create a List
List<int> marks = new List<int>() {40,95,74,23,50,30,81};

// I want to get teh first matching element
int lastElement;

lastElement = marks.FindLastIndex(m => m < 35);
Console.WriteLine($"{lastElement}"); // output: 30

```

# FindLastIndex()
---

![[Pasted image 20231219182001.png]]

```CSharp
// Create a List
List<int> marks = new List<int>() {40,95,74,23,50,30,81};

// I want to get teh first matching element
int lastIndex;

lastIndex = marks.FindLastIndex(m => m < 35);
Console.WriteLine($"{lastIndex}"); // output: 5

```

# FindAll()
---

![[Pasted image 20231219182124.png]]

```CSharp
// Create a List
List<int> marks = new List<int>() {40,95,74,23,50,30,81};

// I want to get teh first matching element
List<int> findAll = marks.FindAll(m => m < 35);

findAll.ForEach(find => 
{
	Console.WriteLine($"{find} \n");
}
);
```






























































