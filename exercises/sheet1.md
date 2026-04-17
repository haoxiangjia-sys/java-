# Exercise Sheet 1: Answers - COMS10018 Algorithms

**Reminder:** $\log n$ denotes the binary logarithm, i.e., $\log n=\log_{2}n$.

## Example Question: Big-O Notation

**Question:** Give a formal proof of the following statement using the definition of Big-O from the lecture (i.e., identify positive constants c, $n_{0}$ for which the definition holds):
$5\sqrt{n}\in O(n)$.

**Solution:**
* We need to show that there are positive constants c, $n_{0}$ such that $5\sqrt{n}\le c\cdot n$ holds, for every $n\ge n_{0}$.
* This is equivalent to showing that $(\frac{5}{c})^{2}\le n$ holds.
* We choose $c=5$ which implies $1\le n.$
* We can thus select $n_{0}=1$, since then $1\le n$ holds for every $n\ge n_{0}$.
* This prove that $5\sqrt{n}\in O(n)$.

**Remark:**
* Observe that there are many other combinations of values for c and $n_{0}$ that satisfy the inequality we need to prove.
* For example, if we pick $c=1$ then we obtain $25\le n$ (which follows from $(\frac{5}{c})^{2}\le n)$.
* In this case, we would have to choose a value for $n_{0}$ that is greater or equal to 25, in particular, $n_{0}=25$ would do.

---

## 1. O-notation: Part I

Give formal proofs of the following statements using the definition of Big-O from the lecture (i.e., identify positive constants c, $n_{0}$ for which the definition holds):

### 1.1 $n^{2}+10n+8\in O(\frac{1}{2}n^{2})$

**Solution:**
* We need to show that there are positive constants c, $n_{0}$ such that $n^{2}+10n+8\le c\cdot\frac{1}{2}n^{2}$ for every $n\ge n_{0}$ To make our life easier, we use the following estimate:

$$n^{2}+10n+8<n^{2}+10n^{2}+8n^{2}=19n^{2}$$

* which holds for every $n\ge1$
* If we can prove that there are constants c, $n_{0}$ such that $19n^{2}\le c\cdot\frac{1}{2}n^{2}$ holds for every $n\ge n_{0}$, then these constants also work for showing that $n^{2}+10n+8\le c\cdot\frac{1}{2}n^{2}$ for every $n\ge n_{0}$.
* This, however, is easy: We can pick $c=38$ and $n_{0}=1$, which completes the proof.

### 1.2 $n^{3}+n^{2}+n=O(n^{3})$

**Solution:**
* We need to show that there are constants c, $n_{0}$ such that $n^{3}+n^{2}+n\le c\cdot n^{3}$ holds for every $n\ge n_{0}$
* Using the idea from the previous exercise, we use the inequality $n^{3}+n^{2}+n\le3n^{3}$ which holds for every $n\ge1$, and prove instead that there are constants $c,n_{0}$ such that $3n^{3}\le cn^{3}$ holds for every $n\ge n_{0}$
* Again, this is easy to do: We pick $c=3$ and $n_{0}=1$

### 1.3 $10\in O(1)$

**Solution:**
* We need to show that there are positive constants c, $n_{0}$ such that $10\le c\cdot1$, for every $n\ge n_{0}$.
* Observe that this expression does not depend on n at all.
* Therefore any positive value for $n_{0}$ would work, e.g.. $n_{0}=1$ (or $n_{0}=23$ or any other value).
* We choose $c=10$ which implies that $10\le c\cdot1$ is satisfied.
* This proves that $10\in O(1)$.

### 1.4 $\sum_{i=1}^{n}i\in O(4n^{2})$

**Solution:**
* First, observe that $\sum_{i=1}^{n}i=n(n+1)/2=\frac{n^{2}}{2}+\frac{n}{2}$.
* We need to find positive constants c, $n_{0}$ such that $\frac{n^{2}}{2}+\frac{n}{2}\le c\cdot4n^{2}$ for every $n\ge n_{0}$.
* We pick $n_{0}=1$.
* Since $n\le n^{2}$, for every $n\ge n_{0}=1$, we will satisfy the inequality $\frac{n^{2}}{2}+\frac{n^{2}}{2}\le c\cdot4n^{2}$ which is equivalent to $1\le4c$
* We can hence pick $c=1$ and we are done.

