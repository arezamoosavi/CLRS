## 31.2 Greatest common divisor

### 31.2-1

> Prove that equations (31.11) and (31.12) imply equation (31.13).

### 31.2-2

 > Compute the values $(d, x, y)$ that the call EXTENDED-EUCLID$(899, 493)$ returns.

$(29, -6, 11)$.

### 31.2-3

> Prove that for all integers $a$, $k$, and $n$,

> $\text{gcd}(a, n) = \text{gcd}(a + kn, n)$.

* $\text{gcd}(a, n) \~|\~ \text{gcd}(a + kn, n)$

Let $d = \text{gcd}(a, n)$, then $d \~|\~ a$ and $d \~|\~ n$. Since $(a + kn) \~\text{mod}\~ d = a \~\text{mod}\~ d + k \cdot (n \~\text{mod}\~ d) = 0$ and $d \~|\~ n$, then $d \~|\~ \text{gcd}(a + kn, n)$, $\text{gcd}(a, n) \~|\~ \text{gcd}(a + kn, n)$.

* $\text{gcd}(a + kn, n) \~|\~ \text{gcd}(a, n)$

Let $d = \text{gcd}(a + kn, n)$, then $d \~|\~ n$ and $d \~|\~ (a + kn)$. Since $(a + kn) \~\text{mod}\~ d = a \~\text{mod}\~ d + k \cdot (n \~\text{mod}\~ d) = a \~\text{mod}\~ d = 0$, then $d \~|\~ a$. Since $d \~|\~ a$ and $d \~|\~ n$, then $d \~|\~ \text{gcd}(a, n)$,  $\text{gcd}(a + kn, n) \~|\~ \text{gcd}(a, n)$.

Since $\text{gcd}(a, n) \~|\~ \text{gcd}(a + kn, n)$ and $\text{gcd}(a + kn, n) \~|\~ \text{gcd}(a, n)$, then $\text{gcd}(a, n) = \text{gcd}(a + kn, n)$.

### 31.2-4

> Rewrite EUCLID in an iterative form that uses only a constant amount of memory (that is, stores only a constant number of integer values).

```python
def euclid(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```

### 31.2-5

> If $a > b \ge 0$, show that the call EUCLID$(a, b)$ makes at most $1 + \log\_\phi b$ recursive calls. Improve this bound to $1 + \log\_\phi(b / \text{gcd}(a, b))$.

$b \ge F\_{k+1} \approx \phi^{k+1} / \sqrt{5}$

$k + 1 < \log\_\phi \sqrt{5} + \log\_\phi b \approx 1.67 + \log\_\phi b$

$k < 0.67 + \log\_\phi b < 1 + \log\_\phi b$.

Since $d \cdot a \~\text{mod}\~ d \cdot b = d \cdot (a \~\text{mod}\~ b)$, $\text{gcd}(d \cdot a, d \cdot b)$ has the same number of recursive calls with $\text{gcd}(a, b)$, therefore we could let $b' = b / \text{gcd}(a, b)$, the inequality $k < 1 + \log\_\phi(b') = 1 + \log\_\phi(b / \text{gcd}(a, b))$. will holds.

## 31.2-6

> What does EXTENDED-EUCLID$(F\_{k+1}, F\_k)$ return? Prove your answer correct.

* If $k$ is odd, then $(1, -F\_{k-2}, F\_{k-1})$.
* If $k$ is even, then $(1, F\_{k-2}, -F\_{k-1})$.

### 31.2-7

> Define the $\text{gcd}$ function for more than two arguments by the recursive equation $\text{gcd}(a\_0, a\_1, \cdots, a\_n) = \text{gcd}(a\_0, \text{gcd}(a\_1, a\_2, \cdots, a\_n))$. Show that the $\text{gcd}$ function returns the same answer independent of the order in which its arguments are specified. Also show how to find integers $x\_0, x\_1, \cdots, x\_n$ such that $\text{gcd}(a\_0, a\_1, \dots, a\_n) = a\_0 x\_0 + a\_1 x\_1 + \cdots + a\_n x\_n$. Show that the number of divisions performed by your algorithm is $O(n + \lg (max \\{a\_0, a\_1, \cdots, a\_n \\}))$.

