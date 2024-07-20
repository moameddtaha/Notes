---
tags:
  - Polymorphism
  - Inheritance
  - Abstraction
  - Encapsulation
---

# Key Notes on OOP Concepts and Examples
---

## 1. Encapsulation
---

Encapsulation is the bundling of data and methods that operate on that data within a single unit, typically a class, and restricting access to some of the object's components. This is typically achieved through access modifiers like `private`, `protected`, and `public`.

**Example:**

```Csharp
public class Person
{
    private string name;
    private int age;

    public string Name
    {
        get { return name; }
        set { name = value; }
    }

    public int Age
    {
        get { return age; }
        set
        {
            if (value >= 0)
            {
                age = value;
            }
        }
    }

    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Age: {Age}");
    }
}

// Usage
Person person = new Person();
person.Name = "John";
person.Age = 30;
person.DisplayInfo();  // Outputs: Name: John, Age: 30

```

## 2. Abstraction
---
### **Abstraction vs. Interface**

**Abstraction:**

- Hides complex implementation details and shows only the necessary parts of an object.
- Abstract classes can provide common implementation code and allow defining methods with different access levels (private, protected, etc.).

**Example of Abstract Class:**

```CSharp
public abstract class Vehicle
{
    public abstract void Start();

    public void Stop()
    {
        Console.WriteLine("Vehicle stopped.");
    }
}

public class Car : Vehicle
{
    public override void Start()
    {
        Console.WriteLine("Car started.");
    }
}

public class Motorcycle : Vehicle
{
    public override void Start()
    {
        Console.WriteLine("Motorcycle started.");
    }
}

// Usage
Vehicle myCar = new Car();
myCar.Start();  // Outputs: Car started.
myCar.Stop();   // Outputs: Vehicle stopped.

```

**Interfaces:**

- Can only declare methods and properties, no implementation.
- All members of an interface are implicitly public.

Example of Interface:

```CSharp
public interface IVehicle
{
    void Start();
    void Stop();
}

public class Car : IVehicle
{
    public void Start()
    {
        Console.WriteLine("Car started.");
    }

    public void Stop()
    {
        Console.WriteLine("Car stopped.");
    }
}

public class Motorcycle : IVehicle
{
    public void Start()
    {
        Console.WriteLine("Motorcycle started.");
    }

    public void Stop()
    {
        Console.WriteLine("Motorcycle stopped.");
    }
}

// Usage
IVehicle myCar = new Car();
myCar.Start();  // Outputs: Car started.
myCar.Stop();   // Outputs: Car stopped.

```

## 3. Polymorphism
---
### **Method Overloading (Compile-Time Polymorphism)**

Allows multiple methods with the same name but different parameters.

**Example:**

```CSharp
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }

    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }
}

// Usage
Calculator calc = new Calculator();
Console.WriteLine(calc.Add(2, 3));        // Outputs: 5
Console.WriteLine(calc.Add(2.5, 3.5));    // Outputs: 6.0
Console.WriteLine(calc.Add(1, 2, 3));     // Outputs: 6

```

### **Method Overriding (Runtime Polymorphism)**

Method overriding allows a subclass to provide a specific implementation of a method that is already defined in its superclass. It is used to achieve runtime polymorphism.

**Example:**

```CSharp
public class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("Animal sound");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Bark");
    }
}

public class Cat : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Meow");
    }
}

// Usage
Animal myDog = new Dog();
myDog.MakeSound();  // Outputs: Bark

Animal myCat = new Cat();
myCat.MakeSound();  // Outputs: Meow

```





**Difference Between Variable Declarations:**

**1. `Animal myDog = new Dog();`**:

- Declares `myDog` as type `Animal` but instantiates it as `Dog`.
- Can call methods defined in `Animal`, including overridden methods in `Dog`.
- Cannot call methods unique to `Dog` unless cast back to `Dog`.


**Example:**

```CSharp
Animal myDog = new Dog();
myDog.Eat();       // Outputs: Animal is eating (method from Animal)
myDog.MakeSound(); // Outputs: Bark (overridden method in Dog)
// myDog.Fetch();  // Error: 'Animal' does not contain a definition for 'Fetch'

// Casting to Dog to access Fetch method
Dog specificDog = (Dog)myDog;
specificDog.Fetch(); // Outputs: Dog is fetching

```

**2. `Dog realDog = new Dog();`**:

- Declares and instantiates `realDog` as type `Dog`.
- Can call all methods defined in `Dog`, including those inherited from `Animal` and methods unique to `Dog`.

**Example:**

```CSharp
Dog realDog = new Dog();
realDog.Eat();       // Outputs: Animal is eating (method from Animal)
realDog.MakeSound(); // Outputs: Bark (overridden method in Dog)
realDog.Fetch();     // Outputs: Dog is fetching

```

