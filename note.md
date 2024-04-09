# 总结

作者：王一乐  
本文在知识共享许可协议 CC BY-SA 4.0 之下提供。

> 追忆我近乎遗忘的。记录我正在了解的。展望我将要学习的。

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

### 单调队列优化 DP

**适用** 求极值，且决策点的贡献关于 $j$ 单调的转移方程。

每次弹出队首过期决策，取取队首为最优决策，弹出队尾劣于当前决策的决策点，加入当前决策点。

**例题** P6040

### 斜率优化 DP

**适用** 形如 $dp[i] = \max / \min \{dp[j] + f(i)g(j) + ...\}$，求极值，且最优决策与 $f(i)$ 和 $g(j)$ 的乘积有关的转移方程。

根据一次函数 $f(x) = kx + b ~ (k \ne 0)$：令 $f(x)$ 与 $dp[j]$ 有关；$x$ 与 $g(j)$ 有关；$k$ 与 $f(i)$ 有关；$b$ 与 $dp[i]$ 有关。极值便转化为最小 / 最大截距，使用凸壳维护，有三种情况：

1. 斜率和 $x$ 均单调：等价于单调队列，每次弹出不优队首，取队首为最优决策，弹出不构成凸壳的队尾，加入当前决策点；
2. $x$ 单调但斜率不单调：因为凸壳上斜率单调，所以每次二分最优决策，弹出不构成凸壳的队尾，加入当前决策点；
3. $x$ 不单调：用数据结构维护凸壳，每次把新决策点插入正确的位置。（缺少例题）

**例题** P3195, P4072, P5785

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

## 数论

### BSGS / exBSGS

解形如 $a^x \equiv b \pmod p$ 的同余方程，拓展版本可以 $(a, p) \ne 1$。BSGS 经过二次拓展可以解一定限制下的 $k$ 次同余方程。（详见 [OI-Wiki](https://oi.wiki/math/number-theory/discrete-logarithm/#%E8%BF%9B%E9%98%B6%E7%AF%87)）

标准 BSGS 因为 $(a, p) = 1$，所以通过逆元，只需预处理 $[0, \sqrt p)$ 范围内的所有整数 $i$ 的 $a^i \mod p$，每次只需判断是否存在 $a^i \cdot a^{k \sqrt p} \equiv b \pmod p$，用哈希表可以达到时间复杂度 $O(\sqrt p)$。

拓展 BSGS 因为 $(a, p) \ne 1$，所以不能直接使用逆元。$a^x \equiv b \pmod p \Rightarrow \frac a {d_1} \cdot a^{x - 1} \equiv \frac b {d_1} \pmod {\frac p {d_1}}$，如此重复直到 $(a, \frac p {d_1 d_2 \dots d_k}) = 1$。记 $D = d_1 d_2 \dots d_k$，原式转化为 $\frac {a^k} D \cdot a^{x - k} \equiv \frac b D \pmod {\frac p D}$，一定有 $(\frac {a^k} D, \frac p D) = 1$，即化为 $a^{x - k} \equiv \frac b {a^k} \pmod {\frac p D}$，用标准 BSGS 求解，答案加上 $k$ 即可。但需要特判答案小于 $k$ 的情况。

**例题** P2485, P3846, P4195

### 二次剩余

解形如 $x^2 \equiv a \pmod p$ 的同余方程，$p$ 为奇素数，有 Cipolla 算法。若 $p$ 不是奇素数，可以通过其他算法解决，这里不讨论。欧拉判别式：在上述条件下，$a$ 是模 $p$ 的二次剩余的充要条件是 $a^{\frac {p - 1} 2} \equiv 1 \pmod p$。Cipolla 算法通过找到 $r$ 使得 $r^2 - a$ 是模 $p$ 的二次非剩余，令 $\text i^2 = r^2 - a$，有两定理：$\text i^p \equiv -\text i \pmod p$；$(A + B)^{\text i} \equiv A^{\text i} + B^{\text i} \pmod p$。通过推导可知 $x^2 \equiv (a + \text i)^{p + 1} \pmod p$，即 $x \equiv \pm (a + \text i)^{\frac {p + 1} 2} \pmod p$。

**参考** [数论：二次剩余](https://www.luogu.com.cn/article/xm0o9xhw)

## 数值算法和线性代数

## 计算几何

最基础的内容不再赘述。

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