Suppose $\text{gcd}(a\_0, \text{gcd}(a\_1, a\_2, \cdots, a\_n))  = a\_0 \cdot x + \text{gcd}(a\_1, a\_2, \cdots, a\_n) \cdot y$ and $\text{gcd}(a\_1, \text{gcd}(a\_2, a\_3, \cdots, a\_n))  = a\_1 \cdot x' + \text{gcd}(a\_2, a\_3, \cdots, a\_n) \cdot y'$, then the coefficient of $a\_1$ is $y \cdot x'$.

```python
def extended_euclid(a, b):
    if b == 0:
        return (a, 1, 0)
    d, x, y = extended_euclid(b, a % b)
    return (d, y, x - (a // b) * y)


def extended_eculid_multi(a):
    if len(a) == 1:
        return (a[0], [1])
    g = a[-1]
    xs = [1] * len(a)
    ys = [0] * len(a)
    for i in xrange(len(a) - 2, -1, -1):
        g, xs[i], ys[i + 1] = extended_euclid(a[i], g)
    m = 1
    for i in xrange(1, len(a)):
        m *= ys[i]
        xs[i] *= m
    return (g, xs)
```

### 31.2-8

> Define $\text{lcm}(a\_1, a\_2, \dots, a\_n)$ to be the __*least common multiple*__ of the $n$ integers $a\_1, a\_2, \dots, a\_n$, that is, the smallest nonnegative integer that is a multiple of each $a\_i$. Show how to compute $\text{lcm}(a\_1, a\_2, \dots, a\_n)$ efficiently using the (two-argument) $\text{gcd}$ operation as a subroutine.

```python
def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)


def lcm(a, b):
    return a / gcd(a, b) * b


def lcm_multi(lst):
    l = lst[0]
    for i in xrange(1, len(lst)):
        l = lcm(l, lst[i])
    return l
```

### 31.2-9

> Prove that $n\_1$, $n\_2$, $n\_3$, and $n\_4$ are pairwise relatively prime if and only if
> 
> $\text{gcd}(n\_1n\_2,n\_3n\_4) = \text{gcd}(n\_1n\_3, n\_2n\_4) = 1$
> 
> More generally, show that $n\_1, n\_2, \dots, n\_k$ are pairwise relatively prime if and only if a set of $\lceil \lg k \rceil$ pairs of numbers derived from the $n\_i$ are relatively prime.

Suppose $n\_1 n\_2 x + n\_3 n\_4 y = 1$, then $n\_1 (n\_2 x) + n\_3 (n\_4 y) = 1$, thus $n\_1$ and $n\_3$ are relatively prime, $n\_1$ and $n\_4$, $n\_2$ and $n\_3$, $n\_2$ and $n\_4$ are the all relatively prime. And since $\text{gcd}(n\_1n\_3, n\_2n\_4) = 1$, all the pairs are relatively prime.

General: in the first round, divide the elements into two sets with equal number of elements, calculate the products of the two set separately, if the two products are relatively prime, then the element in one set is pairwise relatively prime with the element in the other set. In the next iterations, for each set, we divide the elements into two subsets, suppose we have subsets $\\{ (s\_1, s\_2), (s\_3, s\_4), \dots \\}$, then we calculate the products of $\\{s\_1, s\_3, \dots\\}$ and $\\{s\_2, s\_4, \dots\\}$, if the two products are relatively prime, then all the pairs of subset are pairwise relatively prime similar to the first round. In each iteration, the number of elements in a subset is half of the original set, thus there are $\lceil \lg k \rceil$ pairs of products.

To choose the subsets efficiently, in the $k$th iteration, we could divide the numbers based on the value of the index's $k$th bit.
