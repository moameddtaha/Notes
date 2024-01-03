---
tags:
  - Property
  - Method
Links:
  - "[[List]]"
---

# Add()
---

![[Pasted image 20231219042006.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30};

// Add new element at the end of existing collection
myList.Add(40);
```


# AddRange()
---

![[Pasted image 20231219042832.png]]

```CSharp
// Create refrence variable for List class & create object of list class
List<int> myList = new List<int>() {10,20,30};

// Add new element at the end of existing collection
myList.Add(40);

// Another collection
List<int> otherList = new List<int>() {50,60,70};

// Adding another collection to existing collection
myLiat.AddRange(otherList);
```






















