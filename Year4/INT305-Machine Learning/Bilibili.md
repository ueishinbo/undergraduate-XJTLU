Machine learning algorithms:

- Supervised learning: the idea is taht we're going to teach the computer how to do something
- Unsupervised learning: let it learn by itself.

 ## Supervised learning:

<img src="https://i.loli.net/2021/09/15/zMhscS4pYb5No1k.png" alt="WX20210915-230641@2x.png" style="zoom:50%;" />

比如现在有一组真实的房子面积数和它对应卖出的价格所画成的图标，现在你朋友有一个750m<sup>2</sup>的房子，他想卖出去让你预测一下他能卖多少钱。**第一种**方法是画出一次函数的直线（粉色）大概估计出买的价格是150。**第二种**是画出二次函数的曲线（蓝色）大概估计卖出的是200。Supervised learning的意义是先给出很多组争取的平米数对应的房价，然后给出某一平米数，预测它能真正卖出的价格。

专业来讲它被称为<mark>Regression problem（回归问题）</mark> : predit continuous value output 。回归是指我们的目标是预测一个连续输出。

<img src="https://i.loli.net/2021/09/16/pwCyWrxm4XJUZYj.png" alt="WX20210916-002342@2x.png" style="zoom:50%;" />

如果你想预测一个得了肿瘤的人是恶性肿瘤还是良性肿瘤。这是一个分类问题，因为它的离散很小，只有良性和恶性之分（最多恶性再分为A型，B型）我们的目的就是为了预测离散的输出值