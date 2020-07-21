## 31.4 Solving modular linear equations

### 31.4-1

> Find all solutions to the equation $35x \equiv 10 (\text{mod}\~50)$.

$\\{6, 16, 26, 36, 46\\}$.

### 31.4-2

> Prove that the equation $ax \equiv ay \~(\text{mod}\~n)$ implies $x \equiv y \~(\text{mod}\~n)$ whenever $\text{gcd}(a, n) = 1$. Show that the condition $\text{gcd}(a, n) = 1$ is necessary by supplying a counterexample with $\text{gcd}(a, n) > 1$.

$d = \text{gcd}(ax, n) = \text{gcd}(x, n)$

Since $ax \cdot x' + n \cdot y' = d$, then $x \cdot (ax') + n \cdot y' = d$.

$x\_0 = x'(ay / d)$,

$x\_0' = (ax')(y / d) = x'(ay / d) = x\_0$.

### 31.4-3

> Consider the following change to line 3 of the procedure MODULAR-LINEAR-EQUATION-SOLVER: 
> 
> ```
3 x0 = x'(b/d) mod (n/d) 
```

Assume that $x\_0 \ge n / d$, then the largest solution is $x\_0 + (d - 1) \* (n / d) \ge d \* n / d \ge n$, which is impossible, therefore $x\_0 < n / d$.

### 31.4-4 $\star$

> Let $p$ be prime and $f(x) \equiv f\_0 + f\_1 x + \cdots + f\_t x^t \~(\text{mod}\~p)$ be a polynomial of degree $t$, with coefficients $f\_i$ drawn from $\mathbb{Z}\_p$. We say that $a \in \mathbb{Z}\_p$ is a __*zero*__ of $f$ if $f(a) \equiv 0 \~(\text{mod}\~p)$. Prove that if $a$ is a zero of $f$, then $f(x) \equiv (x - a) g(x)\~(\text{mod}\~p)$ for some polynomial $g(x)$ of degree $t - 1$. Prove by induction on $t$ that if $p$ is prime, then a polynomial $f(x)$ of degree $t$ can have at most $t$ distinct zeros modulo $p$.
