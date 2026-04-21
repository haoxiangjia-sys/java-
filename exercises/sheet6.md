### 1. Big-O Notation

**Reminder**: $\log n$ denotes the binary logarithm, i.e., $\log n = \log_2 n$.

---

## Problem
Rank the following functions by order of growth: (no proof needed)

$$(\sqrt{2})^{\log n}, n^2, n!, (\log n)!, \left(\frac{3}{2}\right)^n, n^3, \log^2 n, \log(n!), 2^{2^n}, n \log n$$

**Hint**: Stirling's approximation for the factorial function can be helpful:

$$e\left(\frac{n}{e}\right)^n \leq n! \leq en\left(\frac{n}{e}\right)^n$$

---

## Solution

$$
\begin{align*}
O(\log^2 n) &\subseteq O\left((\sqrt{2})^{\log n}\right) \subseteq O(\log(n!)) \subseteq O(n \log n) \subseteq O(n^2) \\
&\subseteq O(n^3) \subseteq O((\log(n))!) \subseteq O\left(\left(\frac{3}{2}\right)^n\right) \subseteq O(n!) \subseteq O(2^{2^n})
\end{align*}
$$

# 第一部分：多项式与对数区（人类舒适区）

**分析链条：** $O(\log^2 n) \subseteq O((\sqrt{2})^{\log n}) \subseteq O(\log(n!)) \subseteq O(n \log n) \subseteq O(n^2)$

这一段展示了我们在日常算法设计中（如二分、分治、动态规划）最常打交道的复杂度量级。

## 1. 核心化简（扒掉伪装）

* **$(\sqrt{2})^{\log n}$ 的等价转换：**
  利用对数换底公式 $a^{\log_b c} = c^{\log_b a}$，我们可以将其化简为：
  $$(\sqrt{2})^{\log_2 n} = n^{\log_2 \sqrt{2}} = n^{0.5} = \sqrt{n}$$

* **$\log(n!)$ 的等价转换：**
  根据斯特林公式（Stirling's Approximation），$\log(n!) = \sum_{i=1}^{n} \log i$。在渐进复杂度下，它等价于：
  $$\log(n!) = \Theta(n \log n)$$

## 2. 逐级碾压逻辑

化简后，原本的链条变为清晰的：$\log^2 n \subseteq \sqrt{n} \subseteq n \log n \subseteq n \log n \subseteq n^2$

* **对数 vs 根号 ($O(\log^2 n) \subseteq O(\sqrt{n})$)：** 数学铁律：无论对数的常数次幂有多大（哪怕是 $\log^{100} n$），在 $n \to \infty$ 时，其增长速度永远慢于任何正数次幂的多项式（哪怕是 $n^{0.1}$）。
* **根号 vs 线性对数 ($O(\sqrt{n}) \subseteq O(n \log n)$)：** $\sqrt{n}$ 连一次方 $n$ 都无法超越，自然无法超越 $n \log n$。
* **双雄并立 ($O(\log(n!)) \subseteq O(n \log n)$)：** 这两者实际上是同阶的（$\Theta$ 关系）。它代表了基于比较的排序算法（如快速排序、归并排序）的性能天花板。
* **线性对数 vs 平方 ($O(n \log n) \subseteq O(n^2)$)：** 两边同时约去 $n$ 后，比较的是 $\log n$ 与 $n$。线性增长的 $n$ 毫无悬念地秒杀对数增长的 $\log n$。

---

# 第二部分：超越多项式与指数区（地狱难度区）

**分析链条：**
$$O(n^3) \subseteq O((\log n)!) \subseteq O\left(\left(\frac{3}{2}\right)^n\right) \subseteq O(n!) \subseteq O(2^{2^n})$$

这一段跨越了计算可行性的边界，展示了非确定性多项式时间（NP）问题暴力求解时面临的恐怖爆炸。为了清晰对比，我们对它们同时取对数来进行“降维打击”。

## 1. 多项式的极限 vs 准指数

**关系：** $O(n^3) \subseteq O((\log n)!)$
* **$n^3$ 取对数：** $3 \log n$
* **$(\log n)!$ 取对数：** $\approx (\log n) \cdot \log(\log n)$
* **分析：** 虽然大家都有 $\log n$，但 $n^3$ 的系数是固定的常数 $3$；而 $(\log n)!$ 的系数是 $\log(\log n)$。当 $n$ 足够大时，不断增长的 $\log(\log n)$ 必定会突破 $3$。因此，$(\log n)!$ 突破了所有多项式的天花板，属于准指数级（Sub-exponential）。

