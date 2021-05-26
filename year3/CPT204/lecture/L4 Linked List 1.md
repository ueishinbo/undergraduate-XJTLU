# L4 **Linked List 1**

想清楚递归和迭代的区别，一定要想清楚base case和recursive step，想清楚出口条件

比如：

> list1 = [1, 2, 3],  list2 = [4, 5, 6]   
> list = MyList.recCatMutList(list1, list2);
> list → [1, 2, 3, 4, 5, 6]
> list1 → [1, 2, 3, 4, 5, 6]

```java
/**
 * Catenate two MyLists, listA and listB. Mutate listA.
 * @param listA is a MyList object.
 * @param listB is a MyList object.
 * @return a list consisting of the elements of listA followed by the
 * elements of listB.
 */
public static MyList recCatMutList(MyList listA, MyList listB) {

    // base case
    if (listA == null) {
        return listB;
    }
    // recursive step
    listA.next = recCatMutList(listA.next, listB);
    return listA;
}
```

这个题是调用这个方法传进去两个list A和B，然后返回一个list的状态是B跟在A的后面

所以这题的思路是找到listA的最后一个节点也就是list.next==null ，然后再把listB赋给null就大功告成了，所以呢递归我感觉跟循环是一样的，就是得想清楚她为什么要进去。

而下面这个题：

> list1 = [1, 2, 3],  list2 = [4, 5, 6]   
> list = MyList.recCatList(list1, list2);
> list → [1, 2, 3, 4, 5, 6]
> list1 → [1, 2, 3]

```java
/**
 * Catenate two MyLists, listA and listB. Does not mutate listA.
 * @param listA is a MyList object.
 * @param listB is a MyList object.
 * @return a list consisting of the elements of listA followed by the
 * elements of listB.
 */
public static MyList recCatList(MyList listA, MyList listB) {

    // base case
    if (listA == null) {
        return listB;
    }
    // recursive step
    return new MyList(listA.value, recCatList(listA.next, listB));
}
```

 就是不能改变listA和listB，所以呢，我们得创建一个新的list

## Inner / Nested Class

 ```java
 private static class Node{
   public int item;
   public Node next;
   public Node(int i, Node n){
 		item = i;
     next = n;
   }
 }
 ```

> **private** sciece Node is only used by the owner Class, and not other classes
>
> **static** sciece Node never uses istance variable/method of the other class
>
> for private inner classes, these access modify are irrelevant

## generic

To allow types such as Integer, String, and user-defined types to be a parameter to methods, classes, and interfaces, we use  **gneric**，Using it, we can create classes that work with different data types.



## caching

We store the size information as an instance variable, set and update it accordingly

就是我们用一个实例储存修改更新下面题中的size

```java
private Node first;
private int size;

public List(int item){
  first = new Node(item,null);
  size = 1;
}

public void addFirst(int item){
	first = new Node(item, first);
  size += 1;
}
```

this technique is called caching we can also use caching to store max, min, mode

## invariants

**An invariant** is a condition that is guaranteed to be **true** during code execution

就是

invariant is a condition that must be preserved and guaranteed to be true during a method's execution called

就是不管你程序怎么运行，他都不会变的

## constant-time methods

就是一个方法你每次调用花费的时间都是一样的，就比如一个list，因为你在类头中已经定义了size属性，并且在你每次add的时候他都会让size加一，所以当你调用size方法的时候不管这个list有多少值，他都是立马出结果，不会受到你list大小的影响。



## checked VS unchecked

## handling exception

## copy constructor

Copy constructor is a special constructor that takes as input another object of the same type and create a new object that is a copy of the input

## generic arrays

```java
public ARList(){
	items = new T[100];  	//这是错误的写法，编译器会报错滴～
  size = 0;
}
//所以正确的写法应该如下
public ARList(){
  items = (T[]) new Object[100];
  size = 0;
}

private void resize(int capactiy){
  T[] a = (T[]) new Object[capacity];
  System.arraycopy(items,0,a,0,size);
  items = a;
}
```





