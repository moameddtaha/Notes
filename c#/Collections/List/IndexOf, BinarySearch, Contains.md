---
tags:
  - Property
  - Method
Links:
  - "[[List]]"
---

# IndexOf()
---
>[!Hint]
>1. Perform Linear Search.
>2. Once it found a match it stops at the first occurrence.
>3. `startIndex` parameter is optional.

![[Pasted image 20231219065042.png]]

![[Pasted image 20231219070245.png]]

```CSharp

// Search for 1st occurrence
List<int> myList = new List<int>() {10,20,30,40,50,40};

int numberToBeFound = 40;
int n1 = myList.IndexOf(numberToBeFound);
if(n1 >= 0){
	Console.WriteLine($"{numberToBeFound} found at index: {n1}");
}else{
	Console.WriteLine($"{numberToBeFound} not found");
}

// Search for 2st occurrence
int n2 = myList.IndexOf(numberToBeFound, n1 + 1);
if(n2 >= 0){
	Console.WriteLine($"{numberToBeFound} found at index: {n2}");
}else{
	Console.WriteLine($"{numberToBeFound} not found");
}

```


# BinarySearch()
---
>[!info] References
>[[Binary Search]]

>[!Hint]
>The collection must be pre-sorted.

![[Pasted image 20231219073434.png]]

![[Pasted image 20231219073249.png]]

# Contains()
---

> [!NOTE] Title
> It compare the references of the two objects

![[Pasted image 20231219073747.png]]

```CSharp
List<int> myList = new List<int>() {10,20,30};
bool check = myList.Comtains(20);
if(check){
	Console.WriteLine("Found");
}else{
	Console.WriteLine("Not found");
}
```
























































