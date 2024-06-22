---
tags:
  - Handling_Null
Links: "[[Value Types & Reference Types]]"
---

# Nullable Types
---

![[Pasted image 20231205033340.png]]

![[Pasted image 20231205035217.png]]
> When you convert the non-nullable value type into nullable, it contains an additional property called `HasValue`, The `HasValue` becomes true if it's not equal to null and false it it's equal to null. 

> You can access the actual value of the field by using `Value` property. The `Value` property gives you the actual value of the nullable type. So if you want copy the value into another `int` variable (non-nullable), you must use the `Value` property in order to access the actual `int` value inside the nullable type.



















