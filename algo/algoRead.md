# 19
## 19.3关键字减值和删除一个结点

# 21 用于不相交集合的数据结构

## 21.3 不相交集合森林（并查集）

* 改进运行时间的启发式策略
1. 按秩合并：使具有较少结点的树指向具有较多结点的树的根
2. 路径压缩：使路径中的每个结点直接指向根

```
MAKE-SET(x):
    x.p = x
    x.rank =0

UNION(x,y):
    LINK(FIND-SET(x),FIND-SET(y))

LINK(x,y):
    if x.rank > y.rank:
        y.p = x
    else:
        x.p = y
        if x.rank == y.rank:
            y.rank = y.rank+1

FIND-SET(x):
    if x!= x.p:
<<<<<<< HEAD
        x.p = FIND-SET(x.p)
    return x.p
```

# 21.4 带路径压缩的按秩合并的分析

=======
        

```
>>>>>>> 4fdc35fa5049d5921ebc923b3ab56b9f47c4ed5c

# 22 基本的图算法
## 22.1 图的表示

## 22.2 深度优先搜索

## 22.3 广度优先搜索

## 22.4 拓扑排序
下面的算法可以对一个有向无环图进行拓扑排序：
```
TOPOLOGIALAL-SORT(G)    
    调用DFS(g)计算每个结点的time
    当每个节点完成时，插入到链表的头部
    返回链表
```

# 22.5 强联通分量
强联通分量：有向图G=(V,E)的强连通分量是一个最大结点集合C是V的子集，对与该集合中的任意一对结点u和v来说，路径u->v和v->u同时存在。
利用dfs算法求强连通分量：

```
STRONGLY-CONNECCTED-COMPONENTS(G):
    调用DFS(G)计算每个结点的完成时间u.f
    计算G的转置
    以完成时间逆序调用DFS
    输出每棵深度树的结点即为一个强连通分量
```

# 23 最小生成树
解决最小生成树问题的Kruskal算法和Prim算法的两种算法都是贪心算法。如果使用普通的二叉堆，那么可以很容易的将这两个算法的时间复杂度限制在O(ElogV)的数量级内。但如果使用斐波那契堆，Prim算法的运行时间可以改善为O(E+VlogV)。此运行时间在|V|远小于|E|的情况下较二叉堆有很大改进

## 23.1 最小生成树的形成

* 最小生成树的通用范式：
```
GENERIC-MST(G,w)
A=∅
while A 没有形成一个spanning树（全集树？）:
    找到一条安全边edge(u,v)
    A=A∪{(u,v)}
return A
```

* 安全边的辨别规则
 1.边(u,v)∈E的一个端点位于集合S，另一个端点位于V-S,则称该条边横跨切割(S,V-S)。如果集合A中不存在横跨该切割的边，则称该切割尊重集合A
 2.在一个横跨切割的所有边中，权重最小的边称为轻量级边

 ## 23.2 Kruskal算法和Prim算法

 * Kruskal算法
思路：在所有连接森林中两棵不同的树里面，找到权重最小的边(u,v)
```
MST-KRUSTRAL(G,w):
A=∅
for 每个结点 v∈G.V
    MAKE-SET(v)
按照权重w非递减顺序排列G.E中的边:
for edge(u,v) ∈ G.E，以权重非递减方式排列的边：
    if FIND-SET(v) ≠ FIND-SET(v):
        A=A∪{(u,v)}
        UNION(u,v)
retur A
```
<<<<<<< HEAD

* Prim 算法
思路：每一步在连接A和A之外的所有结点中，找到一条轻量级边加入到A中

```
MST-PRIM(G,w,r)
for each u∈G,V
    u.key = ∞
    u.π= nil
r.key =0 //根结点先弹出
Q=G.V
while Q!=∅:
    u = EXTRACT-MIN(Q)
    for each v 属于G.Agj[u]:
        if v ∈ Q and w(u,v)<v.key:
            v.π=u
            v.key = w(u,v)
```

# 24 单源最短路径

* 最短路径的几个变体
单目的地最短路径问题
单结点对最短路径问题
所有结点对的最短路径问题
最短路径的最优子结构

* 负权重的路径

* 环路
我们可以假定找到的最短路径上没有环路，即它们都是简单路径。由于图G=(V,E)中的任意无环路径最多包含|V|个不同的结点，它最多也包含|V|-1条边。因此，我们可以将注意力集中到只包含|V|-1条边的最短路径上

* 最短路径的表示

* 松弛操作
对于每个结点v来说，我们维持一个属性v.d，用来记录从源节点s到结点v的最短路径权重的上界。我们称v.d为s到v的最短路径估计。

```
INITIALIZE-SINGLE-SOURCE(G,s):
for each vertex v ∈ G.V:
    v.d = ∞
    v.π = NIL
