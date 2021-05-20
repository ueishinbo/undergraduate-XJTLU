#  Basic Java Review(L1)

## Hilstone Sequence

Hilstone Sequence is a arithmetic that you input a number **n**, then, the arithemetic return a sequence base tothe follow method.

```
public void hailstone(int n){
	while(n != 1){
		System.out.println(n);
		if(n % 2 == 0){
			n =. n /2;
		}else{
			n = 3*n + 1;
		}
	}
}
```



输入一个整数 如果是偶数数则除2，如果是奇数则乘以3+1，然后直到为1.

例如:

1. hailstone(5)=[5 16 8 4 2 1]
2. hailstone(3)=[3 10 5 16 8 4 2 1]

## Type 

类型是value的集合，允许操作数对其进行执行。

Java有**八种基本(primitive)数据类型**

> byte, int, short, long, float, double, boolean, char

**两种对象类型**

> String, BigInteger

## Operations

- Operations are functions that take input values and produce output values

运算时获取输入值并产生输出值的的函数。

## Static typing

* Java is a statically-typed language

在编译阶段，编译器会检查你的表达式。例如变量a和b声明为int，compiler 计算a+b的结果也当然是int

* 在**dynamically-typed** 类型的语言中 像python 或者javascript， 这种类型语言的检查只有在运行期间会有。

## Array

* 数组的容量在创建完成后就不能改变大小了
* Arrays are fixed-length sequences of another type



## List and ArrayList

* List are variable-length sequences of another type

* To declear a List variable nad make a list value:

  > List<Integer> list = new ArrayList<Integer>();

* List 是一个接口，不能被new 你可以理解为抽象的东西没法实例化。



























