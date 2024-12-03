---
title: "Who Decides What's More Important: Code Readability or Efficiency?"
seoTitle: "Balancing Code Readability, Maintainability, and Efficiency?"
seoDescription: "Explore the balance between code readability, maintainability, & efficiency through a practical analysis of two solutions to a password validator challenge."
datePublished: Sat Jul 13 2024 01:14:26 GMT+0000 (Coordinated Universal Time)
cuid: clyjfp28u00050al6fp5l6c1m
slug: mmrp
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720833238384/f6c511b2-9539-4ec2-bfcb-4d337e0bf019.png
tags: oop, csharp, performance, modularity, console, clean-code, maintainability, separation-of-concerns, codenewbies, coding-journey, single-responsibility-principle, readability

---

In software development, striking a balance between code readability, maintainability, and efficiency is crucial. Recently, I worked on a password validator challenge from Level 24 of [RB Whitaker's The C# Player's Guide (5th Edition)](https://csharpplayersguide.com/)that made me ponder on this topic.

### The Challenge

The task was to create a class that determines if a password meets specific rules as follows:

1. Passwords must be at least 6 characters long and no more than 13 characters long.
    
2. Passwords must contain at least one uppercase letter, one lowercase letter, and one number.
    
3. Passwords cannot contain the capital letter 'T' or the ampersand '&'.
    

### Standard Solution

(Solution from: [https://csharpplayersguide.com/solutions/5th-edition/the-password-validator](https://csharpplayersguide.com/solutions/5th-edition/the-password-validator) )

The standard solution uses a `PasswordValidator` class with a main validation method and several helper methods:

```csharp
public class PasswordValidator
{
    public bool IsValid(string password)
    {
        if (password.Length < 6) return false;
        if (password.Length > 13) return false;
        if (!HasUppercase(password)) return false;
        if (!HasLowercase(password)) return false;
        if (!HasDigits(password)) return false;
        if (Contains(password, 'T')) return false;
        if (Contains(password, '&')) return false;

        return true;
    }

    private bool HasUppercase(string password)
    {
        foreach (char letter in password)
            if (char.IsUpper(letter)) return true;

        return false;
    }

    private bool HasLowercase(string password)
    {
        foreach (char letter in password)
            if (char.IsLower(letter)) return true;

        return false;
    }

    private bool HasDigits(string password)
    {
        foreach (char letter in password)
            if (char.IsDigit(letter)) return true;

        return false;
    }

    private bool Contains(string password, char letter)
    {
        foreach (char character in password)
            if (character == letter) return true;

        return false;
    }
}

class Program
{
    static void Main()
    {
        PasswordValidator validator = new PasswordValidator();
        while (true)
        {
            Console.Write("Enter a password: ");
            string? password = Console.ReadLine();
        
            if (password == null) break; 
        
            if (validator.IsValid(password)) Console.WriteLine("That password is valid.");
            else Console.WriteLine("That password is not valid.");
        }    
    }
}
```

### My Solution

For my approach, I designed a simpler `PasswordValidator` class that encapsulates the password and performs validation within a single method:

```csharp
class PasswordValidator
{
    public string Password { get; }

    public PasswordValidator(string password)
    {
        Password = password;
    }

    public bool isValid()
    {
        int countLetters = 0, upperCases = 0, lowerCases = 0, digits = 0;
        bool hasForbiddenchar = false;
        foreach (char letter in Password)
        {
            countLetters++;
            if(char.IsUpper(letter)) upperCases++;
            if (char.IsLower(letter)) lowerCases++;
            if (char.IsDigit(letter)) digits++;
            if (letter == 'T' || letter == '&') hasForbiddenchar = true;
        }
        if (countLetters >= 6 && countLetters <= 13 && upperCases >= 1 && lowerCases >= 1 && digits >= 1 && !hasForbiddenchar) return true;
        else return false;
    }
}

class Program
{
    static void Main()
    {
        // Boss Battle 5 - The Password Validator
        while (true)
        {
            Console.Write("Enter a password: ");
            string? password = Console.ReadLine();
            if (password == null) break;
            PasswordValidator user = new PasswordValidator(password);
            if (user.isValid()) Console.WriteLine("This password is valid.");
            else Console.WriteLine("This password is not allowed.");
        }    
    }
}
```

### The Comparison

I asked Chat-GPT to compare the two solutions in terms of modularity, readability, performance and maintainability:

| Aspect | Standard Solution | My Solution |
| --- | --- | --- |
| ***Modularity*** | High (separate helper methods) | Low (all logic in a single method) |
| ***Readability*** | High (clear separation of concerns) | Medium (more compact but harder to follow) |
| ***Performance*** | Medium (multiple iterations) | High (single iteration) |
| ***Maintainability*** | High (easier to update individual parts) | Medium (updating logic requires changing the main method) |

### My Questions

How exactly is a trade-off achieved between these aspects? Who determines what is more important when one or more are to be sacrificed?

The standard solution is objectively better, as shown. However, in a real-world setting, working with a team, which trade-offs would be made? Is there any instance where my solution would be considered better? In a coding assessment for a job interview, for example, how would my solution be evaluated?

I would love to hear your thoughts if you have any! 😊✨