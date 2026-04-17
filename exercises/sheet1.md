# [cite_start]Exercise Sheet 1: Answers [cite: 89]
[cite_start]**Course:** COMS10018 Algorithms [cite: 89]

> [cite_start]**Reminder:** $\log n$ denotes the binary logarithm, i.e., $\log n = \log_2 n$[cite: 90].

---

## [cite_start]Example Question: Big-O Notation [cite: 91]

[cite_start]**Question:** Give a formal proof of the following statement using the definition of Big-O from the lecture (i.e., identify positive constants $c$, $n_0$ for which the definition holds): $5\sqrt{n} \in O(n)$[cite: 92, 93].

**Solution:**
* [cite_start]We need to show that there are positive constants $c$, $n_0$ such that $5\sqrt{n} \le c \cdot n$ holds, for every $n \ge n_0$[cite: 94].
* [cite_start]This is equivalent to showing that $(5/c)^2 \le n$ holds[cite: 95].
* [cite_start]We choose $c=5$ which implies $1 \le n$[cite: 96]. 
* [cite_start]We can thus select $n_0=1$, since then $1 \le n$ holds for every $n \ge n_0$[cite: 96].
* [cite_start]This proves that $5\sqrt{n} \in O(n)$[cite: 97].

> [cite_start]**Remark:** Observe that there are many other combinations of values for $c$ and $n_0$ that satisfy the inequality we need to prove[cite: 98]. [cite_start]For example, if we pick $c=1$ then we obtain $25 \le n$ (which follows from $(5/c)^2 \le n$)[cite: 99]. [cite_start]In this case, we would have to choose a value for $n_0$ that is greater or equal to 25, in particular, $n_0=25$ would do[cite: 100].

---

## [cite_start]1 O-notation: Part I [cite: 101]

[cite_start]Give formal proofs of the following statements using the definition of Big-O from the lecture (i.e., identify positive constants $c$, $n_0$ for which the definition holds)[cite: 103]:

### [cite_start]1. $n^2+10n+8 \in O(\frac{1}{2}n^2)$ [cite: 104]
**Solution:**
* [cite_start]We need to show that there are positive constants $c$, $n_0$ such that $n^2+10n+8 \le c \cdot \frac{1}{2}n^2$ for every $n \ge n_0$[cite: 105].
* [cite_start]To make our life easier, we use the following estimate: $n^2+10n+8 < n^2+10n^2+8n^2 = 19n^2$ which holds for every $n \ge 1$[cite: 105, 106, 107].
* [cite_start]If we can prove that there are constants $c$, $n_0$ such that $19n^2 \le c \cdot \frac{1}{2}n^2$ holds for every $n \ge n_0$, then these constants also work for showing that $n^2+10n+8 \le c \cdot \frac{1}{2}n^2$ for every $n \ge n_0$[cite: 107].
* [cite_start]This, however, is easy: We can pick $c=38$ and $n_0=1$, which completes the proof[cite: 108].

### [cite_start]2. $n^3+n^2+n \in O(n^3)$ [cite: 109]
**Solution:**
* [cite_start]We need to show that there are constants $c$, $n_0$ such that $n^3+n^2+n \le c \cdot n^3$ holds for every $n \ge n_0$[cite: 112].
* [cite_start]Using the idea from the previous exercise, we use the inequality $n^3+n^2+n \le 3n^3$ which holds for every $n \ge 1$, and prove instead that there are constants $c, n_0$ such that $3n^3 \le c n^3$ holds for every $n \ge n_0$[cite: 112].
* [cite_start]Again, this is easy to do: We pick $c=3$ and $n_0=1$[cite: 112].

### [cite_start]3. $10 \in O(1)$ [cite: 113]
**Solution:**
* [cite_start]We need to show that there are positive constants $c$, $n_0$ such that $10 \le c \cdot 1$, for every $n \ge n_0$[cite: 114].
* [cite_start]Observe that this expression does not depend on $n$ at all[cite: 115].
* [cite_start]Therefore any positive value for $n_0$ would work, e.g., $n_0=1$ (or $n_0=23$ or any other value)[cite: 116].
* [cite_start]We choose $c=10$ which implies that $10 \le c \cdot 1$ is satisfied[cite: 117]. [cite_start]This proves that $10 \in O(1)$[cite: 117].

### [cite_start]4. $\sum_{i=1}^{n}i \in O(4n^2)$ [cite: 118]
**Solution:**
* [cite_start]First, observe that $\sum_{i=1}^{n}i = n(n+1)/2 = \frac{n^2}{2} + \frac{n}{2}$[cite: 120].
* [cite_start]We need to find positive constants $c$, $n_0$ such that $\frac{n^2}{2} + \frac{n}{2} \le c \cdot 4n^2$ for every $n \ge n_0$[cite: 120].
* [cite_start]We pick $n_0=1$[cite: 121].
* [cite_start]Since $n \le n^2$, for every $n \ge n_0=1$, we will satisfy the inequality $\frac{n^2}{2} + \frac{n^2}{2} \le c \cdot 4n^2$ which is equivalent to $1 \le 4c$[cite: 121].
* [cite_start]We can hence pick $c=1$ and we are done[cite: 121].

