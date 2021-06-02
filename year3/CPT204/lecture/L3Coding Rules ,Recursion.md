# W(3) **Coding Rules** ,**Recursion**

**Partition the Input Space** is the way 

## **Don't Repeat Yourself**

就是不要在两个地方写一模一样的代码，如果发生了bug，你就得改两次，但是呢，有时你会忘记到底第二处在哪，所以有两处用到的话，那就把它抽象成一个方法～

## **Comments Where Needed: Specification**

在需要的地方写注释～

## **Fail Fast**

fail fast 意思就是尽可能让bug快点显现出来，这样才好改，所以是static checking的优先级大于dynamic checkng大于no checking

## **Avoid Magic Numbers**

就是避免直接写数字，不然没人懂你这数字代表的是啥

## **Avoid Magic Numbers: Better Ways**

就是尽量用单词来代表数字

## **Use Good Names: Naming Conventions**

驼峰式命名规则

## **Testing and Bugs**

## **Recursion**

### Factorial

#### 计算阶乘：

```java
    public static int Factorial(int n) {
        if (n == 1)
            return 1;
        return n * Factorial(n-1);
    }
```

#### **Sum of Digits**：

意思计算一串数字的合：例如123合是4. 901合是10. 101和是2

Test case:

> - sumDigits(123) → 6
> - sumDigits(99999) → 45
> - sumDigits(0) → 0
> - sumDigits(101010101) → 5
> - sumDigits(10) → 1

```java 
public static int SumDigits(int n){
  if(n / 10 == 0)
    return n;
  return (n % 10) + SumDigits(n / 10);
}
```



### numSubs

> ```java
> /**
>  *Given an input string and a non-empty substring subs, write a method to
>  * compute recursively the number of times that subs appears in the string.
>  * The substrings must not overlap and no loops used.
>  * @return the number of substirng
>  * numSubs("abcxxxxabc", "abc") → 2
>  * numSubs("abcdef", "xyz") → 0
>  * numSubs("aaaaaaaaaa", "a") → 10
>  * numSubs("aaaaaaaaaa", "aa") → 5
>  * numSubs("", "a") → 0
>  * numSubs("a", "a") → 1
>  */
> ```

```java
public static int numSubs(String input, String subString){
    if (input.length() < subString.length()){
        return 0;
    }
    if (input.substring(0,subString.length()).equals(subString)){
        return 1 + numSubs(input.substring(subString.length()),subString);
    }
    return numSubs(input.substring(1),subString);
}
```

### subseq

> ```java
> /**
>  * Given a word consisting only of letters A-Z or a-z
>  * @param word
>  * @return  all subsequences of word, separated by commas,
>  * where a subsequence is a string of letters found in word in the
>  * same order that they appear in word.
>  * Note the trailing comma preceding the empty string "", which is also a valid subsequence
>  *subsequences("abc") → "abc,ab,bc,ac,a,b,c,"
>  */
> ```

方法1:无helper方法

```java
  public static String subseq(String word){
        if (word.equals(""))
            return "";
        char firstLetter = word.charAt(0);
        String restOfWord = word.substring(1);
        String subsequenceOfRest = subseq(restOfWord);
        String result = "";
        for (String subsequence : subsequenceOfRest.split(",",-1)){
            result += "," + subsequence;
            result += "," + firstLetter + subsequence;
        }
        result = result.substring(1);
        return result;
    }
```

方法2：带helper方法

```java
    public static String subseq(String word){
        return subseqHeaper("",word);
    }
    private static String subseqHeaper(String partialSubseq,String word){
        if (word.equals(""))
            return partialSubseq;
        return subseqHeaper(partialSubseq + word.charAt(0),word.substring(1))
                + ","
                +subseqHeaper(partialSubseq,word.substring(1));
    }
```

### reverseStr

> ```java
> /**
>  * Given a string,
>  * @param str
>  * @return the reverse of that string recursively
>  * reverseStr("abcde")->"edcba"
>  * reverseStr("")->""
>  * reverseStr("a") ->"a"
>  * reverseStr("ab") -> "ba"
>  */
> ```

方法1:不带helper方法

```java
      public static String reverseStr(String str){
        if (word.equals(""))
            return "";
        return str.substring(str.length()-1,str.length()) + reverseStr(str.substring(0,str.length()-1));
    }
```

方法2 ：带helper方法

```java
 public static String reverseStr(String str){
        return reverseStrHelper(str,"");
    }
    private static String reverseStrHelper(String str,String reverse){
        //base case
        if (str.equals(""))
            return reverse;
        return reverseStrHelper(str.substring(1), str.charAt(0) + reverse);
    }
```

























