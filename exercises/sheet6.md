# 1. Big-O Notation

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

# 渐进时间复杂度分析：常见函数的增长率排序

在算法分析中，比较不同函数的渐进增长率（Asymptotic Order of Growth）是评估算法性能的核心基础。本节将针对一组复杂函数进行严格的代数化简与阶（Order）的排序。

**分析对象（待排序函数）：**
$(\sqrt{2})^{\log n}, n^2, n!, (\log n)!, (\frac{3}{2})^n, n^3, \log^2 n, \log(n!), 2^{2^n}, n \log n$

*(注：默认对数底数为 2，即 $\log n = \log_2 n$)*

---

## 一、 核心函数的代数化简与等价转换

在进行增长率比较之前，必须利用数学恒等式对部分“伪装”的函数进行化简，将其还原为标准形式。

1. **对数指数互换法则：** 对于函数 $(\sqrt{2})^{\log n}$，根据对数恒等式 $a^{\log_b c} = c^{\log_b a}$，可得：
   $$(\sqrt{2})^{\log_2 n} = n^{\log_2 \sqrt{2}} = n^{0.5} = \sqrt{n}$$
   **结论：** $(\sqrt{2})^{\log n} \in \Theta(n^{0.5})$

2. **阶乘的对数与斯特林公式（Stirling's Approximation）：**
   对于 $\log(n!)$，根据对数的求和性质：$\log(n!) = \sum_{i=1}^{n} \log i$。
   利用积分逼近或题目提供的斯特林公式边界推导，可知：
   $$\log(n!) = \Theta(n \log n)$$
   **结论：** $\log(n!)$ 与 $n \log n$ 同阶，属于线性对数级。

---

## 二、 函数的渐进量级分类与排序

基于化简结果，我们可以将这些函数严格划分为五个由慢至快的渐进量级（Complexity Classes）。根据极限理论 $\lim_{n \to \infty} \frac{f(n)}{g(n)}$ 的收敛性，排序如下：

### 1. 对数多项式阶 (Polylogarithmic)
* **$\log^2 n$** 对数函数的任何常数次幂，其增长率严格低于任何正数次幂的多项式函数。

### 2. 多项式与线性对数阶 (Polynomial & Linearithmic)
此类别函数满足 $O(n^k)$ 的形式（$k$ 为常数）。
* **$\sqrt{n}$**：即 $(\sqrt{2})^{\log n}$，对应 $k = 0.5$。
* **$n \log n$** 及 **$\log(n!)$**：线性对数阶，增长率高于 $n^{1-\epsilon}$ 且低于 $n^{1+\epsilon}$。
* **$n^2$**：二次方阶。
* **$n^3$**：三次方阶。
**内部排序：** $\sqrt{n} \subset \log(n!) \subset n \log n \subset n^2 \subset n^3$

### 3. 超越多项式/准指数阶 (Super-polynomial / Sub-exponential)
* **$(\log n)!$**
  将其展开并取对数：$\log((\log n)!) \approx (\log n) \cdot \log(\log n)$。
  将其转化为以 $n$ 为底的形式：$(\log n)! \approx n^{\log(\log n / e)}$。
  由于其指数部分 $\log(\log n/e)$ 随 $n$ 缓慢递增趋于无穷，因此它严格大于任何常数多项式 $n^k$，但严格小于任何底数大于 1 的指数函数 $c^n$。

### 4. 指数与阶乘阶 (Exponential & Factorial)
* **$(\frac{3}{2})^n$**：底数为常数 1.5 的标准指数函数。
* **$n!$**：根据斯特林公式推论 $n! \sim \sqrt{2\pi n}(\frac{n}{e})^n$，可将其视为底数为 $\frac{n}{e}$（随 $n$ 递增）的指数函数。由于当 $n$ 足够大时，$\frac{n}{e} \gg 1.5$，故 $n!$ 的增长率远超 $(\frac{3}{2})^n$。

### 5. 双重指数阶 (Double Exponential)
* **$2^{2^n}$**
  此为最高级别的爆炸性增长。可通过对指数阶和阶乘阶取对数来证明其统治地位：
  $\log(n!) \approx n \log n$
  $\log(2^{2^n}) = 2^n$
  显然 $2^n$ 远大于 $n \log n$，故 $2^{2^n} \gg n!$。

---

## 三、 最终结论

综合上述理论推导，以大 O 记号（Big-O Notation）表示各函数的包含关系（$\subseteq$ 表示渐进界限的从属关系），最终的严格升序排列为：

$$
\begin{align*}
O(\log^2 n) &\subseteq O((\sqrt{2})^{\log n}) \\
&\subseteq O(\log(n!)) \subseteq O(n \log n) \\
&\subseteq O(n^2) \subseteq O(n^3) \\
&\subseteq O((\log n)!) \\
&\subseteq O\left(\left(\frac{3}{2}\right)^n\right) \subseteq O(n!) \\
&\subseteq O(2^{2^n})
\end{align*}
$$


# 2 kth Largest Element

## Problem
Give an algorithm that runs in time $O(n + k \log n)$ that computes the $k$th largest number in an array of $n$ distinct integers.

**Hint**: Think about Heapsort!

---

## Solution
In Heapsort, we can construct the tree in time $O(n)$. Then, we can run the first $k$ steps of the Heapsort algorithm, which places the $k$ largest elements at the end of the array. Each step of the sorting takes time $O(\log n)$ (which comes from the `Heapify()` operation). The total runtime therefore is $O(n + k \log n)$. 


# 3 Sorting

## Problem
We are given an array $A$ with $n + m$ elements so that the first $n$ elements are sorted and the last $m$ elements are unsorted.

---

### 1. What is the runtime of Insertionsort on array $A$?
**Solution**: $O(m(n + m))$. ✓

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






# 4 Decision Trees

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