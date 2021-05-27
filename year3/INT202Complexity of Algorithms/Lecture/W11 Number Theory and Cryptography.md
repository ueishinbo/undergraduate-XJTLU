# Number Theory and Cryptography(W11)

## Modular Exponentiation

​		3<sup>94</sup>(mod17)

Any number can be represented as the sum of distinct powers of two

​			**94 = 64+16+8+4+2**

​			**How do you pick them?**

<img src="https://i.loli.net/2021/05/15/2wom5WMqfXheJST.png" alt="WX20210515-153400@2x.png" style="zoom:50%;" />

​			**3<sup>94</sup>(mod17)**

Any number can be represented as the sum of distinct powers of two.

第一步：先把94写成二进制形式：1011110

第二步：在把上面的表格列出来

第三步：然后把非零项拎出来进行小的模运算例如3<sup>64</sup> = (3<sup>16</sup>)<sup>4</sup> = (1)<sup>4</sup> = 1

3<sup>2</sup> = 9

> 9对17取mod还是9

3<sup>4</sup>= 81 = 13 = -4	

> 首先 81对17取mod = 13 但还是太大了，所以得继续取mod但是能是反过来，用17对13取mod结果是4然后再取个负号就是-4啦

3<sup>8</sup> ≡ (3<sup>4</sup>)<sup>2</sup> ≡ (−1)<sup>2</sup>≡ 16 = -1 (原理同上)

3<sup>16</sup> ≡ (3<sup>8</sup>)<sup>2</sup> ≡ (−1)<sup>2</sup>≡ 1(原理同上)

3<sup>64</sup> ≡ (3<sup>16</sup>)<sup>4</sup> ≡ (−1)<sup>4</sup>≡ 1

最后把他们全加起来

​	(1)(1)(-1)(-4)(9)

=36

=2

### Theorem

