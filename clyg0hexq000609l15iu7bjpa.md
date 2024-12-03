---
title: "User Input and Enums in C#"
seoTitle: "Enums in C#: Definition, Usage, and Handling User Input"
seoDescription: "Explore practical examples for defining enums, handling user input, and leveraging numeric options, ideal for beginners and experienced developers alike."
datePublished: Wed Jul 10 2024 15:45:16 GMT+0000 (Coordinated Universal Time)
cuid: clyg0hexq000609l15iu7bjpa
slug: user-input-and-enums-in-c
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720626418511/cf202934-ce37-4046-91fd-87c65ae79546.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720626178572/30646d9e-379e-4714-ae6a-a2747885be6a.jpeg
tags: oop, csharp, net, input, enum, types, codingnewbies, enumeration, consoleapp, input-validation, enum-for-beginners

---

An enumeration (enum) in C# is a custom type used when you need to make a choice from a set of possible options. Enums are ideal for representing things that don't fit into one of C#'s default or pre-existing types.

### Creating an Enum

The syntax to create an enum is simple:

```csharp
enum DaysOfTheWeek { Monday, Tuesday, Wednesday, Thursday, Friday }
```

Enums can be defined after the main method in your program. Here’s an example of defining and using an enum in a simple C# program:

```csharp
using System;

namespace ConsoleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            DaysOfTheWeek day;
            day = DaysOfTheWeek.Monday;
            Console.WriteLine($"Today is {day}");
        }
    }

    enum DaysOfTheWeek { Monday, Tuesday, Wednesday, Thursday, Friday }
}
```

### Declaring and Defining Variables with Enums

Enums are data types, meaning they can be used to declare and define variables, just like `string`, `int`, `bool`, and so on.

```csharp
DaysOfTheWeek today = DaysOfTheWeek.Monday;
```

### Getting User Input for an Enum Type

When solving practice questions on enums and classes, I needed to get user input and compare it to an enum value. At first, it seemed confusing, but I figured out multiple ways to do so. Here are 3 ways:

1. #### Using Numeric Input
    

Each enumeration has an underlying type, which is the integer type that it builds upon. Each enumeration member is assigned an `int` value. By default, these are given in the order they appear in the definition, starting with 0. For example, below, Monday is 0, Tuesday is 1, and so on.

```csharp
enum DaysOfTheWeek { Monday, Tuesday, Wednesday, Thursday, Friday }
```

You can assign custom numbers too, but note that any enumeration member without an assigned number is automatically given the one after the member before it.

Since the underlying type of an enum is `int`, you can use explicit casting if you need numeric input.

```csharp
Console.Write("Enter a number for the day of the week (0 for Monday, 1 for Tuesday, etc.): ");
int input = int.Parse(Console.ReadLine());
DaysOfTheWeek day = (DaysOfTheWeek)input;
Console.WriteLine($"You selected {day}");
```

2. #### Using `Enum.TryParse`
    

The `Enum.TryParse` method in C# is used to convert a string to the corresponding enum value.

Here's how you can use `Enum.TryParse` to get user input:

```csharp
using System;

namespace ConsoleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter a day of the week: ");
            if (Enum.TryParse<DaysOfTheWeek>(Console.ReadLine(), true, out DaysOfTheWeek day))
            {
                Console.WriteLine($"You selected {day}");
            }
            else
            {
                Console.WriteLine("Invalid day entered.");
            }
        }
    }

    enum DaysOfTheWeek { Monday, Tuesday, Wednesday, Thursday, Friday }
}
```

`Enum.TryParse` returns a boolean indicating whether the parsing was successful or not, not the parsed enum value directly. The correct parsed enum value is provided via the `out` parameter.

There is a potential problem with this method: if the user input matches one of the enum names (case-insensitively, because the `true` parameter is used), it will successfully convert the input into the enum value and assign it to `aInput`. If the input does not match any of the enum names, `Enum.TryParse` will return `false`, and `aInput` will be set to the default value of the enum type (which is typically the first value in the enum declaration, unless explicitly set).

To ensure that the user types in one of the specified strings, you need to add a validation loop. Here's an example of how you can do this by using the `Enum.IsDefined` method to check if the parsed value is a valid enum value.

```csharp
ArrowHead aInput;
while (true)
{
    Console.WriteLine("'steel', 'wood', or 'obsidian' arrowhead? ");
    string input = Console.ReadLine();
    
    if (Enum.TryParse<ArrowHead>(input, true, out aInput) && Enum.IsDefined(typeof(ArrowHead), aInput))
    {
        break;
    }
    else
    {
        Console.WriteLine("Invalid input. Please type 'steel', 'wood', or 'obsidian'.");
    }
}

enum ArrowHead { Steel, Wood, Obsidian }
```

3. #### Using Strings and Switch Statements
    

You can collect input as a string normally, then use a switch statement with string names as cases to match each enum type:

```csharp
using System;

namespace ConsoleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter a material type (plastic, wood, steel): ");
            string input = Console.ReadLine();
            Fletching material = input switch
            {
                "plastic" => Fletching.Plastic,
                "wood" => Fletching.Wood,
                "steel" => Fletching.Steel,
                _ => Console.WriteLine("Error, please input a valid option.")
            };
            Console.WriteLine($"You selected {material}");
        }
    }

    enum Fletching { Plastic, Wood, Steel }
}
```

Using enums in C# helps create more readable and maintainable code by clearly defining a set of related constants. By following these methods, you can effectively use enums for various input and comparison tasks in your programs.

If you read this till the end, I hope you have learned something useful! 😊✨