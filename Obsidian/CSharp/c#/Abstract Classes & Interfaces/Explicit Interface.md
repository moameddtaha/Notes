---
tags:
  - Interfaces
Links:
  - "[[Interfaces]]"
---

# Explicit Interface
---

![[Pasted image 20231202052749.png]]

![[Pasted image 20231202052935.png]]

![[Pasted image 20231202053406.png]]

![[Pasted image 20231202053600.png]]

> An explicit interface implementation doesn't have an access modifier since it isn't accessible as a member of the type it's defined in. Instead, it's only accessible when called through an instance of the interface. If you specify an access modifier for an explicit interface implementation, you get compiler error [CS0106](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-messages/cs0106). For more information, see [`interface` (C# Reference)](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface). [Microsoft Page](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation) 


```CSharp
public class SampleClass : IControl, ISurface
{
    void IControl.Paint()
    {
        System.Console.WriteLine("IControl.Paint");
    }
    void ISurface.Paint()
    {
        System.Console.WriteLine("ISurface.Paint");
    }
}
```

> The class member `IControl.Paint` is only available through the `IControl` interface, and `ISurface.Paint` is only available through `ISurface`. Both method implementations are separate, and neither are available directly on the class. For example:

```CSharp
SampleClass sample = new SampleClass();
IControl control = sample;
ISurface surface = sample;

// The following lines all call the same method.
//sample.Paint(); // Compiler error.
control.Paint();  // Calls IControl.Paint on SampleClass.
surface.Paint();  // Calls ISurface.Paint on SampleClass.

// Output:
// IControl.Paint
// ISurface.Paint
```



