## 31.5 The Chinese remainder theorem

### 31.5-1

> Find all solutions to the equations $x \equiv 4 \~(\text{mod}\~5)$ and $x \equiv 5 \~(\text{mod}\~11)$.

$m\_1 = 11$, $m\_2 = 5$.

$m\_1^{-1} = 1$, $m\_2^{-1} = 9$.

$c\_1 = 11$, $c\_2 = 45$.

$a = (c\_1 \cdot a\_1 + c\_2 \cdot a\_2) \~\text{mod}\~ (n\_1 \cdot n\_2) = (11 \* 4 + 45 \* 5) \~\text{mod}\~ 55 = 49$.

## 31.5-2

> Find all integers $x$ that leave remainders $1, 2, 3$ when divided by $9, 8, 7$ respectively.

$10 + 504i$, $i \in \mathbb{Z}$.

### 31.5-3

> Argue that, under the definitions of Theorem 31.27, if $\text{gcd}(a, n) = 1$, then
> 
>  $(a^{-1} \~\text{mod}\~ n) \leftrightarrow ((a\_1^{-1} \~\text{mod}\~ n\_1), (a\_2^{-1} \~\text{mod}\~ n\_2), \dots, (a\_k^{-1} \~\text{mod}\~ n\_k))$.

$\text{gcd}(a, n) = 1 \rightarrow \text{gcd}(a, n\_i) = 1$.

### 31.5-4

> Under the definitions of Theorem 31.27, prove that for any polynomial $f$, the number of roots of the equation $f(x) \equiv 0 \~(\text{mod}\~n)$ equals the product of the number of roots of each of the equations $f(x) \equiv 0 \~(\text{mod}\~n\_1), f(x) \equiv 0 \~(\text{mod}\~n\_2), \dots, f(x) \equiv 0 \~(\text{mod}\~n\_k)$.

Based on 31.28 ~ 31.30.
