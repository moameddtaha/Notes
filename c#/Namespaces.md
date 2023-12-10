---
tags:
  - Namespaces
---
# Namespaces
---

![[Pasted image 20231202205315.png]]

![[Pasted image 20231202205359.png]]


# Nested Namespaces
---

![[Pasted image 20231202205942.png]]


# 'using' Alias Name
---

![[Pasted image 20231202213917.png]]


> You can also create an alias for a namespace or a type with a _using alias directive_. [Microsoft Page](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive)

```CSharp
using Project = PC.MyCompany.Project;
```

# 'using static' directive
---
![[Pasted image 20231202214309.png]]


> The `using static` directive names a type whose static members and nested types you can access without specifying a type name. Its syntax is: [Microsoft Page](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive)

```CSharp
using static <fully-qualified-type-name>;
```

> You can access static members of a type without having to qualify the access with the type name:
```CSharp
using static System.Console;
using static System.Math;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4));
    }
}
```



