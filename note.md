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
    - 【模板】区间最值操作 & 区间历史最值 P6242 **需要补题**
    - SP1557 GSS2 - Can you answer these queries II
- 历史和线段树 **需要学习 & 补题**
    - P8868 [NOIP2022] 比赛
    - CF1824D LuoTianyi and the Function
- 线段树合并
    - 【模板】线段树合并 P3224, P4556
    - P4577 [FJOI2018] 领导集团问题
- 线段树分裂 **需要学习**
    - 【模板】线段树分裂 P5494
- 线段树二分
    - P4559 [JSOI2018] 列队
- 线段树分治 **需要学习**
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

又称单词查找树，通过一种树形结构查找单词。典型应用是用于保存、统计和排序大量的字符串。

**例题** P2580, P5149

### K-D Tree

## 图论

## 字符串

### 哈希

通过较少的信息描述大量的信息。字符串哈希的本质是：把字符串看作一个进制为字符集大小的大整数，在模意义下的十进制值。因此，哈希值不同的字符串一定不同，相同的字符串的哈希值一定相同。

哈希值相同，原字符串不一定相同，这种情况称为**哈希冲突**。对此，哈希表等数据结构的处理方式是开散列或二次寻址；字符串匹配只能暴力扫一遍。实际竞赛中不常使用前述方法，而是尽可能使用优秀的哈希方法防止冲突。

#### 哈希冲突概率

对标准字符串哈希计算冲突概率，即 $hs = \sum\limits_{i = 1}^{n}base^{i - 1} \cdot s_i$。

形式化地，定义 $S$ 为输入空间，$T$ 为目标空间，$N = |T|$，$K$ 为输入样本数，$f$ 为哈希映射，有

$$S \stackrel{f} \longrightarrow T$$

假设映射 $f$ 遵从均匀分布，类比生日悖论，有（`collision` 是“碰撞”的英文）

$$P_{collision, N} = 1 - \sum\limits_{i = 0}^{K - 1}\frac i N$$

有估计

$$\lim_{K \rightarrow \infty} P_{collision, N} \sim 1 - e^{- \frac {K(K - 1)} {2N}}$$

可以发现，目标空间大小越大，则越不容易发生哈希冲突。

只需考虑如何设计一个趋近于均匀分布的哈希映射。

这是很难的，据实验，常见字符串哈希算法难以达到此效果。

我曾考虑使用方差分析其均匀分布程度，但是忘记实现了。因此我们不妨使用 $\begin{cases} base &= 31 \\ mod &= 37191016349 \end{cases}$ 吧。

**例题** P4513

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