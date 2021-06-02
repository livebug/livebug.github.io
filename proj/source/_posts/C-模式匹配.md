---
title: C# 模式匹配
date: 2021-05-25 23:29:03
tags: 
- C#
- 模式匹配
categories: 
- C#
---

<https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/patterns>

C# 在 C# 7.0 中引入了模式匹配。 自此之后，每个主要 C# 版本都扩展了模式匹配功能。 以下 C# 表达式和语句支持模式匹配：

- `is`表达式
- `switch` 语句
- `switch` 表达式（在 C# 8.0 中引入）

在这些构造中，可将输入表达式与以下任一模式进行匹配：

- [声明模式](#声明和类型模式)：用于检查表达式的运行时类型，如果匹配成功，则将表达式结果分配给声明的变量。 在 C# 7.0 中引入。
- [类型模式](#类型模式)：用于检查表达式的运行时类型。 在 C# 9.0 中引入。
- [常量模式](#常量模式)：用于测试表达式结果是否等于指定常量。 在 C# 7.0 中引入。
- [关系模式](#关系模式)：用于将表达式结果与指定常量进行比较。 在 C# 9.0 中引入。
- [逻辑模式](#逻辑模式)：用于测试表达式是否与模式的逻辑组合匹配。 在 C# 9.0 中引入。
- [属性模式](#属性模式)：用于测试表达式的属性或字段是否与嵌套模式匹配。 在 C# 8.0 中引入。
- [位置模式](#位置模式)：用于解构表达式结果并测试结果值是否与嵌套模式匹配。 在 C# 8.0 中引入。
- [var 模式](#var模式)：用于匹配任何表达式并将其结果分配给声明的变量。 在 C# 7.0 中引入。
- [弃元模式](#弃元模式)：用于匹配任何表达式。 在 C# 8.0 中引入。

_逻辑、属性和位置模式都是递归模式。 也就是说，它们可包含嵌套模式。_

有关如何使用这些模式来生成数据驱动算法的示例，请参阅教程：使用模式匹配来生成类型驱动的算法和数据驱动的算法。

## 声明和类型模式

1. IS

```csharp
int? xNullable = 7;
int y = 23;
object yBoxed = y;
if (xNullable is int a && yBoxed is int b)
{
    Console.WriteLine(a + b);  // output: 30
}
```

1. SWITCH

```csharp
public static decimal CalculateToll(this Vehicle vehicle) => vehicle switch
{
    Car => 2.00m,
    Truck => 7.50m,
    null => throw new ArgumentNullException(nameof(vehicle)),
    _ => throw new ArgumentException("Unknown type of a vehicle", nameof(vehicle)),
};
```

## 常量模式

在常量模式中，可使用任何常量表达式，例如：

- integer 或 floating-point 数值文本
- char 或 string 文本
- 布尔值 true 或 false
- enum 值
- 声明常量字段或本地的名称
- null

```csharp
public static decimal GetGroupTicketPrice(int visitorCount) => visitorCount switch
{
    1 => 12.0m,
    2 => 20.0m,
    3 => 27.0m,
    4 => 32.0m,
    0 => 0.0m,
    _ => throw new ArgumentException($"Not supported number of visitors: {visitorCount}", nameof(visitorCount)),
};

input is not null
```

## 关系模式

在关系模式中，可使用关系运算符 <、>、<= 或 >= 中的任何一个。 关系模式的右侧部分必须是常数表达式。 常数表达式可以是 integer、floating-point、char 或 enum 类型。

要检查表达式结果是否在某个范围内，请将其与合取 and 模式匹配，

```csharp
Console.WriteLine(GetCalendarSeason(new DateTime(2021, 3, 14)));  // output: spring
Console.WriteLine(GetCalendarSeason(new DateTime(2021, 7, 19)));  // output: summer
Console.WriteLine(GetCalendarSeason(new DateTime(2021, 2, 17)));  // output: winter

static string GetCalendarSeason(DateTime date) => date.Month switch
{
    >= 3 and < 6 => "spring",
    >= 6 and < 9 => "summer",
    >= 9 and < 12 => "autumn",
    12 or (>= 1 and < 3) => "winter",
    _ => throw new ArgumentOutOfRangeException(nameof(date), $"Date with unexpected month: {date.Month}."),
};
```

## 逻辑模式

从 C# 9.0 开始，可使用 `not`、`and` 和 `or` 模式连结符来创建以下逻辑模式：

and 模式连结符的优先级高于 or。 要显式指定优先级，请使用括号，如以下示例所示：

```csharp
static bool IsLetter(char c) => c is (>= 'a' and <= 'z') or (>= 'A' and <= 'Z');
```

## 属性模式

```csharp
static bool IsConferenceDay(DateTime date) => date is { Year: 2020, Month: 5, Day: 19 or 20 or 21 };

Console.WriteLine(TakeFive("Hello, world!"));  // output: Hello
Console.WriteLine(TakeFive("Hi!"));  // output: Hi!
Console.WriteLine(TakeFive(new[] { '1', '2', '3', '4', '5', '6', '7' }));  // output: 12345
Console.WriteLine(TakeFive(new[] { 'a', 'b', 'c' }));  // output: abc

static string TakeFive(object input) => input switch
{
    string { Length: >= 5 } s => s.Substring(0, 5),
    string s => s,

    ICollection<char> { Count: >= 5 } symbols => new string(symbols.Take(5).ToArray()),
    ICollection<char> symbols => new string(symbols.ToArray()),

    null => throw new ArgumentNullException(nameof(input)),
    _ => throw new ArgumentException("Not supported input type."),
};
```

属性模式是一种递归模式。 也就是说，可以将任何模式用作`嵌套`模式。 使用属性模式将部分数据与嵌套模式进行匹配，如以下示例所示：

```csharp
public record Point(int X, int Y);
public record Segment(Point Start, Point End);

static bool IsAnyEndAtOrigin(Segment segment) =>
    segment is { Start: { X: 0, Y: 0 } } or { End: { X: 0, Y: 0 } };
```

## 位置模式

位置模式来解构表达式结果并将结果值与相应的嵌套模式匹配

```csharp

var numbers = new List<int> { 1, 2, 3 };
if (SumAndCount(numbers) is (Sum: var sum, Count: > 0))
{
    Console.WriteLine($"Sum of [{string.Join(" ", numbers)}] is {sum}");  // output: Sum of [1 2 3] is 6
}

static (double Sum, int Count) SumAndCount(IEnumerable<int> numbers)
{
    int sum = 0;
    int count = 0;
    foreach (int number in numbers)
    {
        sum += number;
        count++;
    }
    return (sum, count);
}

```

## var 模式

```csharp
static bool IsAcceptable(int id, int absLimit) =>
    SimulateDataFetch(id) is var results
    && results.Min() >= -absLimit
    && results.Max() <= absLimit;

static int[] SimulateDataFetch(int id)
{
    var rand = new Random();
    return Enumerable
               .Range(start: 0, count: 5)
               .Select(s => rand.Next(minValue: -10, maxValue: 11))
               .ToArray();
}
```

## 弃元模式

从 C# 8.0 开始，可使用弃元模式 `_` 来匹配任何表达式，包括 null，如以下示例所示

```csharp
Console.WriteLine(GetDiscountInPercent(DayOfWeek.Friday));  // output: 5.0
Console.WriteLine(GetDiscountInPercent(null));  // output: 0.0
Console.WriteLine(GetDiscountInPercent((DayOfWeek)10));  // output: 0.0

static decimal GetDiscountInPercent(DayOfWeek? dayOfWeek) => dayOfWeek switch
{
    DayOfWeek.Monday => 0.5m,
    DayOfWeek.Tuesday => 12.5m,
    DayOfWeek.Wednesday => 7.5m,
    DayOfWeek.Thursday => 12.5m,
    DayOfWeek.Friday => 5.0m,
    DayOfWeek.Saturday => 2.5m,
    DayOfWeek.Sunday => 2.0m,
    _ => 0.0m,
};
```

## 带括号模式

从 C# 9.0 开始，可在任何模式两边加上括号。 通常，这样做是为了强调或更改逻辑模式中的优先级，如以下示例所示：

```csharp
if (input is not (float or double))
{
    return;
}
```
