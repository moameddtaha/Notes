---
tags:
  - Property
  - Method
Links:
  - "[[List]]"
---

# ToArray()
---

![[Pasted image 20231219104714.png]]

```CSharp
// Create a List
List<string> myFriends = new List<string>() {"Scott", "Allen", "James", "John"};

// Convert to array
string[] myFriendsArray = myFriends.ToArray();
```


# ForEach()
---

>[!info] References
>[[Lambda Expressions]]
>[[Action]]

![[Pasted image 20231219105939.png]]

```CSharp
// Create a List
List<string> myFriends = new List<string>() {"Scott", "Allen", "James", "John"};

// ForEach method
myFriends.ForEach(freind => 
{
	Console.WriteLine(freind);
}
);
```





























