---
tags:
  - Collection
  - Generic
---

# List
---

![[Pasted image 20231218223805.png]]

![[Pasted image 20231219035354.png]]

![[Pasted image 20231219035511.png]]

>[!Hint]
>If you're aware of the initial capacity your list will have, consider initializing the list with that capacity. This can significantly enhance performance by allocating the required memory upfront, avoiding unnecessary resizing as elements are added. Optimal initialization is particularly beneficial when dealing with large datasets or frequent additions to the list.
>
>![[Pasted image 20231219040427.png]]

``` CSharp
// Example with initial capacity
int initialCapacity = 100; // Set your desired initial capacity
List<int> myList = new List<int>(initialCapacity);
```


![[Pasted image 20231219040552.png]]



















