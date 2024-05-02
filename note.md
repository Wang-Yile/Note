# 总结

> 作者：王一乐  
> 本文在知识共享许可协议 CC BY-SA 4.0 之下提供。

## DP

### 背包

#### 0-1 背包

$dp[j]$ 表示处理到第 $i$ 个物品，代价为 $j$ 的最大贡献。一般转移形如

$$dp[j] = \max\{dp[j - cost[i]] + value[i]\}$$

滚动数组后需要倒序枚举 $j$。

**例题** P1048, P1060, P1417

#### 完全背包

同 0-1 背包，但正序枚举 $j$。

**例题** P1616, P1853

#### 多重背包

A. 暴力枚举

B. 二进制拆分

把一个物品的数量限制 $k$ 拆分成 $2^0, 2^1, 2^2, \dots, 2^{\lfloor\log_2 k\rfloor}, 2^{\lceil\log_2 k\rceil} - 1 - k$，即转化为 0-1 背包。

C. 单调队列优化

$$\text{to be countinued.}$$

**例题** AcWing #6

#### 4. 分组背包 / 树上背包

$dp[u][j]$ 表示在 $u$ 的子树内，代价为 $j$ 的最大贡献。一般转移形如：

$$dp[u][j] = \max\{dp[v][j - k] + dp[v][k]\}$$

**例题** LOJ #160, P1064, P1273, P1757, P2014, P2015

### 状压 DP

通过一些整数值描述当前局面，为下一次决策提供参考。

**例题** P1896, P2150, P4363

### 区间 DP

通过合并区间的信息处理答案，需要先处理小区间后处理大区间。

可以采用记忆化搜索的方式简化代码实现。

**例题** P1880, P7914

### 数位 DP

数位 DP 本质是逐位填数，并且逐渐破除限制，最后归纳出共性，减少重复计数。

对于与数字（数位）有关的计数类型题目，例如有多少个符合条件的小于 $n$ 的非负整数，可以使用数位 DP。数位 DP 至少通过“当前处理的位”和“是否有最高位限制”两个状态控制是否答案的记忆化，有时需要“上一位填入的数”或者“是否有前导 $0$”等额外状态处理答案。

**例题** P2657

### 概率 DP

一般从初始状态推向结束状态，并结合概率知识设计转移方程。

### 期望 DP

常用策略：逆推。

**例题** CF605E, CF1810G

### 状态设计优化 DP

通过合并状态或者重新设计特征状态优化无用状态数，或者优化转移复杂度。需要结合具体题目具体分析。

**例题** P5664, CF1810G, AT_chokudai_S001_h

### 单调队列优化 DP

**适用** 求极值，且决策点的贡献关于 $j$ 单调的转移方程。

每次弹出队首过期决策，取取队首为最优决策，弹出队尾劣于当前决策的决策点，加入当前决策点。

**例题** P3957, P6040

### 斜率优化 DP

**适用** 形如 $dp[i] = \max / \min \{dp[j] + f(i)g(j) + ...\}$，求极值，且最优决策与 $f(i)$ 和 $g(j)$ 的乘积有关的转移方程。

根据一次函数 $f(x) = kx + b ~ (k \ne 0)$：令 $f(x)$ 与 $dp[j]$ 有关；$x$ 与 $g(j)$ 有关；$k$ 与 $f(i)$ 有关；$b$ 与 $dp[i]$ 有关。极值便转化为最小 / 最大截距，使用凸壳维护，有三种情况：

1. 斜率和 $x$ 均单调：等价于单调队列，每次弹出不优队首，取队首为最优决策，弹出不构成凸壳的队尾，加入当前决策点；
2. $x$ 单调但斜率不单调：因为凸壳上斜率单调，所以每次二分最优决策，弹出不构成凸壳的队尾，加入当前决策点；
3. $x$ 不单调：用数据结构维护凸壳，每次把新决策点插入正确的位置。（缺少例题）

**例题** P3195, P4072, P5785

### 其它 DP 优化

#### “斜率”优化 DP

**例题** CF1905F

## 数据结构

### 线段树

**例题**

- 线段树
    - 【模板】线段树 P3372
    - 【模板】乘加线段树 P2023, P3373
    - 【模板】李超线段树 P4097