[Fermat's Little Theorem]: Let p be prime, and let x be an integer such that x mode p ≠ 0. Then 

​				x<sup>p-1</sup> mod p

Fermat's little theorem is a fundamental theorem in elementary number theory, which helps **compute powers of integers modulo prime numbers**

* Example(p = 5):
  * 1<sup>4</sup> mod 5 = 1								2<sup>4</sup> mode 5 = 16 mod 5 = 1
  * 3<sup>4</sup>mod5 = 81 nod 5 = 1	      	4<sup>4</sup>mod 5 = 256 mod 5 = 1

**Corollary**

Let p be a prime. For each nonzero residue x of Z<sub>p'</sub> the multiplicative inverse of x is x<sup>p-2</sup>mode p

**Proof**

x(x<sup>p-2</sup> mod p) mod p = xx<sup>p - 2</sup> mod p = x<sup>p - 1</sup> mod p = 1

​				**X<sup>-1</sup> ≡X<sup>p - 2</sup>(mode p)**

## Euler's function

* The multiplicativve group for Z<subb>n'</, denoted with Z<sup>*</sup><sub>n'</sub>, is the subset of elements of Z<sub>n</sub> relatively prime with n
* The totient funciton of n, denoteed with φ(n), is the size of Z<sup>*</sup><sub>n</sub>
  * Example Z<sup>*</sup> = {1,3,7,9}			φ(10) = 4
* if p is prime, we have
  * Z<sup>*</sup><sub>p</sub> = {1,2,...,(p-1)}					φ(p) = p -1

欧拉函数就是求一个数质数的数量

> **Theorem [Euler's Theorem]: **
>
> Let n be a positive integer, and let X be an integer such taht gcd(x,n) = 1. Then
>
> ​								X<sup>φ(n)</sup> ≡ 1 mod n

* Example(n = 10)

  3<sup>φ(10) </sup>mod 10 = 3<sup>4</sup> mod 10 = 81 mod 10 = 1

  7<sup>φ(10)</sup> mod 10 = 7<sup>4</sup> mod 10 = 2401 mod 10 = 1

  9<sup>φ(10)</sup> mod 10 = 9<sup>4</sup> mod 10 = 6561 mod 10 = 1

## Primality Testing

Let *n* *>* 0 be an integer. How to find out if *n* is prime? This is a central question in cryptographic computations.

**Can we use Fermat's Little Theorem?** No because of the existence of **Carmichael** numbers that have the property X<sup>n-1</sup> ≡ 1 mod n for all 1 <= x <= n -1, but n is composite. For example, 561 is Carmichael number (561 = 3 * 11 * 18).

This can be done using for example probabilistic methods: We can use a **witness funciton** witness(x,n)(wherein x in a random number 1<= x <= n -1), which gives a definite answer when n is composite and an answer with some error probability q when n is prime (as there are only 255 Carmichael numbers for integers from 1 to 10<sup>8</sup>)

## Cryptorgaphic communications

Throughout history there has often been the need (or desire ) to securely transmit information through insecure channels. Such applications include communications for business reasons and military purposes, and most recently, transactions through the Internet.

A variety of cryptographic methods have been developed to facilitate this type of communication. Yhese include encryption/decryption transformations and digital signatures.

## Encryption schemes

Confidentially in communication can be achieved by encryption schemes, or ciphers.

The general idea behind these schemes is that the message M to be sent, often referred to as th plaintext, is encrypted into an unrecognizable string of characters C, the ciphertext.

The ciphertext C is then transmitted to the recipient who decryots C to recover the original message M.

-----

可以通过encryption schemes或者 ciphers 进行秘密交谈

这些方案背后的总体思想是，要发送的消息M（通常称为明文）被加密为字符C（密文）无法识别的字符串。

秘文C 通过解释器解释C然后传送给接收者

<img src="https://i.loli.net/2021/05/15/1FsNEhIqjyGbrR2.png" alt="WX20210515-175815@2x.png" style="zoom:30%;" />

* Scenario:
  * Alice wants to send a message(plaintext p ) to Bob.
  * The communication channel is insecure and can be eavesdropped If Alice and Bob have previously agreed on an ncryption scheme(cipher), the message can be sent encrypted (ciphertext c )

------

情节：

​	Alice 想发一个消息(明文)给Bob

​	如果他俩遵循某种密码协议，那么就可以保证通信过程是安全的，不会被偷听。

## Symmetric encryption schemes and secret keys

对称加密方案和秘密密钥

In a traditional encryption scheme a common secret key, K, is shared by Alice and Bob.

This common key is used for both encryption and decrption of messages.

Such an encryption scheme is called symmetric since the recipient receiver both have access to the same secret key, and it is used for encryption and decryption,

-----

在传统的加密方案中，爱丽丝和鲍勃共享一个公共密钥K。

编码方和解码方有共同的密匙信息

这样的加密方案称为对称方案，因为接收方的接收方都可以访问相同的密钥，并且用于加密和解密，

## Symmetric encryption schemes and secret keys Substitution ciphers

对称加密方案和秘密密钥替换密码

A classic example of a symmetric cipher is a substitution cipher. In this case the secret key is a permuation *π* of the characters of the alphabet.(for example, example, each A gets replaced by the letter D, each A gets replaced by the letter D, each B gets replaced by the leter H, etc.)

Encrypyion of the plaintext M is accomplished by mapping each character x with its corresponding character y = *π*(x).

Decrypting the ciphertext C is easily accomplished with knowledge of the permutation *π*,i.e. each character y of C is replaced with x = *π*<sup>-1</sup>(y).

-----

对称密码的经典示例是替换密码。在这种情况下，密钥是字母字符的排列π。 （例如，每个A被字母D替换，每个B被字母H替换，等等。）

通过将每个字符x与其对应的字符y =π（x）映射来完成对明文M的加密。

借助对置换π的了解可以很容易地完成对密文C的解密，即C的每个字符y都用x =π-1（y）代替。

## Symmetric encryption schemes and secret keys The Caesar cipher

The *Caesar cipher* is an early example of a substitution cipher wherein each character *x* is replaced by thecharacter *y*=(*x*+*k*) mod*n*,where*n*isthesizeofthealphabetandthe integer *k* , 1 ≤ *k* *<* *n*, is the secretkey.

凯撒密码是替换密码的早期示例，其中每个字符x都由字符y =（x + k）modn代替，其中字母的大小和整数k（1≤k <n）是密钥。

This type of cipher is called the “Caesar cipher” because Julius Caesar is known to have used it with *k* =3.

这种类型的密码被称为“凯撒密码”，因为众所周知朱利叶斯·凯撒使用k = 3的密码。

## Symmetric encryption schemes and secret keys

对称加密方案和秘密密钥

**传统密码学**

* Ciphers were already studied n. ancient times

* Caesar's cipher:

  * Replace a with d
  * Replace b with e
  * ....
  * replace z with c

  **N = 3**

Substitution cipher takes the plaintext alphabets and replace them by other alphabets to generate the ciphertext.

替代密码采用明文字母并将其替换为其他字母以生成密文。





























