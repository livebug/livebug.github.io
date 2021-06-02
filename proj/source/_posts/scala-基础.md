---
title: Scala 基础
date: 2021-04-25 23:10:00
tags:
- Scala
- 大数据

categories: 
- Scala 
---

https://docs.scala-lang.org/overviews/scala-book/introduction.html

# 1. scala install on window

## 1.1 scala release

conf env

1. `SCALA_HOME`
2. Path add `%SCALA_HOME%\bin`

### 1.1.1 install on linux

1. install sdkman
   $ curl -s "https://get.sdkman.io" | bash
   $ source "$HOME/.sdkman/bin/sdkman-init.sh"
    $ sdk version
2. install sbt
   echo "deb https://repo.scala-sbt.org/scalasbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
   curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
   sudo apt-get update
   sudo apt-get install sbt
3. install scala
   sdk install scala

## 1.2 edge 安装

### 1.2.1 命令行安装

+ (1) Setup

    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
    sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/edge stable main" > /etc/apt/sources.list.d/microsoft-edge-dev.list'
    sudo rm microsoft.gpg

+ (2) Install

    sudo apt update
    sudo apt install microsoft-edge-dev

<!-- ————————————————
版权声明：本文为CSDN博主「cugautozp」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/cugautozp/article/details/109325559 -->

### 1.2.2 deb 安装

    sudo dpkg -i “xxx.deb”

# 2. 基本了解

## 2.1 `val` & `var`

`val` is an immutable variable — like final in Java — and should be preferred  
`var` creates a mutable variable, and should only be used when there is a specific reason to use it

## 2.2 if/else

    val x = if (a < b) a else b

## 2.3 match expressions

### 2.3.1 Scala has a match expression, which in its most basic use is like a Java `switch` statement:

    val result = i match {
        case 1 => "one"
        case 2 => "two"
        case _ => "not 1 or 2"
    }

### 2.3.2 matching against many different `types`:

    def getClassAsString(x: Any):String = x match {
        case s: String => s + " is a String"
        case i: Int => "Int"
        case f: Float => "Float"
        case l: List[_] => "List"
        case p: Person => "Person"
        case _ => "Unknown"
    }

## 2.4 try/catch

    try {
        writeToFile(text)
    } catch {
        case fnfe: FileNotFoundException => println(fnfe)
        case ioe: IOException => println(ioe)
    }

## 2.5 `for` loops and expressions

Scala for loops — which we generally write in this book as for-loops — look like this:

    for (arg <- args) println(arg)

    // "x to y" syntax
    for (i <- 0 to 5) println(i)

    // "x to y by" syntax
    for (i <- 0 to 10 by 2) println(i)

You can also add the yield keyword to for-loops to create for-expressions that yield a result. Here’s a for-expression that doubles each value in the sequence 1 to 5:

    val x = for (i <- 1 to 5) yield i * 2

Here’s another for-expression that iterates over a list of strings:

    val fruits = List("apple", "banana", "lime", "orange")

    val fruitLengths = for {
        f <- fruits
        if f.length > 4
    } yield f.length

## 2.4.1  For

> foreach is available on most collections classes, including `sequences`, `maps`, and `sets`.

    val ratings = Map(
        "Lady in the Water"  -> 3.0,
        "Snakes on a Plane"  -> 4.0,
        "You, Me and Dupree" -> 3.5
    )

    for ((name,rating) <- ratings) println(s"Movie: $name, Rating: $rating")


    ratings.foreach {
        case(movie, rating) => println(s"key: $movie, value: $rating")
    }

> While a for-loop is used for side effects (such as printing output), a for-expression is used to create new collections from existing collections.

> For 循环用于产生副作用(如打印输出)，
> 而 for 表达式用于从现有集合创建新的集合。

## 2.5 Types

### 2.5.1 Use the explicit form when you need to be clear

确认何时应该使用明确类型  

One place where you’ll want to show the data type is when you want to be clear about what you’re creating. That is, if you don’t explicitly declare the data type, the compiler may make a wrong assumption about what you want to create. Some examples of this are when you want to create numbers with specific data types. We show this in the next lesson.

当你想用明确的类型，防止编译器在进行类型推断推断错误。

| Data Type | Possible Values                                                                                 |
| --------- | ----------------------------------------------------------------------------------------------- |
| Boolean   | true or false                                                                                   |
| Byte      | 8-bit signed two’s complement integer (-2^7 to 2^7-1, inclusive) `-128 to 127`                  |
| Short     | 16-bit signed two’s complement integer (-2^15 to 2^15-1, inclusive) `-32,768 to 32,76`7         |
| Int       | 32-bit two’s complement integer (-2^31 to 2^31-1, inclusive) `-2,147,483,648 to 2,147,483,647`  |
| Long      | 64-bit two’s complement integer (-2^63 to 2^63-1, inclusive) (`-2^63 to 2^63-1`, inclusive)     |
| Float     | 32-bit IEEE 754 single-precision float `1.40129846432481707e-45 to 3.40282346638528860e+38`     |
| Double    | 64-bit IEEE 754 double-precision float `4.94065645841246544e-324d to 1.79769313486231570e+308d` |
| Char      | 16-bit unsigned Unicode character (0 to 2^16-1, inclusive) `0 to 65,535`                        |
| String    | a sequence of `Char`                                                                            |

## 2.6 Input and Output

    import scala.io.StdIn.readLine

    object HelloInteractive extends App {

        print("Enter your first name: ")
        val firstName = readLine()

        print("Enter your last name: ")
        val lastName = readLine()

        println(s"Your name is $firstName $lastName")

    }

# 3. DEMOMATCH 模式匹配样例

```scala
package org.aeewz.scala.demo

object DemoMatch extends  App{
  println("================ Match ====================")
  def convertBooleanToStringMessage(bool: Boolean): String = bool match {
    case true => "you said true"
    case false => "you said false"
  }
  val result = convertBooleanToStringMessage(true)
  println(result)
  println("========== Type (is int or string) ========")
  def isTrue(a: Any) = a match {
    case i:Int => false
    case s:String => false
    case _ => true
  }
  println(isTrue(0))
  println(isTrue(""))
  println(isTrue(1.1))
  println("================ isOdd ====================")
  def isOdd(num: Int) : Boolean = num % 2 match {
    case 0 => true
    case 1 => false
  }
  val nums = (1 to 5).toList
  nums.foreach{
    case(num) => {
      println(s" $num is${ if(isOdd(num)) "" else " not"} odd.")
    }
  }
  println("===========================================")

}
```

Output:

```shell
================ Match ====================
you said true
========== Type (is int or string) ========
false
false
true
================ isOdd ====================
 1 is not odd.
 2 is odd.
 3 is not odd.
 4 is odd.
 5 is not odd.
===========================================
```
