# Number Theory and Cryptography(Week10)

## Security of Communications

Use cryptography to make communications secure;

For example, encrypt messages to preserve secrets.

To protect sensitive information, we. must ensure the following goals are met:

* **Data Integrity: ** Information should not be altered without detection.
* **Authentication:** Agents involeved in the communication must be identified.
* **Nonrepudiation**: if binded by contracts, agents cannot drop out of their obligations without being detected.
* **Confidentiality**: Sensitive information must be kept securet from agents that are not authorised to access it .
* To protect sensitive information, techniques based on algorithms and communication protocols have been developed.
* Many of these thechniques use number theory,e.g.,the popular RSA(Rivest Shamir Adleman) secheme.
* It is not only about number theory! Security protocols need be proven correct: this uses formal methods(anothere area of computer science that will not be addressed here).

-----------

使用密码学来保证通信安全

例如：加密信息来储存秘密

为了保护敏感信息，我们必须确保以下目标得完成。

* 数据完整：数据在没有detection之前不允许改变。
* 准许：必须确定参与通信的代理。
* 认可：

## REVIEW OF MATH BASICS

### INTEGER ARITHMETIC

In integer arithmetic, we usse a set and a few operations. You are familiar with this set and the corresponding operations, but they are revewed here to create a background for modular arithmetic .

在整数运算中，我们使用一组和一些运算。你应该熟悉此设置以及其相应的操作，但是这里对他们进行了回顾，以创建模块化算数的背景。

#### 1.1 Set of Integers

The set of integers, denoted by Z, contaions all integeral numbers(with no fraction) from negative infinitu to positive infinity.

<img src="https://i.loli.net/2021/05/14/rqJwT4HdMEPghuY.png" alt="WX20210514-145514@2x.png" style="zoom:40%;" />

In cryptographty, we are interested in three binary operations applied to the set of integers. A binary operation takes two inputs and creates one output.

在密码学方面，我们对应用于整数集的三个二进制运算感兴趣。 二进制运算需要两个输入并创建一个输出。

<img src="https://i.loli.net/2021/05/14/hEVWPnuJ3FvadUZ.png" alt="WX20210514-153419@2x.png" style="zoom:50%;" />

#### 1.2 Continued

**Example**

The following shows the results of the three binary operations on two integers. Because each input can be either positive or negative, we can have our cases for each operation.

<img src="https://i.loli.net/2021/05/14/ptyj7DqOHWufk64.png" alt="WX20210514-153734@2x.png" style="zoom:50%;" />

**What about in their inverse operations?**

​	**What aboout division?**

**3➗2 = ？ not an integer**

因为除法可能会生成非整数的数。所以不用除法

#### 1.3 Integer Division

In integer arithmetic, if we divide a by n, we can get q and r.

<img src="https://i.loli.net/2021/05/14/4Rq69OvBgLUrhne.png" alt="WX20210514-172955@2x.png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/05/14/BvuWF4VnSTbPgjd.png" alt="WX20210514-173926@2x.png" style="zoom:40%;" />





r and q are negative when a is negative.

How can we apply the restriction that r needs to be positive?

The value of **q -1 <--> r + n**, to make r positive.

<img src="https://i.loli.net/2021/05/14/T5ltsU2JmZNeEHM.png" alt="WX20210514-174327@2x.png" style="zoom:50%;" />

#### 1.4 Divisibility

If a is not zero and we let r= 0 in the division relation, we get

​						**a = q ✖️ n**

If the remainder is zero, n|a  <-- The divisibility of a by n is denoted by the smbol

if the remainder is not zero n~~|~~a



1. The integer 4 divides the integer 32 because 32 = 8 ✖️4. We show this as 

​													**4|23**

2. The number 8 does not divide the number 42 because 42 = 5 ✖️ 8 +2. There is a remainder, the number 2, in the equation. We show this as 

​													**8~~|~~42**

1. We have 13|78, 7|98, -6|24, 4|44, and 11|(-33).
2. We have 13 ~~|~~23, 7~~|~~50, -6~~|~~24, 4~~|~~41 and 11~~|~~(-32).

#### 1.4 Continued :<mark>Properties</mark>

<mark>Properties</mark>

* Property 1: if a |1  = ±1.
* Property2: if a|b, and a|b ,then a = ±b
* Property3:if b|a and c|b, then c|a.
* Property4:if a|b and a|c, then a|(m ✖️ b+ n✖️c), where m and n are arbitrary integers.

1. Since 3|15 and 15|45

   accprding to the third property, 3| 45

2. Since 3|15 and 3 | 9

   according to the fourth property,

   3|(15✖️2+9✖️4), which means 3|66

   

#### 1.4 Continued : Common divisors of twointegers

<img src="https://static01.imgkr.com/temp/d0a8d7cb58324d329ed87fe1952d591b.png" alt="WX20210514-174327@2x.png" style="zoom:30%;" />

* Greatest Common Divisor

意思就是公共除数中最大的

The greatest common divisor of two positive integers is the largest integer that can divide both integers

* Eucildean Algorithm (欧几里德算法，也叫辗转相除法)

Fact: gcd(a,0) = a

Lemma:Let a, b, q and r be integer such taht a = bq + r and b ≠ 0. Then gcd(a,b) = gcd(b, r).

1. Given 26 = 64 ✖️4 + 2， find the gcd(26,6) and gcd(6,2).

**Solution**

a= 26, b = 6, r = 2

common divisors of 26 and 6:(1,2)

common divisors of 6 and 2: (1,2)

Gcd(a,b) = 2, gcd(b,r) = 2

2. Given 60 = 24 ✖️ 2 + 12 Find the gcd(60,24) and gcd(24,12)

**Solutitpn**

a = 60, b = 24, r = 12

common divisors of 60 and 24:(1,2,3,4,6,12)

Common divisors of 24 and 12:(1,2,3,4,5,12)

Gcd(a,b) = 12, gcd(b,r) = 12

<img src="https://i.loli.net/2021/05/15/FjalZ5tcTmQUDgL.png" alt="WX20210515-141745@2x.png" style="zoom:40%;" />



* 欧几里得算法扩展（辗转相除法扩展）

扩展欧几里得算法是欧几里得算法（又叫辗转相除法）的扩展。除了计算a、b两个整数的最大公约数，此算法还能找到整数x、y（其中一个很可能是负数）。通常谈到最大公因子时, 我们都会提到一个非常基本的事实: 给予二整数 a 与 b, 必存在有整数 x 与 y 使得ax + by = gcd(a,b)。有两个数a,b，对它们进行辗转相除法，可得它们的最大公约数——这是众所周知的。然后，收集辗转相除法中产生的式子，倒回去，可以得到ax+by=gcd(a,b)的整数解。

![WX20210515-144503@2x.png](https://i.loli.net/2021/05/15/QJFdtZIT5sr7wu9.png)

### MODULAR ARITHMETIC

The division reationship(a = q ✖️ n + r) discussed in the previous section has two inputs (a and n) and two outputs( q and r). In modular arithmetic, we are interested in only one of the outputs, the remainder r.

### MATRICES























