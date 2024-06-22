---
tags:
  - Handling_Null
Links: "[[Value Types & Reference Types]]"
---

# Null Propagation Operator
---

![[Pasted image 20231205040338.png]]
> It is used to check if a reference variable is not equal to `null` before accessing a property or invoking a method on that variable. If the variable is `null`, the entire expression evaluates to `null` without throwing a `NullReferenceException` and it will return property or method if it's not equal to null.

Here's an example:

```CSharp
class Person
{
    public string Name { get; set; }
}

class Program
{
    static void Main()
    {
        Person person = GetPerson();

        // Using ?. to avoid NullReferenceException
        string personName = person?.Name;

        if (personName != null)
        {
            Console.WriteLine($"Person's name: {personName}");
        }
        else
        {
            Console.WriteLine("Person is null");
        }
    }

    static Person GetPerson()
    {
        // Simulating a case where the person object might be null
        return null;
    }
}

```


