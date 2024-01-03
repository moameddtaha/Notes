---
tags:
  - Property
  - Method
Links:
  - "[[List]]"
  - "[[Lambda Expressions]]"
---


# ConvertAll()
---

>[!Tip]
>You can use inline Lambda Expression or Regular Lambda Expression but in that case yo must return the value.

![[Pasted image 20231219183228.png]]

```CSharp
// Create a List
List<int> intCollection = new List<int>() {1,2,3};

List<string> strCollection = intCollection.ConvertAll<string>(n => {
	string word;
	switch(n)
	{
		case 1:
			word = "One";
			break;
		case 2:
			word = "Two";
			break;
		case 3:
			word = "Three";
			break;
		default:
			return "";
			break;
	}
	return word;
});

strCollection.ForEach(n => {Console.WriteLine(n);});
```






