---

## [cite_start]2 Racetrack Principle [cite: 122]

[cite_start]**Question:** Use the racetrack principle to prove the following statement: $n \le e^n$ holds for every $n \ge 1$[cite: 123, 124].

**Solution:**
* [cite_start]First, we verify that $n \le e^n$ holds for $n=n_0=1$[cite: 125]. [cite_start]This is true, since $1 \le e$ holds[cite: 125].
* [cite_start]Next, we verify that $(n)' \le (e^n)'$ holds for every $n \ge n_0$[cite: 126].
* [cite_start]We have $(n)'=1$ and $(e^n)'=e^n$[cite: 127].
* [cite_start]We thus need to show that $1 \le e^n$ holds for every $n \ge 1$[cite: 127].
* [cite_start]Taking the natural logarithm on both sides, we obtain $0 \le n$, which is true for every $n \ge n_0=1$[cite: 127].
* [cite_start]Hence, $n \le e^n$ holds for every $n \ge 1$[cite: 127].

---

## [cite_start]3 O-notation: Part II [cite: 130]

[cite_start]Give formal proofs of the following statements using the definition of Big-O from the lecture[cite: 131].

### [cite_start]1. $f \in O(h_1)$, $g \in O(h_2)$ then $f \cdot g \in O(h_1 \cdot h_2)$ [cite: 132]
**Solution:**
* [cite_start]Similar as in the previous exercise, we know that there are constants $c_1, c_2, n_1, n_2$ such that $f(n) \le c_1 \cdot h_1(n)$, for every $n \ge n_1$, and $g(n) \le c_2 \cdot h_2(n)$, for every $n \ge n_2$[cite: 133].
* [cite_start]Then: $f(n) \cdot g(n) \le c_1 \cdot h_1(n) \cdot c_2 \cdot h_2(n) = c_1 c_2 \cdot h_1(n)h_2(n)$ for every $n \ge \max\{n_1, n_2\}$[cite: 134, 135].
* [cite_start]We thus select $C = c_1 \cdot c_2$ and $N = \max\{n_1, n_2\}$ and obtain $f(n)g(n) \le C(h_1(n)h_2(n))$, for every $n \ge N$[cite: 135].

### [cite_start]2. $2^n \in O(n!)$ [cite: 136]
**Solution:**
* [cite_start]To prove this statement, we will show that $2^n \le C \cdot n!$ holds for $C=2$ and every $n \ge 2$[cite: 138].
* [cite_start]To this end, observe that $2^n \le 2n!$ is equivalent to $2^{n-1} \le n!$[cite: 138].
* Observe that $2^{n-1} = \underbrace{2 \cdot 2 \cdot \dots \cdot 2}_{(n-1) \text{ times}}$ and $n! [cite_start]= n \cdot (n-1) \cdot \dots \cdot 2 \cdot 1$ ($(n-1)$ factors, each larger equal to 2)[cite: 139, 141, 142, 143].
* [cite_start]Trading off the factors of the two expressions, we see that $2^{n-1} \le n!$ which proves the result[cite: 144].