## 2. 准指数 vs 真指数

**关系：** $O((\log n)!) \subseteq O\left(\left(\frac{3}{2}\right)^n\right)$
* **准指数取对数：** $(\log n) \cdot \log(\log n)$
* **真指数取对数：** $n \cdot \log 1.5 \approx 0.58n$
* **分析：** 在真正的线性变量 $n$ 面前，任何对数的组合（$\log n$）都如同龟速。即使指数的底数很小（$1.5$），其本质的指数爆炸趋势也足以彻底碾压对数阶乘。

## 3. 常数底数 vs 膨胀底数（阶乘）

**关系：** $O\left(\left(\frac{3}{2}\right)^n\right) \subseteq O(n!)$
* **$1.5^n$ 取对数：** $0.58n$
* **$n!$ 取对数：** $\approx n \log n$
* **分析：** 两者都含有线性项 $n$。但指数函数的系数是静态的常量 $0.58$，而阶乘的系数是动态膨胀的 $\log n$。从底数的角度看，$n! \approx (n/e)^n$，当 $n$ 趋于无穷大时，底数 $n/e \gg 1.5$。

## 4. 阶乘 vs 双重指数

**关系：** $O(n!) \subseteq O(2^{2^n})$
* **$n!$ 取对数：** $n \log n$（降维后变成了多项式级的线性对数）
* **$2^{2^n}$ 取对数：** $2^n \cdot \log 2$（降维后依然是指数级）
* **分析：** 降维打击后立判高下。多项式级的 $n \log n$ 无论如何也追赶不上指数级的 $2^n$。双重指数是复杂度宇宙中的绝对黑洞。

---


### 2 kth Largest Element

## Problem
Give an algorithm that runs in time $O(n + k \log n)$ that computes the $k$th largest number in an array of $n$ distinct integers.

**Hint**: Think about Heapsort!

---

## Solution
In Heapsort, we can construct the tree in time $O(n)$. Then, we can run the first $k$ steps of the Heapsort algorithm, which places the $k$ largest elements at the end of the array. Each step of the sorting takes time $O(\log n)$ (which comes from the `Heapify()` operation). The total runtime therefore is $O(n + k \log n)$. 


### 3 Sorting

## Problem
We are given an array $A$ with $n + m$ elements so that the first $n$ elements are sorted and the last $m$ elements are unsorted.

---

### 1. What is the runtime of Insertionsort on array $A$?
**Solution**: $O(m(n + m))$. 

# 插入排序复杂度分析：部分有序数组

当给定一个数组 $A$，其中前 $n$ 个元素已经排好序，而后 $m$ 个元素是无序的。我们可以将插入排序的运行过程拆分为两个阶段来进行复杂度分析：

## 第一阶段：趟过平原（前 $n$ 个有序元素）

插入排序的逻辑是：每看到一个新元素，就跟前面的比，如果比前面的小，就往前换。但是，前 $n$ 个元素**已经是有序的**。

* 算法看第 2 个，比第 1 个大，不动（1 次比较，0 次交换）。
* 算法看第 $n$ 个，比第 $n-1$ 个大，不动（1 次比较，0 次交换）。

**账本：** 这一路顺风顺水，总共只做了约 $n$ 次比较，**耗时 $O(n)$**。

---

## 第二阶段：翻山越岭（后 $m$ 个无序元素）

好日子到头了，现在碰到了第 $n+1$ 个元素（也就是后 $m$ 个里的第 1 个）。因为它可能是无序的，在最坏情况下（比如它特别小），它需要一路往前交换，穿过前面所有的 $n$ 个元素，才能找到自己的位置。

* **后 $m$ 个的第 1 个：** 最坏往前挪 $n$ 步。
* **后 $m$ 个的第 2 个：** 最坏往前挪 $n+1$ 步。
* ...
* **后 $m$ 个的第 $m$ 个：** 最坏往前挪 $n+m-1$ 步。

**账本：** 这一段的运算量是一个等差数列求和：

$$\sum_{i=1}^{m} (n+i-1) = n + (n+1) + \dots + (n+m-1)$$

### 等差数列求和推导

根据等差数列求和公式：

$$\text{总和} = \frac{\text{项数} \times (\text{首项} + \text{末项})}{2}$$

代入我们的关键要素（首项为 $n$，末项为 $n+m-1$，项数为 $m$）：

$$\text{总和} = \frac{m \times (n + (n + m - 1))}{2}$$
$$\text{总和} = \frac{m \times (2n + m - 1)}{2}$$
$$\text{总和} = mn + \frac{m^2}{2} - \frac{m}{2}$$

