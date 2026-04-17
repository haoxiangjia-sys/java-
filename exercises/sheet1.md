# 📘 Exercise Sheet 1 – Solutions

**COMS10018 Algorithms**

> 📌 Reminder:
> `log n` 表示二进制对数（log₂ n）

---

## ✏️ Example: Big-O Notation

### Problem

证明：
$$
5\sqrt{n} \in O(n)
$$

### Solution

我们需要找到常数 $c, n_0 > 0$，使得：
$$
5\sqrt{n} \leq c \cdot n \quad \forall n \geq n_0
$$

等价于：
$$
\left(\frac{5}{c}\right)^2 \leq n
$$

取：

* $c = 5$
* $n_0 = 1$

则对所有 $n \geq 1$ 成立 ✅

---

## 🔢 1. O-notation: Part I

### (1)

$$
n^2 + 10n + 8 \in O\left(\tfrac{1}{2}n^2\right)
$$

**Proof:**

对于 $n \geq 1$：
$$
n^2 + 10n + 8 \leq 19n^2
$$

取：

* $c = 38$
* $n_0 = 1$

---

### (2)

$$
n^3 + n^2 + n \in O(n^3)
$$

$$
n^3 + n^2 + n \leq 3n^3 \quad (n \geq 1)
$$

取：

* $c = 3$
* $n_0 = 1$

---

### (3)

$$
10 \in O(1)
$$

取：

* $c = 10$
* 任意 $n_0$

---

### (4)

$$
\sum_{i=1}^n i \in O(4n^2)
$$

$$
\sum_{i=1}^n i = \frac{n(n+1)}{2} = \frac{n^2}{2} + \frac{n}{2}
$$

对于 $n \geq 1$，有 $n \leq n^2$

取：

* $c = 1$
* $n_0 = 1$

---

## 🏁 2. Racetrack Principle

### Problem

证明：
$$
n \leq e^n \quad \forall n \geq 1
$$

### Proof

初始：
$$
1 \leq e
$$

导数：
$$
(n)' = 1,\quad (e^n)' = e^n
$$

因为：
$$
1 \leq e^n
$$

所以命题成立 ✅

---

## 🔁 3. O-notation: Part II

### (1)

如果：
$$
f \in O(h_1), \quad g \in O(h_2)
$$

则：
$$
fg \in O(h_1 h_2)
$$

**Proof:**

$$
f(n) \leq c_1 h_1(n), \quad g(n) \leq c_2 h_2(n)
$$

$$
f(n)g(n) \leq c_1 c_2 h_1(n) h_2(n)
$$

---

### (2)

$$
2^n \in O(n!)
$$

比较：

* $2^{n-1} = 2 \cdot 2 \cdots 2$
* $n! = 2 \cdot 3 \cdots n$

每项 ≥ 2 ⇒ 成立 ✅

---

### (3)

$$
2\sqrt{\log n} \in O(n)
$$

利用：
$$
\sqrt{x} \leq x \quad (x \geq 1)
$$

取：

* $c = 1$
* $n_0 = 2$

---

## ⛰️ 4. Fast Peak Finding（反例）

### Counterexample

$$
A[i] = i,\quad 0 \leq i \leq 7
$$

算法会递归到：
$$
A[0..2]
$$

但该区间在原数组中**没有 peak** ❌

---

## 🧠 5. Optional (Advanced)

### 5.1 Racetrack Principle

证明：
$$
\frac{2}{\log n} \leq \frac{1}{\log \log n}
$$

化简为：
$$
(\log n)^2 \leq n
$$

取：

* $n_0 = 16$

成立 ✅

---

### 5.2 Finding Two Peaks

### Question

是否存在比 $O(n)$ 更快的算法？

### Answer

❌ 不存在

**原因：**

* 最坏情况必须检查所有元素
* 无法使用二分剪枝

因此时间复杂度下界为：
$$
\Omega(n)
$$

---

# ✨ 使用说明

1. 新建文件：

```
README.md
```

2. 粘贴本内容

3. 推到 GitHub 即可显示美观公式 🎉

---

💡 如果你想再升级：

* 加目录（Table of Contents）
* 自动编号定理
* 或转成 LaTeX PDF

我可以帮你再优化一版更“论文风”的版本
