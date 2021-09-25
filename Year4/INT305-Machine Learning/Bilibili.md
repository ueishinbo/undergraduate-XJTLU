Machine learning algorithms:

- Supervised learning: the idea is taht we're going to teach the computer how to do something
- Unsupervised learning: let it learn by itself.

 ## Supervised learning:

<img src="https://i.loli.net/2021/09/15/zMhscS4pYb5No1k.png" alt="WX20210915-230641@2x.png" style="zoom:50%;" />

比如现在有一组真实的房子面积数和它对应卖出的价格所画成的图标，现在你朋友有一个750m<sup>2</sup>的房子，他想卖出去让你预测一下他能卖多少钱。**第一种**方法是画出一次函数的直线（粉色）大概估计出买的价格是150。**第二种**是画出二次函数的曲线（蓝色）大概估计卖出的是200。Supervised learning的意义是先给出很多组争取的平米数对应的房价，然后给出某一平米数，预测它能真正卖出的价格。

专业来讲它被称为<mark>Regression problem（回归问题）</mark> : predit continuous value output 。回归是指我们的目标是预测一个连续输出。

<img src="https://i.loli.net/2021/09/16/pwCyWrxm4XJUZYj.png" alt="WX20210916-002342@2x.png" style="zoom:50%;" />

如果你想预测一个得了肿瘤的人是恶性肿瘤还是良性肿瘤。这是一个分类问题，因为它的离散很小，只有良性和恶性之分（最多恶性再分为A型，B型）我们的目的就是为了预测离散的输出值

## unsupervised learning:

没有明确的目标。比如我将10万条新闻放入unsupervised learning algorithm 中他会自动吧这些新闻分成一些类。    

## 模型描述

<img src="https://i.loli.net/2021/09/20/SEqAyMLjmahu9cD.png" alt="WX20210920-223956.png" style="zoom:80%;" />

m = Number of training examples

x's = "input" variable / feature

y's = "output" variable / "target" variable

* **(x,y) ------- one training example**

* **(X<sup>(i)</sup>,y<sup>(i)</sup>) -----第i个 training example (这里的i指的不是幂指数）**
  * 就比如上图中x<sup>(1)</sup> = 2104, x<sup>(2)</sup> = 1416, y<sup>(1)</sup> = 460, y<sup>(2)</sup> = 232

Training Set  

<img src="https://i.loli.net/2021/09/20/Tv8bV46KJXYrSjc.png" alt="WX20210920-230854.png" style="zoom:80%;" />

  ### liner regression

<img src="https://i.loli.net/2021/09/20/QT7AxHZX52Yvmfy.png" alt="WX20210920-231319.png" style="zoom:80%;" />

## Cost function

 <img src="https://i.loli.net/2021/09/24/RUkdhsEMetpKjiS.png" alt="WX20210924-214848@2x.png" style="zoom:80%;" />

代价函数就是实际跟预测的差，这个函数越小越好，就比如上图右上的公式，h<sub>0</sub>(x<sup>(i)</sup>） - y<sup>(i)</sup>)<sup>2</sup> 计算的就是预测跟实际的差。	

### 简化版本

![WX20210924-215743@2x.png](https://i.loli.net/2021/09/24/xXFjG1OYR89PvZp.png)

比如右边是原先的，我先把θ<sub>0</sub>设为0这样h<sub>θ</sub>(x) = θ<sub>1</sub>x了，相应的cost function也相应变简洁了。 



### θ<sub>1</sub> = 1

现在我们让θ<sub>1</sub> = 1,画图可得<img src="https://i.loli.net/2021/09/25/mlPkY3qHudiGKTF.png" alt="WX20210925-092431@2x.png" style="zoom:67%;" />

其次，我们将θ<sub>1</sub>带入代价函数得： <img src="https://i.loli.net/2021/09/25/3eynGWz1Hgi4Npj.png" alt="WX20210925-093202@2x.png" style="zoom:50%;" />

得到 J(1) = 0.

### θ<sub>1</sub> = 0.5

现在我们让θ<sub>1</sub> = 0.5，画图可得<img src="https://i.loli.net/2021/09/25/ky8AO7CVSnvajQi.png" alt="WX20210925-125012@2x.png" style="zoom:80%;" />

**（上图中红色叉代表原本实际的值，而蓝色的点代表θ<sub>1</sub> = 0.5时预测的值，蓝色的线段代表实际与预测的差值）**

其次，我们把θ<sub>1</sub> = 0.5 带入代价函数得：<img src="https://i.loli.net/2021/09/25/I72g5R1T8FLfokV.png" alt="WX20210925-125632@2x.png" style="zoom:67%;" />

**（是0.58，老师写错了）**

### θ<sub>1</sub> = 0

 现在我们让θ<sub>1</sub> = 0，画图可得：<img src="https://i.loli.net/2021/09/25/txi2qHgfK18dSCZ.png" alt="WX20210925-130758@2x.png" style="zoom:67%;" />

由于θ<sub>1</sub> = 0 所以x轴就是那条线。还是**蓝线代表实际与预测的差值，红叉代表实际的值**

其次，我们把θ<sub>1</sub> = 0 带入代价函数得：<img src="https://i.loli.net/2021/09/25/FTNw4dH6zgluOo1.png" alt="WX20210925-131129@2x.png" style="zoom:67%;" />

### ...

随着不断改变θ<sub>1</sub> 的值，最终我们可以得到不同的代价函数J(θ<sub>1</sub> ) 的图，如下所示

<img src="https://i.loli.net/2021/09/25/2Zbv4iEXB7pNPOL.png" alt="WX20210925-131424@2x.png" style="zoom:67%;" />

 



线性回归函数的目地是找到最小的J(θ<sub>1</sub> )的值,上面的一系列例子中，我们发现θ<sub>1</sub>  = 1时候误差是最小的也就是完美的拟合了他。



## Cost function 2

