s.d =0

//松弛操作

RELAX(u,v,w):
    if v.d > w.d + w(u,v):
        v.d = u.d+w(u,v)
        v.π = u
```
本章的所有算法都将调用INITIALIZE-SINGLE-SOURCE，然后重复对边进行松弛。不同之处是所有算法之间对每条边的松弛次数和松弛边的次序不同。Dijkstra算法和用于有向无环图的最短路径算法对每条边仅松弛一次。Bellman-Ford算法则对每条边松弛|V|-1次

* 五条性质
1. 三角不等式性质
2. 上界性质
3. 非路径性质
4. 收敛性质
5. 路径松弛性质
6. 前驱子图性质

## 24.1 Bellman-Ford算法
```
BELLMAN-FORD(G,w,s)
for i=1 to |G.V|-1:
    for each edge(u,v)∈ G.E
        RELAX(u,v,w)
for each edge(u,v)∈ G.E
    if v.d >u.d +w(u,v):
        return FALSE
return TRUE
```
## 24.2 有向无环图中的单源最短路径问题
根据有向无环图的拓扑排序来对带权重的有向五环图G=(V,E)进行边的松弛操作，我们便可以在O(V+E)时间内计算出从单个源点到所有结点之间的最短路径

```
DAG-SHORTTEST-PATHS(G,w,s)
对G 进行拓扑排序
INITIALIZE-SINGLE-SOURCE(G,s)
对于每个结点u，按照拓扑排序后的G：
    对于每个u的邻结点：
        RELAX(u,v,w)
```

## 24.3 Dijkstra算法
```
DIJKSTRA(G,w,s)
    INITIALIZE-SINGLE-SOURCE(G,s)
    S=∅
    Q=G.V
    while Q!=∅:
        u = EXTRACT-MIN(Q)
        S= S∪{u}
        for 每个 v∈G.Adj[u]:
            RELAX(u,v,w)
```

## 24.4 差分约束和最短路径
* 线性规划问题
* 差分约束系统
* 约束图
* 求解差分约束系统：Bellman-Ford算法

## 24.5 最短路径性质的证明


# 25 所有结点对的最短路径问题

## 25.1 最短路径和矩阵乘法
```
EXTEND-SHORTEST-PATHS(L,W)
n=L.rows
令 L'=(l'ij)为一个新的nxn矩阵
for i=1 to n
    for j=1 to n
        l'ij= ∞
        for k = 1 to n
            l'ij=min(l'ij,lik+wkj)
return L'

SQUARE-MATRIX-MULTIPLY(A,B)
n=A.rows
令 C 是一个新的nxn的矩阵
for i =1 to n
    for j=1 to n
        cij=0
        for k = 1 to n
            cij=cij+aik*bkj //这里其实每次还是需要比较的
return C

//下面采用重复平方的技术来计算上述矩阵序列
FASTER-ALL-PAIRS-SHORTEST-PATHS(W)
n=W.rows
L(1)=W
m = 1
while m <n-1:
    令 L(2m)为一个新矩阵
    L(2m) = EXTEND-SHORTEST-PATHS(L(m),L(m))
    m=2m
return L(m)
```

* 改进算法的运行时间

这样下来整个算法的时间复杂度降低到O(n*3\*logn)

## 25.2 Floyd-Warshall算法

* 最短路径的结构

* 所有结点对最短路径问题的一个递归解

* 自底向上计算最短路径权重

```
FLOYD-WARSHALL(W)
n =W.rows
D(0)=W
for k = 1 to n:
    令 D(k)=(dij(k))为一个新矩阵
    for i = 1 to n:
        for j = 1 to n:
            dij(k) = min(dij(k-1),dik(k-1)+dkj(k-1))
return D(n)
```

* 构建一条最短路径 （计算前驱矩阵）

* 有向图的传递闭包 （应用）
```
TRANSITIVE-CLOSURE(G)
n =|G.V|
令 T(0) = (tij(0))为一个新矩阵
for i= 1 to n
    for j = 1 to n
        if i == j or (i,j)∈ G.E
            tij(0)=1
        else tij(0)=0