- 可持久化线段树
    - 【模板】可持久化数组 P3919
    - 【模板】可持久化线段树（区间 k 小值） P3834
    - 【模板】单点修区间 k 小值 P2617
    - 【模板】可持久化并查集 P3402
    - P2633 / SP10628 Count on a tree
- 区间最值操作 & 区间历史最值线段树
    - 【模板】区间历史最值 P4314
    - 【模板】区间最值操作 & 区间历史最值 P6242
    - SP1557 GSS2 - Can you answer these queries II
- 历史和线段树
    - P8868 [NOIP2022] 比赛
    - CF1824D LuoTianyi and the Function
- 线段树合并
    - 【模板】线段树合并 P3224, P4556
    - P4577 [FJOI2018] 领导集团问题
    - P4197 Peaks / P7834 [ONTAK2010] Peaks 加强版
- 线段树分裂
    - 【模板】线段树分裂 P5494
- 线段树二分
    - P4559 [JSOI2018] 列队
- 线段树分治
    - 【模板】线段树分治 P5787

**好题**

- P4137 Rmq Problem / mex **需要补线段树解法**
- P4198 楼房重建
- P8969 幻梦 | Dream with Dynamic **需要补线段树解法**
- CF1149C Tree Generator™
- CF1192B Dynamic Diameter
- SP1043 GSS1 - Can you answer these queries I
- SP1716 GSS3 - Can you answer these queries III

**总结和反思**

- P4137 Rmq Problem / mex 和 SP1557 GSS2 的思路很像，都是离线、按询问右端点排序处理数据。
- 抄了很多题解。

### 树状数组

常数较线段树略小，只能维护前缀信息，可以利用树状数组的结构性质完成一些树套树（例如 P2617 单点修区间 k 小值）可以做逆序对。

二维树状数组是二维的树状数组。

**例题** P4514

### 0-1 Trie 树

按二进制位插入 Trie 树。

### Trie 树

又称单词查找树，通过一种树形结构查找单词。典型应用是保存、统计和排序大量的字符串。

**例题** P2580, P5149

### K-D Tree

## 图论

### 图的生成树

图的生成树是图的一个无环连通子图，且如果两点在图上连通，它们在生成树上仍连通。

#### Kruskal 算法和 Kruskal 重构树

Kruskal 算法用于寻找无向图的最小 / 最大生成树。以下内容均以最小生成树为例。

基于贪心思想，每次尝试将最小的边加入生成树，如果这条边连接的点在生成树上尚未连通，则这条边在生成树上。这样得到的生成树是 Kruskal 生成树。

当找到一条在生成树上的边时，会合并两个集合，此时新建一个点，点权为这条边的边权，左右儿子分别为这两个集合的根节点，并将新建点设为新集合的根。如此得到的树称为 Kruskal 重构树。

Kruskal 重构树有以下性质：

- 是一棵有根二叉树；
- 是一个大根堆；
- 有恰好 $n$ 个叶子节点；
- 重构树上 $\text{LCA}(u, v)$ 的权值表示原图上 $u$ 到 $v$ 的所有路径的最大边权最小值；
- 重构树上的叶子结点就是原图中的节点，非叶子节点都是原图的一条边；
- 如果原图不连通，则 Kruskal 重构树是重构树森林，每棵树独立满足所有 Kruskal 重构树的性质；
- 重构树上至多有 $2 \cdot n - 1$ 个节点，当且仅当原图连通时取等。

**例题** P1967, P7834, P9235

