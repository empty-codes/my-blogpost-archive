---
title: "Why Is Shadowing In C# An Issue?"
seoTitle: "Understanding Shadowing in C#: How to Avoid Name Hiding Issues"
seoDescription: "Learn about shadowing in C#, also known as name hiding, and discover solutions to prevent common coding pitfalls."
datePublished: Sun Aug 18 2024 12:36:43 GMT+0000 (Coordinated Universal Time)
cuid: clzzjx5aj001y09mb0j4n5uvn
slug: why-is-shadowing-in-c-an-issue
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723984350957/65a4c983-77aa-4a29-9ed4-4bd2744d8f77.jpeg
tags: csharp, constructor, methods, this-keyword, shadowing, namehiding, methodparameters

---

Shadowing, also known as name hiding, occurs when a parameter name in a method or constructor matches the name of a field in the class. This overlap causes the parameter to "hide" the class field, making it difficult to access the intended field within that scope.

Consider the following example:

```csharp
public class Score
{
    public string name;
    public int points;
    public int level;

    public Score(string name, int points, int level)
    {
        name = name; // This will not do what you want!
        points = points;
        level = level;
    }
}
```

At first glance, it might seem like the constructor assigns the values of `name`, `points`, and `level` to the respective class fields. However, due to shadowing, all these assignments are actually self-references. The `name = name;` line assigns the value of the `name` parameter back to itself, leaving the class field `name` unchanged.

### Why is This a Problem?

This issue can lead to bugs where the class fields remain uninitialized or retain default values, even though it appears that they were assigned properly. This can be especially confusing during debugging or code reviews, as the code seems correct but doesn't behave as expected.

### Solutions

#### 1\. Use Different Variable Names

Avoid using the same names for parameters and fields. A common convention in C# is to prefix field names with an underscore (`_`). This helps distinguish between class fields and method parameters:

```csharp
public class Score
{
    public string _name;
    public int _points;
    public int _level;

    public Score(string name, int points, int level)
    {
        _name = name;
        _points = points;
        _level = level;
    }
}
```

In this approach, `_name`, `_points`, and `_level` are clearly identified as class fields, while `name`, `points`, and `level` are method parameters.

#### 2\. Use the `this` Keyword

`this` refers to the current instance of the class, allowing you to explicitly specify that you're accessing the class field rather than a method parameter:

```csharp
public class Score
{
    public string name;
    public int points;
    public int level;

    public Score(string name, int points, int level)
    {
        this.name = name;
        this.points = points;
        this.level = level;
    }
}
```

In this example, [`this.name`](http://this.name), `this.points`, and `this.level` clearly refer to the class fields, while the right-hand side refers to the parameters.

### Conclusion

Name hiding in C# can lead to confusing and incorrect code when method parameters and class fields share the same names. By either using different variable names or the `this` keyword, you can ensure that your code behaves as intended and remains easy to read and maintain.

If you read this till the end, I hope you have learned something useful! 😊✨