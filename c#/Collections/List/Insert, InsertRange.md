---
tags:
  - Property
  - Method
Links:
  - "[[List]]"
---


# Insert()
---

![[Pasted image 20231219043618.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30};

// insert element at position 1
myList.Insert(1, 100); // List Values: 10, 100, 20, 30
```


# InsertRange()
---

>[!error] Mistake
>There is a little bit of mistake in the following image.
>`value2` shouldn't be removed after the new values inserted.

![[Pasted image 20231219044422.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30};

// insert element at position 1
myList.Insert(1, 100); // List Values: 10, 100, 20, 30

// Another collection
List<int> otherList = new List<int>() {200,300,400};

// insert element at position 2                             ->
myLiat.InsertRange(2, otherList); // List Values: 10, 100, 200, 300, 400, 20, 30
```