**参考** [Kruskal 重构树总结 - Luogu - LawrenceSivan](https://www.luogu.com.cn/article/jzk4d839)

### 图连通性

#### Tarjan 算法

找一棵 DFS 生成树，将进入点 $u$ 的时间戳定义为 $dfn_u$，从点 $u$ 开始不经过其与生成树上父亲的连边可以到达的最小的时间戳定义为 $low_u$，不妨定义该生成树为 Tarjan 生成树。基于此，处理图连通性问题。

#### 割点 / 点双连通分量

割点定义为：删除该点及其所有连边后，使得原图不连通的点。

在 Tarjan 生成树上，这表现为：
- 若 $u$ 是树根，则 $u$ 在树上有至少两个孩子；
- 否则只需 $low_v \ge dfn_u$。

形式化地，对于一个极大子图，如果其不存在割点，那么这个子图就是一个点双连通分量。  
需要指出，

**例题** P3388, P8435

#### 割边 / 边双连通分量

割边定义为：删除该边后，使得原图不连通的边。

在 Tarjan 生成树上，这表现为：点 $u$ 与点 $v$ 之间的连边是割边，当且仅当这样的边只有一条且 $low_v > dfn_u$。

形式化地，对于一个极大子图，如果其不存在割边，那么这个子图就是一个边双连通分量。

**例题** P8436

#### 圆方树

圆方树将无向图转化为树以处理一些问题。

对于一个无向图，其圆方树的构造过程如下：

- 原图中的点被称为**圆点**。
- 求得原图中所有点双连通分量，对每一个点双都新建一个**方点**；
- 每个方点向其对应的点双连通分量里的所有圆点连边，这些连边组成圆方树。

圆方树有以下性质：

- 圆点仅与方点连边，方点仅与圆点连边；
- 任何一条路径都是圆点和方点交错出现的；
- 如果原图连通，则圆方树是一棵树；

**例题** CF487E

### 图的匹配

图的匹配是无向图的一个边集，该边集内所有的边不共端点。

#### 二分图最大匹配

##### 增广路算法

增广路算法的过程是尝试将当前点加入匹配，枚举该点可到达的未处理过的点。如果未匹配则将其与当前点匹配；否则尝试拆除其所在的匹配，再与当前点匹配。

其本质为寻找一条增广路，其两端的边均未匹配，然后执行增广，把路径上的匹配与未匹配反转，于是增加了一个匹配数。

根据**增广路定理**，当图上不存在增广路时，得到最大匹配。

有两种实现方式。

**DFS 版**

十分简单。

**BFS 版**

相对麻烦，但是是带花树算法的基础。

##### 网络流建模

进行二分图染色，每条边从黑点向白点定向，源点连向所有黑点，所有白点连向汇点，容量均为 $1$，最大流即可。

#### 一般图最大匹配（带花树算法 Blossom Algorithm）

带花树算法是扩展的增广路算法，通过处理奇环实现在一般图上的运作。_无需理会为什么会有某些规定，因为在增广路算法中就是如此，只不过这里特别强调出来。_

带花树算法基于 BFS 版的增广路算法。其在寻找点 $x$ 开始的增广路时会得到一棵 BFS 生成树。

定义标记 $col_u$：（距离定义为两点之间最短路径的边数）

- 若点 $u$ 未访问过，则 $col_u = 0$；
- 若点 $u$ 在生成树上，且与 $x$ 的距离为 **偶数**，则 $col_u = 1$；
- 若点 $u$ 在生成树上，且与 $x$ 的距离为 **奇数**，则 $col_u = 2$；

规定在 BFS 的过程中，进入队列的只有 $col_u = 1$ 的点 $u$。

$pre_u, match_u$ 变量与增广路算法保持一致。

---

定义 **花** 表示连通的一些点组成的点集，**缩花** 即为合并两个点集。

扫描 $u$ 的出边连向的点 $v$ 时，有以下情况：

- $col_v = 0$
    - $match_v = 0$，说明已找到增广路，增广即可。
    - $match_v \ne 0$，同增广路算法，将 $match_v$ 入队，设置 $col_v = 2, col_{match_v} = 1$；
- 否则
    - $u$ 与 $v$ 在同一朵花内，忽略。
    - $col_v = 1$，说明找到奇环，需要 **缩花**。
    - $col_v = 2$，说明找到偶环，增广路算法可以正确处理，忽略。

---

接下来讨论 **缩花**。

**定理** 设原图为 $G$，缩花后的图为 $G'$，则

- 若 $G$ 上存在增广路，则 $G'$ 上也存在；
- 若 $G'$ 上存在增广路，则 $G$ 上也存在。

为了方便，设缩花后的花根存放在与 $x$ 距离最小的点上。

设将 $u$ 和 $v$ 缩花，$u$ 的总花根为 $rt$。

考虑寻找总花根：先跳到 $u$ 和 $v$ 各自的分花根，不断设置 $u = pre_{match_u}, v = pre_{match_v}$，也就是向生成树的父亲的方向跳两级，直到 $u = v$，此时 $u$ 为总花根。

然后进行 **收缩（Shrink）** 操作，将 $u - rt$ 和 $v - rt$ 两条链缩到总花根上。

不妨考虑收缩 $u - rt$ 这条链：反向建立 $pre$，将所有链上 $col = 2$ 的点向外增广（入队），并将链上的分花根合并到总花根上。

---

模拟缩花工作流程：尝试对 $x$ 增广。

![](https://cdn.luogu.com.cn/upload/image_hosting/2wm291sk.png)

其中 $1 \leftrightarrow 2, 3 \leftrightarrow u, 4 \leftrightarrow v$ 是三条已匹配边，$col_x = col_2 = col_u = col_v = 1, col_1 = col_3 = col_4 = 2$。

此时找到 $u \leftrightarrow v$ 连接了两个 $col = 1$ 的点，说明有奇环。

寻找总花根：已跳至 $u, v$ 各自的分花根。$u$ 跳两级得到 $2$，$v$ 跳两级也得到 $2$，说明 $2$ 是总花根。

![](https://cdn.luogu.com.cn/upload/image_hosting/3pxwv7n4.png)

缩花

![](https://cdn.luogu.com.cn/upload/image_hosting/1bn4y903.png)

收缩路径 $u - 2$，将 $3$ 入队，$pre_u = v$。收缩路径 $v - 2$，将 $4$ 入队，$pre_v = u$。图中黄色表示原来的 $pre$，橙色表示被修改的 $pre$。

![](https://cdn.luogu.com.cn/upload/image_hosting/gepxt9c9.png)

于是完成了一次缩花，本次缩花并未增加匹配数。

**例题** P6113

**参考** [一般图最大匹配学习笔记 - Luogu - lanos212](https://www.luogu.com.cn/article/yrj6im2x) [一般图最大匹配 - OI Wiki](https://oi-wiki.org/graph/graph-matching/general-match/)

## 字符串

### 哈希

通过较少的信息描述大量的信息。哈希值不同的字符串一定不同，相同的字符串的哈希值一定相同。

哈希值相同，原字符串不一定相同，这种情况称为**哈希冲突**。对此，哈希表等数据结构的处理方式是开散列或二次寻址；字符串匹配只能暴力扫一遍。实际竞赛中不常使用前述方法，而是尽可能使用优秀的哈希方法防止冲突。

以下是一些常见哈希方法。

#### 标准字符串哈希（BKDRHash）

BKDRHash 的本质是：把字符串看作一个进制为 $base$ 的大整数，在模意义下的十进制数值。

字符串 $s$ 的 BKDRHash 值定义为

$$hs_s = \sum\limits_{i = 1}^{|s|} s_i \cdot base^{|s| - i}$$

#### 数列哈希

数列 $a_1, a_2, \dots, a_n$ 的哈希值定义为 $base^{a_1} + base^{a_2} + \dots + base^{a_n}$。

#### 随机哈希

即通过随机值替换 $base^k$。

还有很多不同的哈希方法，例如 [基于 sin 的 Hash](https://www.luogu.com.cn/article/ih4e3v2o)、[APHash](https://ieeexplore.ieee.org/document/8462326/) [等](https://www.cnblogs.com/Stomach-ache/p/3724836.html)。

**例题** P4513, P6688

### 后缀数组

定义 $sa_i$ 表示排序后第 $i$ 小的后缀，$rk_i$ 表示后缀 $i$ 的排名。

#### $O(n \log^2 n)$ 求法

基于倍增思想，先处理所有长度为 $1$ 的子串的 $sa$ 和 $rk'$ 数组。

假设已处理出长度为 $w$ 的子串的答案，从 $w$ 推向 $2w$：  
以 $rk'_i$ 作为第一关键字，$rk'_{i + w}$ 作为第二关键字对 $sa$ 进行排序。  
即对每个子串 $s[i \dots \min\{i + w - 1, n\}]$ 排序。  
特别地，当 $i + w > n$ 时，认为 $rk'_{i + w}$ 足够小。  
然后根据排序后的 $sa$ 数组重新处理 $rk'$ 数组即可。

#### $O(n \log n)$ 求法

发现上面方法的一个复杂度瓶颈在于排序算法是 $O(n \log n)$ 的。但实际上关键字值域只有 $O(n)$ 级别（除第一次排序外），可以考虑基于值域的排序方式。因为需要二维关键字排序，所以使用[基数排序](https://oi.wiki/basic/radix-sort/)，可以实现 $O(n \log n)$。

#### SA-IS

一种线性进行后缀排序的算法。参见：[诱导排序与 SA-IS 算法](https://riteme.site/blog/2016-6-19/sais.html)。

**例题** P3809, P4051

## 数论

### 整除理论

#### 算术基本定理（唯一分解定理）

任何一个大于 $1$ 的自然数 $n$，如果 $n$ 不为素数，那么 $n$ 可以唯一将其分解为有限个素数的乘积

$$n = p_1^{a_1} p_2^{a_2} \dots p_k^{a_k}$$

其中 $p_1, p_2, \dots, p_k$ 为互不相等的素数，指数 $a_i$ 为正整数。该分解式被称为 $n$ 的标准分解（唯一分解）。

#### 数论分块

数论分块一般用于求解和式

$$S(n) = \sum\limits_{i = 1}^n f(i) g(\lfloor \frac n i \rfloor)$$

其中 $f$ 的前缀和与 $g$ 均容易计算。

记 $s(x) = \sum\limits_{i = 1}^x f(i)$，伪代码如下

$$
\begin{array}{ll}
l = 1 \\
\text{while} ~ l \le n: \\
\qquad r = \left\lfloor \dfrac {n} {\left\lfloor \frac n l \right\rfloor} \right\rfloor \\
\qquad ans += (s(r) - s(l - 1)) \cdot \left\lfloor \dfrac n l \right\rfloor \\
\qquad l = r + 1
\end{array}
$$

### 数论函数和筛法

#### 积性函数

积性函数：对于任何互素的整数有 $f(a \cdot b) = f(a) \cdot f(b)$ 的数论函数。  
完全积性函数：对于任何整数有 $f(a \cdot b) = f(a) \cdot f(b)$ 的数论函数。

常见积性函数：欧拉函数 $\varphi$，莫比乌斯函数 $\mu$，因数个数函数 $\tau$，因数和函数 $\sigma$。

$\pi$ 函数不是积性函数。

**性质 1** 若 $f(x), g(x)$ 均为积性函数，则 $h(x) = f(x) \cdot g(x)$ 也为积性函数。

#### 欧拉函数

欧拉函数 $\varphi(n)$ 描述小于 $n$ 的与 $n$ 互素的正整数个数。

**计算公式**

$$\varphi(n) = n \cdot \prod\limits_{p \mid n}{(1 - p^{-1})}$$

**欧拉定理** 若正整数 $a, p$ 互素，$a^{\varphi(p)} \equiv 1 \pmod p$。

**欧拉降幂** 若 $k > \varphi(p)$，$a^k \equiv a^{k \mod \varphi(p) + \varphi(p)} \pmod p$。

**性质 1（欧拉反演）**

$$n = \sum\limits_{d \mid n}\varphi(d)$$

推广

$$(i, j) = \sum\limits_{d \mid (i, j)}\varphi(d)$$

**线性筛**

```cpp
phi[1] = 1;
for (int i = 2; i <= n; ++i) {
    if (!vis[i]) {
        pr[++tail] = i;
        phi[i] = i - 1;
    }
    for (int j = 1; j <= tail && i * pr[j] <= n; ++j) {
        vis[i * pr[j]] = true;
        if (i % pr[j] == 0) {
            phi[i * pr[j]] = phi[i] * pr[j];
            break;
        }
        phi[i * pr[j]] = phi[i] * phi[pr[j]];
    }
}
```

**例题（欧拉定理）** P1405, P5091, P8412

**例题（欧拉反演）** P1891, CF1900D, SP3871, SP5971, UVA11417, UVA11424, UVA11426

#### 莫比乌斯函数

**定义**

$$\mu(n) = \begin{cases} 1, & n = 1, \\ 0, & \exist x \in \mathbf{N}, x \in [2, +\infty), x^2 \mid n, \\ (-1)^k, &\text{otherwise, k 是 n 本质不同的素因子个数}.\end{cases}$$

**性质 1（莫比乌斯反演）** $*$ 表示狄利克雷卷积，则

$$\begin{aligned} \varphi * 1 & = \varepsilon \\ \varepsilon * \mu & = \varphi \end{aligned}$$

即

$$\sum\limits_{d \mid n} \mu(d) = \begin{cases} 1, & n = 1, \\ 0, & \text{otherwise}.\end{cases} = \varepsilon(n)$$

推广

$$[(i, j) = 1] = \sum\limits_{d \mid (i, j)} \mu(d)$$

**线性筛**

```cpp
mu[1] = 1;
for (int i = 2; i <= n; ++i) {
    if (!vis[i]) {
        pr[++tail] = i;
        mu[i] = -1;
    }
    for (int j = 1; j <= tail && i * pr[j] <= n; ++j) {
        vis[i * pr[j]] = true;
        if (i % pr[j] == 0) {
            mu[i * pr[j]] = 0;
            break;
        }
        mu[i * pr[j]] = -mu[i];
    }
}
```

**例题** P1447, P1829, P2257, P2522, P2568, P3327, P3768, SP5971, UVA12888

#### 杜教筛

求数论函数 $f$ 的前缀和 $S$。

$$S(n) = \sum\limits_{i = 1}^n f(i)$$

考虑一个容易求前缀和的函数的 $g$，接下来 $*$ 表示狄利克雷卷积。

$$
\begin{aligned}
&\sum\limits_{i = 1}^n (f * g)(i) \\
= &\sum\limits_{i = 1}^n \sum\limits_{d \mid i} g(d) f(\frac i d) \\
= &\sum\limits_{d = 1}^n g(d) \sum\limits_{i = 1}^{\lfloor \frac n d \rfloor} f(i) \\
= &\sum\limits_{d = 1}^n g(d) S(\lfloor \frac n d \rfloor) \\
= & g(1) S(n) + \sum\limits_{d = 2}^n g(d) S(\lfloor \frac n d \rfloor)
\end{aligned}
$$

所以

$$
\begin{aligned}
g(1) S(n) + \sum\limits_{d = 2}^n g(d) S(\lfloor \frac n d \rfloor) &= \sum\limits_{i = 1}^n (f * g)(i) \\
S(n) &= \dfrac {\sum\limits_{i = 1}^n (f * g)(i) - \sum\limits_{d = 2}^n g(d) S(\lfloor \frac n d \rfloor)} {g(1)}
\end{aligned}
$$

可以对 $\sum\limits_{d = 2}^n g(d) S(\lfloor \frac n d \rfloor)$ 使用数论分块，且 $\sum\limits_{i = 1}^n (f * g)(i)$ 容易求得，记忆化搜索即可。

例如，求

$$S(n) = \sum\limits_{i = 1}^n \varphi(i)$$

知

$$\varphi * 1 = \text{id}$$

代入，得

$$
\begin{aligned}
S(n) &= \dfrac {\sum\limits_{i = 1}^n \text{id}(i) - \sum\limits_{d = 2}^n 1(d) S(\lfloor \frac n d \rfloor)} {1(1)} \\
&= \dfrac {n (n+1)} {2} - \sum\limits_{d = 2}^n S(\lfloor \frac n d \rfloor)
\end{aligned}
$$

数论分块即可。

**例题** P4213

### 同余理论

#### BSGS / exBSGS

解形如 $a^x \equiv b \pmod p$ 的同余方程，拓展版本可以 $(a, p) \ne 1$。BSGS 的拓展还可以解一定限制下的 $k$ 次同余方程。（详见 [OI-Wiki](https://oi.wiki/math/number-theory/discrete-logarithm/#%E8%BF%9B%E9%98%B6%E7%AF%87)）

标准 BSGS 因为 $(a, p) = 1$，所以通过逆元，只需预处理 $[0, \sqrt p)$ 范围内的所有整数 $i$ 的 $a^i \mod p$，每次只需判断是否存在 $a^i \cdot a^{k \sqrt p} \equiv b \pmod p$，用哈希表可以达到时间复杂度 $O(\sqrt p)$。

拓展 BSGS 因为 $(a, p) \ne 1$，所以不能直接使用逆元。$a^x \equiv b \pmod p \Rightarrow \frac a {d_1} \cdot a^{x - 1} \equiv \frac b {d_1} \pmod {\frac p {d_1}}$，如此重复直到 $(a, \frac p {d_1 d_2 \dots d_k}) = 1$。记 $D = d_1 d_2 \dots d_k$，原式转化为 $\frac {a^k} D \cdot a^{x - k} \equiv \frac b D \pmod {\frac p D}$，一定有 $(\frac {a^k} D, \frac p D) = 1$，即化为 $a^{x - k} \equiv \frac b {a^k} \pmod {\frac p D}$，用标准 BSGS 求解，答案加上 $k$ 即可。但需要特判答案小于 $k$ 的情况。

**例题** P2485, P3846, P4195

#### 二次剩余

解形如 $x^2 \equiv a \pmod p$ 的同余方程，$p$ 为奇素数，有 Cipolla 算法。若 $p$ 不是奇素数，可以通过其他算法解决，这里不讨论。欧拉判别式：在上述条件下，$a$ 是模 $p$ 的二次剩余的充要条件是 $a^{\frac {p - 1} 2} \equiv 1 \pmod p$。Cipolla 算法通过找到 $r$ 使得 $r^2 - a$ 是模 $p$ 的二次非剩余，令 $\text i^2 = r^2 - a$，有两定理：$\text i^p \equiv -\text i \pmod p$；$(A + B)^{\text i} \equiv A^{\text i} + B^{\text i} \pmod p$。通过推导可知 $x^2 \equiv (a + \text i)^{p + 1} \pmod p$，即 $x \equiv \pm (a + \text i)^{\frac {p + 1} 2} \pmod p$。

**参考** [数论：二次剩余](https://www.luogu.com.cn/article/xm0o9xhw)

### 不定方程

#### 裴蜀定理

关于 $x, y$ 的不定方程

$$ax + by = c$$

有整数解的充要条件是 $(a, b) \mid c$。

推广：关于 $x_1, x_2, \dots, x_n$ 的不定方程

$$a_1x_1 + a_2x_2 + \dots + a_nx_n = c$$

有整数解的充要条件是 $(a_1, a_2, \dots, a_n) \mid c$。

#### GCD / exGCD

### 连分数理论

## 数值算法和线性代数

## 计算几何

### 弧度制和角度制

角度制：以 $1 \degree$ 为单位；  
弧度制：以 $1 ~\text{rad}$ 为单位。  
$1 ~\text{rad} = \frac {180} \pi \degree$，$1 \degree = \frac \pi {180} ~\text{rad}$。

C++ 的三角函数接受以弧度为单位的参数，反三角函数返回以弧度为单位的结果。

### 两点距离

平面两点距离公式

$$dis = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}$$

高维推广

$$dis = \sqrt{(a_1 - b_1)^2 + (a_2 - b_2)^2 + \dots + (a_k - b_k)^2}$$

**例题** P2625

### 点与三角形的关系

可以利用向量的夹角（数量积的变形）判断，另一种方法是利用叉积（可惜我不会），或者转换坐标系（这用在纹理着色上）。

**例题** P1355

### 线段关系

分两步进行：

1. 快速排斥；
2. 跨立实验。

## 莫队和分块思想

### 普通莫队

离线询问，按所在块为第一关键字、右端点为第二关键字排序，每次收缩当前区间至询问区间，并回答询问。如果收缩区间的时间复杂度为 $O(1)$，那么莫队的时间复杂度为 $O(m \sqrt n)$。

### 根号分治

通过在不同情况下使用复杂度为两个极端的暴力，达到相对均衡的时间复杂度。

**例题** CF506D, ABC259Ex

### 其他分块思想

BSGS / exBSGS。