for k = 1 to n:
    令 T(0) = (tij(k))为一个新矩阵
        for i = 1 to n
            for j = 1 to n
                tij(k) = tij(k-1) ∪(tik(k-1) ∩ tkj(k-1))
return T(n)
```

## 25.3 用于稀疏图的Johnson算法
Johnson算法可以在O(V^2logV+VE)的时间内找到所有结点对之间的最短路径。
Johnson使用的方法是重新赋予权重，新赋予的权重w'必须满足以下两个重要性质：
1. 对于所有结点对u,v∈V,一条路径p是在使用权重函数w时从结点u到结点v的一条最短路径，当且仅当p是在使用权重w'时从u到v的一条路径
2. 对于所有的边(u,v)，新权重w'(u,v)为非负值

* 重新赋予权重来维持最短路径
证明 w'(p)=w(p)+h(v0)-h(vk) 从而得出新的权重不影响最短路径的寻找

* 通过重新赋值来生成非负的权重

* 计算所有结点对之间的最短路径
```
JOHNSON(G,w):
compute G',G'V=G.V∪{s}
G'.E=G.E∪{(s,v):v∈G.V}，并且对于所有的v∈G.V,w(s,v)=0
if BELLMAN-FORD(G',w,s)==FALSE:
    打印包含负权重的边
else 
    对于所有的 v ∈ G'.V:
        设置 h(v)= BELLMAN-FORD算法计算的 lambda(s,v)权重
    对于所有的 edge(u,v) ∈ G'.E:
        w'(u,v) = w(u,v)+h(u)-h(v)
        令 D= (duv) 为一个新矩阵:
            对于每个 u ∈ G.V
                运行DIJKSTRA(G,w',u) 来计算所有 v∈ G.V 的lambda'(u,v)
                for v ∈ G.V
                    duv= lambda'(u,v)+ h(v)-h(u)
    return D
```

# 26 最大流
* 流网络和流
* 容量限制
* 流量守恒
* 解决反平行边问题
* 具有多个源节点和多个汇点的问题 (super source  super target)

## 26.2 Ford-Fulkerson方法
```
FORD-FULKERSON-METHOD(G,s,t)
初始化 f 为 0:
while 残存网络中存在一条增广路径:
    沿路径增加流
返回 f
```

* 残存网络
* 增广路径
* 流网络的切割
最大流最小切割定理：一个流网络中的最大流的值不能超过该网络最小切割的容量

* 基本的Ford-Fulkerson算法
```
FORD-FULKERSON(G,s,t)
    (u,v).f=0
while 在残存网络Gf中存在一条从s到t的增广路径p：
    cf(p)=min(cf(u,v):u,v在路径p中)
    对于路径p中的每条边：
        if (u,v)∈E：
            (u,v).f=(u,v).f+cf(p)
        else:
            (v,u).f=(u,v).f-cf(p)
```
FORD-FULKSON的时间复杂度取决于如何寻找增广路径。如果使用广度优先搜索，那么，时间复杂度将是多项式级别

* Edmonds-Karp算法


## 26.3 最大二分匹配

# 27 多线程算法

* 动态编程模型
包含两个特征：嵌套并行和并行循环。嵌套并行允许派生一个子过程，并且允许派生的子过程在计算自己的结果的同时调用者继续执行。并行循环如同普通的for循环一样，只因循环中的迭代可以并发执行

## 27.1 动态多线程基础
```
//伪代码下的动态多线程过程
P-FIB(n)
if n <=1
    return n
else x = spawn P-FIB(n-1)
     y = P-FIB(n-2)
     sync 
     return x+y
```

spawn 关键字并不意味着一个过程调用必须要与其派生子过程同时执行，这里只是允许这样。
sync 关键字表达了同步语义，一个过程只有使用sync关键字，才能安全地使用其派生子过程的返回值

* 性能度量
可以使用两种衡量标准来度量多线程算法的理论效率：工作效率和持续时间
1. 工作量：多线程计算的工作量是指在一个处理器上执行整个计算的总时间，换句话说，工作量就是每个链消耗时间的总和
2. 持续时间：持续时间则是计算有向无环图中沿着任意一条路径链的最长执行时间

工作量定律 Tp>=T1/P
持续时间定律 Tp>=T∞

加速比 T1/Tp
并行度 T1/T∞
松弛度 T1/(P*T∞)
=======
>>>>>>> 4fdc35fa5049d5921ebc923b3ab56b9f47c4ed5c
