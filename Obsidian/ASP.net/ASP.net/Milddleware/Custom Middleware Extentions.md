---
tags:
  - Asp_Net_Core
  - Middleware
  - Extension
  - Methods
---

## Extension Method
---

An extension method is a special kind of static method in C# that allows you to add new methods to existing types without modifying the original type. Extension methods are defined in static classes and use the `this` keyword in the parameter list to specify the type they extend.

### Key Points

- **Static Method**: Extension methods must be static.
- **Static Class**: They must be contained within a static class.
- **`this` Keyword**: The first parameter of the method specifies the type it extends and uses the `this` keyword.

#### Example

Suppose you want to add a method to the `string` class that repeats the string a specified number of times. You can do this using an extension method:

Defining an Extension Method
```CSharp
public static class StringExtensions
{
    public static string Repeat(this string str, int count)
    {
        if (count < 0)
            throw new ArgumentOutOfRangeException(nameof(count), "Count cannot be less than zero.");

        if (string.IsNullOrEmpty(str) || count == 0)
            return string.Empty;

        StringBuilder result = new StringBuilder(str.Length * count);
        for (int i = 0; i < count; i++)
        {
            result.Append(str);
        }
        return result.ToString();
    }
}
```

Using an Extension Method
```CSharp
class Program
{
    static void Main()
    {
        string hello = "Hello";
        string result = hello.Repeat(3);
        Console.WriteLine(result); // Output: HelloHelloHello
    }
}
```

##### Explanation

- **Static Class**: `StringExtensions` is a static class containing the extension method.
- **Static Method**: `Repeat` is a static method.
- **`this` Keyword**: The `this` keyword before the `string str` parameter indicates that this method extends the `string` type.

### Benefits

- **Cleaner Code**: Allows you to call the method as if it were a member of the type, resulting in cleaner and more readable code.
- **Non-Intrusive**: You can add functionality to existing types without modifying them or creating derived types.

Extension methods are widely used in LINQ and ASP.NET Core middleware to extend the functionality of built-in types and interfaces.


