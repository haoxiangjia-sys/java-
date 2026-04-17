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