# Minimum Spanning Tree and Network Flow(W9)

## Minimum Spanning Tree(MST)

最小生成树：

![WX20210513-154734@2x.png](https://i.loli.net/2021/05/13/QBiCtHTUS3OowZ6.png)

* 对于一个图而言，它可以生成很多中树，如上面图2、3就是由图1生成的。
* 从上面可以看出生成树是将原图的全部顶点以最少的边连通的子图，对于有n个顶点的连通图，生成树有**n-1**条边，若边数小于此数就可能将各个顶点连通，如果边的数量多于**n-1**条边，必定会产生回路。
* 对于一个带权连通图，生成树不同，树中各边上权值总和也不同，权值和最小的生成树则称为图的最小生成树。

### Prim算法

**基本思想**：

假设有一个无向带权图G=(V,E),它的最小生成树为MinTree, 其中V为顶点的集合，T为边的集合。球边的集合T的步骤如下：

1. 令U={u<sub>0</sub>},T = {}.其中U为最小生成树的顶点集合，开始时U中只含有顶点u<sub>0</sub>(U<sub>0</sub>可以为集合V中的任意一项)，在开始构造最小生成树时我们从u<sub>0</sub>出发。
2. 对所有u∈U,v∈(V - U)(其中u,v表示顶点)的边(u,v)中，找一条权值最小的边(u',v'),将这条边加入到集合T中，将顶点v‘加入到集合U中。
3. 直到将V中所有的顶点加入U中，则算法结束，否则一直重复以上两步。
4. 符号说明：**我们用大写字母表示集合，用小些字母表示顶点元素，用<>表示两点之间的边**

为了更好的说明问题，我们下面一步一步来为大家展示这个过程

1. 初始状态：U = {a},V = {b,c,d,e} T = {}

<img src="https://i.loli.net/2021/05/13/z83vDr6NfACIwKy.png" alt="WX20210513-170649@2x.png" style="zoom:50%;" />

2. 集合U和V相关联的权值最小的边是<a,b>,于是我们将b加入U。

   ​			U = {a,b}, V = {d,c,e}, T = {<a,b>}

<img src="https://i.loli.net/2021/05/13/s6PwImTQhcvRdBa.png" alt="WX20210513-171509@2x.png" style="zoom:50%;" />

3. 此时集合U和V相关联的权值最小的边是<b,c>于是我们将c加入U。

   ​		U = {a,b,c}, V = {d,e}, T = {<a,b>,<b,c>}

<img src="https://i.loli.net/2021/05/13/gXEmeAxbkTLlyzF.png" alt="WX20210513-171851@2x.png" style="zoom:50%;" />

4. 显然此时集合U和V中相关联的权值最小的边是<c,d>,于是我们将d加入U

   ​	U = {a,b,c,d}, V = {e}, T = {<a,b>,<b,c>,<c,d>}

<img src="https://i.loli.net/2021/05/13/NmvfLErkgJDRAuT.png" alt="WX20210513-172204@2x.png" style="zoom:50%;" />

5. 最后集合U和V中相关联的权值最小的边是<d,e>于是将e加入U.

   ​	U = {a,b,c,d,e},V = {}, T = {<a,b>,<c,d>,<d,e>}

   <img src="https://i.loli.net/2021/05/13/aAJC5Wsg1S6lxDH.png" alt="WX20210513-172601@2x.png" style="zoom:50%;" />

```
 1//prime算法
 2//将城市X标记为visit=true时，就表示该城市加入到集合U，用sum累加记录边的总费用
 3
 4#include<iostream>
 5#define NO 99999999   //99999999代表两点之间不可达
 6#define N 5
 7using namespace std;
 8
 9bool visit[N];
10long long money[N] = { 0 };
11long long graph[N][N] = {0};
12
13void initgraph()
14{
15    for (int i = 0; i < N; i++)
16    {
17        for (int j = 0; j < N; j++)
18        {
19            scanf(" %lld", &graph[i][j]);
20        }
21    }
22
23}
24
25void printgraph()
26{
27    for (int i = 0; i < N; i++)
28    {
29        for (int j = 0; j < N; j++)
30        {
31            printf(" %lld", graph[i][j]);
32        }
33    }
34
35}
36
37int prim(int city)
38{
39    initgraph();
40    printgraph();
41    int index = city;
42    int sum = 0;
43    int i = 0;
44    int j = 0;
45    cout <<"访问节点：" <<index << "\n";
46    memset(visit, false, sizeof(visit));
47    visit[city] = true;
48    for (i = 0; i < N; i++)
49    {
50        money[i] = graph[city][i];//初始化，每个与城市city间相连的费用存入money，以便后续比较
51    }
52
53    for (i = 1; i < N; i++)
54    {
55        int minor = NO;
56        for (j = 0; j < N; j++)
57        {
58            if ((visit[j] == false) && money[j] < minor)  //找到未访问的城市中，与当前最小生成树中的城市间费用最小的城市
59            {
60                minor = money[j];
61                index = j;
62            }
63        }
64        visit[index] = true;
65        cout << "访问节点：" << index << "\n";
66        sum += minor; //求总的最低费用
67        /*这里是一个更新，如果未访问城市与当前城市间的费用更低，就更新money,保存更低的费用*/
68        for (j = 0; j < N; j++)
69        {
70            if ((visit[j] == false) && money[j]>graph[index][j])
71            {
72                money[j] = graph[index][j];
73            }
74        }
75    }
76    cout << endl;
77    return sum;               //返回总费用最小值
78}
79int main()
80{
81    cout << "修路最低总费用为："<< prim(0) << endl;//从城市0开始
82    return 0;
83}
```

### Kruskal算法

解最小生成树的另一种常见的算法是Kruskal算法。它比Prim算法更加直观。

Kruskal算法的做法是：每次都从剩余边中选取权重值最小的，当然，这条边不能使已有边产生回路。手动求解会发现Kruskal算法异常简单。如下所示：

<img src="https://i.loli.net/2021/05/13/5nxr9DL8cYfbh2o.png" alt="WX20210513-173424@2x.png" style="zoom:50%;" />

先对边的权值排个序：

1(v0,v4)	2(v2,v6)	4(v1,v3)	6(v1,v2)	8(v3,v6)	10(v5,v6)	12(v3,v5)	15(v4,v5)	20(v0,v1)

首选边1(v0,v4)	2(v2,v6)	4(v1,v3)	6(v1,v2)此时的图是这样

<img src="https://i.loli.net/2021/05/13/b2r7pufZsL3PXyQ.png" alt="WX20210513-174126@2x.png" style="zoom:50%;" />

显然，若选取边8(V3,V6)则会出现环，则必须抛弃8(V3,V6)，选择下一条10(V5,V6)没有问题，此时图变成这样

<img src="https://i.loli.net/2021/05/13/RDvWO9InKQVksdu.png" alt="WX20210513-175807@2x.png" style="zoom:50%;" />

显然，12(V3,V5)同样不可取，选取15(V4,V5)，边数已达到要求，算法结束。最终的图是这样的

<img src="https://i.loli.net/2021/05/13/c26BZYjT1tr7vpi.png" alt="WX20210513-180031@2x.png" style="zoom:50%;" />

算法逻辑很容易理解，但用代码判断当前边是否会引起环的出现则很棘手。这里简单提一提连通分量

* 在无向图中，如果从顶点vi到顶点vj有路径，则称vi和vj连通。如果图中任意两个顶点之间都连通，则称该图为连通图，否则，将其中较大的连通子图称为连通分量。
* 在有向图中，如果对于每一对顶点vi和vj，从vi到vj和从vj到vi都有路径，则称该图为强连通图；否则，将其中的极大连通子图称为强连通分量。

**算法说明**

为了判断环的出现，我们换个角度来理解Kruskal算法的做法：初始时，把图中的n个顶点看成是独立的n个连通分量，从树的角度看，也是n个根节点。我们选边的标准是这样的：若边上的两个顶点从属于两个不同的连通分量，则此边可取，否则考察下一条权值最小的边。
于是问题又来了，如何判断两个顶点是否属于同一个连通分量呢？这个可以参照并查集的做法解决。它的思路是：如果两个顶点的根节点是一样的，则显然是属于同一个连通分量。这也同样暗示着：在加入新边时，要更新父节点。

```
 1//kruskal算法
 2
 3#include<cstdio>
 4#include<iostream>
 5#include<cstring>
 6#include<cstdlib>
 7#include<algorithm>
 8#include<cmath>
 9#include<map>
10#include<set>
11#include<list>
12#include<vector>
13using namespace std;
14#define N 10005
15#define M 50005
16#define qm 100005
17#define INF 2147483647
18struct arr{
19    int ff, tt, ww;
20}c[M << 1];// 存储边的集合，ff，tt，ww为一条从ff连接到tt的权值为ww的边 
21int tot = 0;//边的总数 
22int ans = 0;//最小生成树的权值和 
23int f[N];//并查集 
24bool comp(const arr & a, const arr & b){
25    return a.ww < b.ww;
26}
27int m, n;//边数量，点数量 
28int getfa(int x){
29    return f[x] == x ? x : f[x] = getfa(f[x]);
30}//并查集，带路径压缩 
31
32inline void add(int x, int y, int z){
33    c[++tot].ff = x;
34    c[tot].tt = y;
35    c[tot].ww = z;
36    return;
37}//新增一条边 
38
39void kruscal(){
40    for (int i = 1; i <= n; i ++) f[i] = i;
41    for (int i = 1; i <= m; i ++){
42        int fx = getfa(c[i].ff);//寻找祖先 
43        int fy = getfa(c[i].tt);
44        if (fx != fy){//不在一个集合，合并加入一条边 
45            f[fx] = fy;
46            ans += c[i].ww;
47        }
48    }
49
50    return;
51} 
52int main(){
53    freopen("input10.txt", "r", stdin);
54    freopen("output10.txt", "w", stdout);
55    scanf("%d%d",&n, &m);
56    int x, y, z;
57    for (int i = 1; i <= m; i ++){
58        scanf("%d %d %d", &x, &y, &z);
59        add(x, y, z);
60    }
61    sort(c + 1, c + 1 + m, comp);//快速排序 
62    kruscal();
63    printf("%d\n", ans);
64    return 0;
65}
```

### Borůvka's algorithm

### Flow Network

* A flow network(or just network) N consists of 
  * A weighted digraph G with nonnegative integer edge weights, where the weight of an edge e is called the capacity c(e) of e
  * Two distinguished verices, s and t of G, called the source and snk repectiveley, such taht s has incoming edges and t has no outgoing edges

An example

<img src="https://i.loli.net/2021/05/13/CgzbrHcBvSAyOKD.png" alt="WX20210513-193030@2x.png" style="zoom:50%;" />

### Flow 

就是搞成两个集合一个是S集合也就是出发集合，一个是T集合，也就是终止集合，

如果存在大小为0的cut就说明不存在从s到t的路径

A flow f for a network N is an assignment of an integer value f(e) to each edge e that satisfies the following properties:

1. Capacity Rule: For each edge e, 0 ≤ f(e) ≤c(e)
2. Conservation Rule: For each vertex v ≠ s ,t 

<img src="https://i.loli.net/2021/05/13/W68iSClevb13XAk.png" alt="WX20210513-194222@2x.png" style="zoom:30%;" />

where E-(v) and E+ (v) are the incoming and outgoing edges fo v, respectively 

<img src="https://i.loli.net/2021/05/13/cILSTiUVAx4ht19.png" alt="WX20210513-194607@2x.png" style="zoom:50%;" />

The value of a flow f, denoted|f|, is the total folow from the source, which is the total flow into the sink.

Problem:Find a flow of maximum value?

### Cut

### Flow Augmentation

### Max-Flow and Min-Cut

### The Ford-Fulkerson Algorithm



