### [cite_start]3. $2^{\sqrt{\log n}} \in O(n)$ [cite: 145]
**Solution:**
* [cite_start]We need to show that there are constants $c$, $n_0$ such that $2^{\sqrt{\log n}} \le c \cdot n$ holds for every $n \ge n_0$[cite: 146]. 
* [cite_start]Observe that the previous inequality is equivalent to $2^{\sqrt{\log n}} \le 2^{\log(n) + \log(c)}$, which holds if $\sqrt{\log n} \le \log(n) + \log(c)$[cite: 146].
* [cite_start]Observe that $\sqrt{x} \le x$ for every $x \ge 1$[cite: 147].
* [cite_start]Hence, $\sqrt{\log n} \le \log(n)$ holds for every $\log(n) \ge 1$ or every $n \ge 2$[cite: 147].
* [cite_start]We can thus pick $n_0=2$ and $c=1$ (observe that $\log(x) < 0$ for $x < 1$ we therefore couldn't choose $c < 1$)[cite: 147].

---

## [cite_start]4 Fast Peak Finding [cite: 148]

[cite_start]**Question:** Consider the following variant of `FAST-PEAK-FINDING` where the `>` sign in the condition in instruction 4 is replaced by a `<` sign[cite: 149]:
1. [cite_start]if $A$ is of length 1 then return 0 [cite: 150]
2. [cite_start]if $A$ is of length 2 then compare $A[0]$ and $A[1]$ and return position of larger element [cite: 151]
3. [cite_start]if $A[\lfloor n/2 \rfloor]$ is a peak then return $\lfloor n/2 \rfloor$ [cite: 152]
4. [cite_start]Otherwise, if $A[\lfloor n/2 \rfloor - 1] < A[\lfloor n/2 \rfloor]$ then return `FAST-PEAK-FINDING` ($A[0, \lfloor n/2 \rfloor - 1]$) [cite: 153, 154]
5. [cite_start]else return $\lfloor n/2 \rfloor + 1 +$ `FAST-PEAK-FINDING` ($A[\lfloor n/2 \rfloor + 1, n-1]$) [cite: 154, 155]

[cite_start]Give an input array of length 8 on which this algorithm fails[cite: 156].

**Solution:**
* [cite_start]Consider the instance $A[i]=i$ for every $0 \le i \le 7$[cite: 157].
* [cite_start]Then the algorithm recurses on the subarray $A[0...2]$ in line 4[cite: 157].
* [cite_start]Observe however that none of the elements in $A[0...2]$ constitute a peak in array $A$[cite: 157].

---

## [cite_start]5 Optional and Difficult [cite: 158]

### [cite_start]5.1 Advanced Racetrack Principle [cite: 159]
[cite_start]**Question:** Use the racetrack principle and determine a value $n_0$ such that $\frac{2}{\log n} \le \frac{1}{\log \log n}$ holds for every $n \ge n_0$[cite: 160, 161].

> [cite_start]**Hint:** Transform the inequality and eliminate the log-function from one side of the inequality before applying the racetrack principle[cite: 163]. If needed, apply the racetrack principle twice! [cite_start]Recall that $(\log n)' = \frac{1}{n \ln(2)}$[cite: 164]. [cite_start]The inequality $\ln(2) \ge 1/2$ may also be useful[cite: 164].

**Solution:**
[cite_start]We use the provided "Hint" and transform the given inequality as follows[cite: 165]:

$$
\begin{aligned}
\frac{2}{\log n} &\le \frac{1}{\log \log n} \\
2 \log \log n &\le \log n \\
2^{2 \log \log n} &\le 2^{\log n} \\
(\log n)^2 &\le n
\end{aligned}
$$
[cite_start][cite: 166, 167].

* [cite_start]We now pick $n_0=16$[cite: 168]. [cite_start]Then, $(\log 16)^2 \le 16$ holds[cite: 168].
* [cite_start]Next, observe that $((\log n)^2)' = \frac{2 \ln(n)}{(\ln(2))^2 n}$ and $(n)' = 1$[cite: 168].
* [cite_start]Using the racetrack principle, it is enough to show that $\frac{2 \ln(n)}{(\ln(2))^2 n} \le 1$, for every $n \ge n_0=16$[cite: 168].
* [cite_start]This is equivalent to showing that $2 \ln(n) \le \ln(2)^2 n$ (for every $n \ge 16$)[cite: 168].
* [cite_start]We now apply the racetrack principle again: To this end, we first verify that $2 \ln(n) \le \ln(2)^2 n$ holds for $n=n_0=16$[cite: 168]. [cite_start]We indeed have $2 \ln(16) = 2 \ln(2^4) = 8 \ln(2) \le \ln(2)^2 \cdot 16$ (which holds since $\ln(2) \ge 1/2$)[cite: 168].
* [cite_start]Next, observe that $(2 \ln(n))' = \frac{2}{n}$ and $(\ln(2)^2 n)' = \ln(2)^2$[cite: 168].
* [cite_start]It thus remains to argue that $\frac{2}{n} \le \ln(2)^2$ for every $n \ge 16$[cite: 168].
* [cite_start]The previous inequality is equivalent to $\frac{2}{\ln(2)^2} \le \frac{2}{(1/2)^2} \le 8 \le n$, which holds for every $n \ge 16$[cite: 168].
* [cite_start]Hence, $\frac{2}{\log n} \le \frac{1}{\log \log n}$ holds for every $n \ge 16$[cite: 169].

### [cite_start]5.2 Finding Two Peaks [cite: 170]
**Question:**
[cite_start]We are given an integer array $A$ of length $n$ that has exactly two peaks[cite: 171]. [cite_start]The goal is to find both peaks[cite: 172]. [cite_start]We could do this as follows: Simply go through the array with a loop and check every array element[cite: 172]. [cite_start]This strategy has a runtime of $O(n)$ (requires $c \cdot n$ array accesses, for some constant $c$)[cite: 173]. 

Is there a faster algorithm for this problem (e.g. similar to `FAST-PEAK-FINDING`)? [cite_start]If yes, give such an algorithm[cite: 174]. [cite_start]If no, justify why there is no such algorithm[cite: 175].