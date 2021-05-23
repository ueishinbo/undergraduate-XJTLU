# Immutability, List, Map

## checking 

1. Static checking: the bug is found automatically before the program even runs
2. Dynamic checking: the bug i found automatically when the code is executed
3. No checking: the language doesn't help you find the error at all You have to watch for it yourself, or endup with wrong answers!

不用说，静态变异抓住bug比动态抓更好，而动态抓笔没有checking更好

### Static Checking 

静态检查可以cratch:

1. 语意错误：例如拼写错误
2. 错误的方法名
3. 错误的数据类型
4. 错误的返回值

### Dynamic Checking

动态检查可以捕捉：

* 非法的参数值，例如整数表达式x / y 只有当y = 0的时候才能被发现。
* 不可呈现的返回值
* 指针越界
* 空指针异常

### Static Checking VS Dynamic Checking

静态检查就是它一定是错的，错的很明白，而动态检查是由于特殊值或者特殊情况造成的。

### No Checking

Integer division.

例如5/2不会返回一个分数，他会返回一个被删减了的整数。

当您的回答情况过于肯定而无法满足该有限范围内是，会发生什么情况，计算会悄悄地溢出（环绕），并从合法范围的某个地方返回一个整数。但是返回的答案不正确。

浮点类型（例如双精度类型）具有一些不是实数的特殊值：NaN（代表“非数字”），

## Public and Static 

public 意味着在任何program的任何地方你都可以去调用此方法。

static 意味着只有在本类中可以调用。

## Javadoc Comments

也就是下面这种注释

```
/**
*@param n 
*@return 
*/
```

Start with summary of the method/calss documented, optioonally include one or two examples

Describe each parameter with @parm, state the assumptiion

Describe the return value with @return， if user follow teh assumptions.

## Assumptions

## Two goals



写代码的俩目的， 一个是给机器看，一个是给人看。

## Java Collections and List

## Snapshot Diagrams

可以用来描述程序运行时的内部状态。

画Snapshot Diagram 不仅能让我们对程序的运行有所了解，还能加强我们对一些基本概念的理解和认识，例如：基本数据类型，对象数据类型，不可变值等等。

同时Snapshot Diagrams能够更加直观的向我们展示值的改变以及引用改变之间的关联，和具体实现。

对于基本数据类型，使用单线箭头指向实际值，不需要表明数据类型。

<img src="https://i.loli.net/2021/05/17/CihuADMQJjk7tTI.png" alt="WX20210517-142311@2x.png" style="zoom:40%;" />

对于对象的值：如果是可变对象，使用单线椭圆，椭圆内写明对象的类型以及对象内的值。

<img src="https://i.loli.net/2021/05/17/BQIJtCz1hFXm2na.png" alt="WX20210517-142522@2x.png" style="zoom:50%;" />

如果是不可变对象，使用双线椭圆，椭圆内写明对象的类型以及对象内的值。

<img src="https://i.loli.net/2021/05/17/XDmzq1BUtHbsRy9.png" alt="WX20210517-143234@2x.png" style="zoom:50%;" />

如果对象是不可变引用（final标记），使用双箭头，如果对象是可变引用，则使用单箭头。eg:age

<img src="https://i.loli.net/2021/05/17/9WHs1T2qF7MwL6n.png" alt="WX20210517-143522@2x.png" style="zoom:50%;" />



when you change the contents of a **mutable value(可变值)** - such as an array or list-- you're changing references inside that value

* this is called mutating the value

```java
List<Integer> list = new ArrayList<>();
list.add(3);
list.add(5);
list.set(0,9);
```

<img src="https://i.loli.net/2021/05/17/WQfyJxYTMnbwmer.png" alt="WX20210517-150258@2x.png" style="zoom:40%;" />

* In previous, a list an example of a mutable value
* Now, a string is an example of an **immutable value**(不可变值)
  * For,example, if we have a String variable s, we can **reassign** it from a value of "a" to "ab"

```java
String s = "a";
s= s + "b";
```

But StringBuilder and StringBuffer is ** a mutable value** that represents a string of characters it has methods taht change the value of the object:

```java
String builder sb = new StringBuilder("a");
sb.append("B");
```

Those two napspshot diagrams look **very different**, which is good: the difference between mutability and immutability will play an important role in making our code safe from bugs

<img src="https://i.loli.net/2021/05/17/f6Jne3xN8hWQDbC.png" alt="WX20210517-155250@2x.png" style="zoom:33%;" />

## Immutable Referneces

* Java also gives aus **immutable references** variables that are assigned once and never reassigned. To make a reference immutable, declare it with the key word final:

```java
final int n = 5;
```

* if the java compiler isn't convinced that your final variable will only be assigned once at runtime, then it will produce a compiler error. So final gives you static checking for immutable references.
* In a snapshot diagram, an immutable reference(final) is denoted by a double arrow. Here's an object whose id never changes(it can't be reassigned to a different number), but whose age can change

 ## Final

* Final can be used on both **pa rammers** and **local variables** 
  * when used on a parameter, final means taht the parameter is assigned when teh method is called, and then cannot be reassigned during the body of the method
  * when usebe reassigned on a local variable, final means taht the variable cannot reassigned after its first assignment, until the variable's scope ends.
* final 也可以修饰List。但是如果修饰了以后就不能再重新赋值，但是对象的指针还是可以变的,例如调用List的add()方法。



