---

## 2. Racetrack Principle

Use the racetrack principle to prove the following statement:
$n\le e^{n}$ holds for every $n\ge1$.

**Solution:**
* First, we verify that $n\le e^{n}$ holds for $n=n_{0}=1.$
* This is true, since $1\le e$ holds.
* Next, we verify that $(n)^{\prime}\le(e^{n})^{\prime}$ holds for every $n\ge n_{0}$.
* We have $(n)^{\prime}=1$ and $(e^{n})^{\prime}=e^{n}.$
* We thus need to show that $1\le e^{n}$ holds for every $n\ge1$
* Taking the natural logarithm on both sides, we obtain $0\le n.$ which is true for every $n\ge n_{0}=1$
* Hence, $n\le e^{n}$ holds for every $n\ge1$

---

## 3. O-notation: Part II

Give formal proofs of the following statements using the definition of Big-O from the lecture.

### 3.1 $f\in O(h_{1})$, $g\in O(h_{2})$ then $f\cdot g\in O(h_{1}\cdot h_{2})$

**Solution:**
* Similar as in the previous exercise, we know that there are constants $c_{1}$, C2, N1, $n_{2}$ such that $f(n)\le c_{1}\cdot h_{1}(n)$, for every $n\ge n_{1},$ and $g(n)\le c_{2}\cdot h_{2}(n),$ for every $n\ge n_{2}$
* Then: $f(n)\cdot g(n)\le c_{1}\cdot h_{1}(n)\cdot c_{2}\cdot h_{2}(n)=c_{1}c_{2}\cdot h_{1}(n)h_{2}(n)$
* for every $n\ge max\{n_{1},n_{2}\}$.
* We thus select $C=c_{1}\cdot c_{2}$ and $N=max\{n_{1},n_{2}\}$ and obtain $f(n)g(n)\le C(h_{1}(n)h_{2}(n))$, for every $n\ge N$

### 3.2 $2^{n}\in O(n!)$

**Solution:**
* To prove this statement, we will show that $2^{n}\le C\cdot n!$ holds for $C=2$ and every $n\ge2$
* To this end, observe that $2^{n}\le2n!$ is equivalent to $2^{n-1}\le n!$
* Observe that:

$$2^{n-1}=\frac{2\cdot2\cdot\cdot\cdot\cdot2}{(n-1)\text{ times}}$$

* and $n! = (n-1) \text{ factors, each larger equal to 2}$ 
* Trading off the factors of the two expressions, we see that $2^{n-1}\le n!$ which proves the result.

### 3.3 $2^{\sqrt{log~n}}\in O(n)$

**Solution:**
* We need to show that there are constants c, $n_{0}$ such that $2^{\sqrt{log~n}}\le c\cdot r$ holds for every $n\ge n_{0}$
* Observe that the previous inequality is equivalent to $2^{\sqrt{log~n}}\le2^{log(n)+log(c)}$, which holds if $\sqrt{log~n}\le log(n)+log(c)$.
* Observe that $\sqrt{x}\le x$ for every $x\ge1$
* Hence, $\sqrt{log~n}\le log(n)$ holds for every $log(n)\ge1$ or every $n\ge2$
* We can thus pick $n_{0}=2$ and $c=1$ (observe that $log(x)<0$ for $x<1$ we therefore couldn't choose $c<1$.

---

## 4. Fast Peak Finding

Consider the following variant of FAST-PEAK-FINDING where the ">" sign in the condition in instruction 4 is replaced by a "<" sign:
1. if A is of length 1 then return 0
2. if A is of length 2 then compare $A[0]$ and $A[1]$ and return position of larger element
3. if $A[[n/2]]$ is a peak then return $\lfloor n/2\rfloor$
4. Otherwise, if $A[\lfloor n/2\rfloor-1]<A[\lfloor n/2\rfloor]$ then return FAST-PE