在渐进时间复杂度（Big-O）分析中，我们遵循“抓大放小”的原则：去掉常数系数 $\frac{1}{2}$，并忽略在二次方 $m^2$ 面前微不足道的低次项 $\frac{m}{2}$，这大约等于：

$$m \times n + \frac{m^2}{2}$$

提取公因式 $m$ 后，得到第二阶段的时间复杂度：

$$O(mn + m^2) = O(m(n+m))$$

---

## 最终总结

整个算法的总耗时是两阶段之和：第一阶段的 $O(n)$ 加上第二阶段的 $O(m(n+m))$。

在绝大多数情况下（只要 $m \ge 1$），大头吃小头，最后的总时间复杂度就是被第二阶段主导的：

$$O(m(n+m))$$

---

### 2. Suppose that $m = O(1)$. How can we sort $A$ as efficiently as possible and what is the resulting runtime?
**Solution**: We can run Insertionsort on the unsorted elements. This would then take time $O(n)$. ✓

---

### 3. Suppose that $m = O(\sqrt{n})$. How can we sort $A$ as efficiently as possible and what is the resulting runtime?
**Solution**: We can run any $O(m \log m)$ sorting algorithm in order to sort the unsorted elements first. Then, we merge the two sorted parts in time $O(n+m)$, resulting in a sorting algorithm that runs in time $O(m \log(m) + n + m) = O(n + m \log m)$. If $m = O(\sqrt{n})$, then the final runtime is $O(n)$. ✓

---

**4. What is the largest value of $m$ so that we can obtain a runtime of $O(n)$? (difficult!)**

**Solution:** According to the previous exercise, the runtime is $O(m \log(m) + n)$. We need to identify the largest value for $m$ such that $O(m \log(m) + n) = O(n)$. This is equivalent to choosing the largest $m$ such that $O(m \log m) = O(n)$.

First, suppose that $m = \Theta(n / \log(n))$. Then:

$$
\begin{aligned}
m \log m &= O(n / \log(n) \cdot \log(n / \log(n))) \\
&= O(n / \log(n) \cdot (\log(n) - \log \log(n))) \\
&= O(n + n \log \log(n) / \log(n)) = O(n)
\end{aligned}
$$

since both $n$ and $n \log \log(n) / \log(n)$ are in $O(n)$.

Next, suppose that $m \in O(n)$ if $m = \Theta(f(n)n / \log(n))$, for some growing (superconstant) function $f$. Then:

$$
\begin{aligned}
m \log m &= O(f(n)n / \log(n) \cdot \log(f(n)n / \log(n))) \\
&= O(f(n)n / \log(n) \cdot (\log(f(n)) + \log(n) - \log \log(n))) \\
&= O(f(n) \log(f(n))n / \log(n) + f(n)n - f(n)n \log \log(n) / \log(n)) \notin O(n)
\end{aligned}
$$

since $f(n)n \notin O(n)$ (since $f(n)$ is increasing with $n$ and hence superconstant). This implies that the largest $m$ is in $\Theta(n / \log n)$.  

---

### 5. Suppose that $m = \Theta(n)$. How can we sort $A$ as efficiently as possible and what is the resulting runtime?
**Solution**: We can use any $O(n \log n)$ time sorting algorithm to obtain a total runtime of $O(n \log n)$. ✓






### 4 Decision Trees

---

### 1. Give a lower bound on the number of queries needed for sorting 4 elements.
**Solution**: At least 5 queries are needed. There are $4! = 24$ possible permutations, which correspond to the leaves in a decision tree. Any binary tree with 24 leaves has a height of at least 6. A root-to-leaf path of length 6 visits at least 5 internal nodes, which correspond to the number of queries. ✓

---

### 2. Give an optimal decision tree/guessing strategy for sorting 4 elements $a, b, c, d$ (draw the decision tree).
**Solution**:
```mermaid
graph TD
A{a < b?} -- Yes --> B{c < d?}
A -- No --> C{c < d?}

B -- Yes --> D{a < c?}
B -- No --> E["E (with role of c and d reversed)"]

C -- Yes --> F["F (with role of a and b reversed)"]
C -- No --> G["G (with role of a and b, and c and d reversed)"]

D -- Yes --> H{b < c?}
D -- No --> I{a < d?}

H -- Yes --> J[abcd]
H -- No --> K{b < d?}
K -- Yes --> L[acbd]
K -- No --> M[acdb]

I -- Yes --> N{b < d?}
I -- No --> O[cdab]
N -- Yes --> P[cabd]
N -- No --> Q[cadb]