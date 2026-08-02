---
title: The Chinese Remainder Theorem
date_created: 2026-07-06
---

# The Chinese Remainder Theorem

## The need — several congruences at once

[Modular Inverses and Linear Congruences](Modular%20Inverses%20and%20Linear%20Congruences/) solves one congruence. Many problems instead fix several remainders at once: find an integer that leaves remainder $2$ on division by $3$, remainder $3$ on division by $5$, and remainder $2$ on division by $7$. This exact problem appears in the Sunzi Suanjing, a Chinese text from around the third century, which is why the result carries that name. The genuine problem is whether a system $x \equiv a_1 \pmod{n_1}, \dots, x \equiv a_k \pmod{n_k}$ has a solution, and how many, when the moduli are pairwise coprime. The Chinese Remainder Theorem answers both: there is a solution, and it is unique modulo the product of the moduli.

## The two-modulus theorem

Concrete first. Solve $x \equiv 2 \pmod 3$ and $x \equiv 3 \pmod 5$. The integers congruent to $2$ modulo $3$ are $2, 5, 8, 11, 14, \dots$; among them the first also congruent to $3$ modulo $5$ is $8$. Every solution differs from $8$ by a multiple of $15$, so the solution set is $x \equiv 8 \pmod{15}$, one class modulo the product $3 \cdot 5$.

{% callout_tip() %}
**Theorem — CRT for two coprime moduli.**

If $\gcd(m, n) = 1$, then for any integers $a, b$ the system $x \equiv a \pmod m$, $x \equiv b \pmod n$ has a solution, and the solution is unique modulo $mn$.
{% end %}

Skeleton. For existence, the load-bearing step is a Bézout identity $um + vn = 1$, which produces two "selector" numbers: $vn$, congruent to $1$ modulo $m$ and $0$ modulo $n$, and $um$, congruent to $0$ modulo $m$ and $1$ modulo $n$. Combining them as $a\,vn + b\,um$ hits $a$ modulo $m$ and $b$ modulo $n$. For uniqueness, two solutions differ by a common multiple of $m$ and $n$, and coprimality upgrades that to a multiple of $mn$.

**Proof.**

> Existence. By coprimality and [Bézout's Identity](../unique-factorization/Be%CC%81zout%27s%20Identity/),
> $$um + vn = 1 \tag{1}$$
> $$vn \equiv 1 \pmod m, \qquad vn \equiv 0 \pmod n \tag{2}$$
> $$um \equiv 0 \pmod m, \qquad um \equiv 1 \pmod n \tag{3}$$
> $$x = a\,vn + b\,um \tag{4}$$
>
> `Depends-on:` line $(1)$ is Bézout for the coprime pair $m, n$.
> `Algebra:` line $(2)$ reads $(1)$ modulo $m$: $um \equiv 0$, so $vn \equiv 1$; and $vn$ is a multiple of $n$, so $vn \equiv 0 \pmod n$. Line $(3)$ is the same reading with $m$ and $n$ swapped.
> `Algebra:` line $(4)$ combines the selectors: modulo $m$, $x \equiv a\cdot 1 + b\cdot 0 = a$ by $(2)$–$(3)$; modulo $n$, $x \equiv a\cdot 0 + b\cdot 1 = b$. So $x$ solves both congruences.
>
> Uniqueness.
> $$x \equiv x' \pmod m \text{ and } x \equiv x' \pmod n \implies m \mid (x - x'),\ n \mid (x - x') \tag{5}$$
> $$\gcd(m,n) = 1 \implies mn \mid (x - x') \implies x \equiv x' \pmod{mn} \tag{6}$$
>
> `Assumption:` line $(5)$ takes two solutions and subtracts, so their difference is a common multiple of $m$ and $n$.
> `Depends-on:` line $(6)$ uses the corollary from [GCD Properties and Coprimality](../unique-factorization/GCD%20Properties%20and%20Coprimality/) that if $m \mid c$, $n \mid c$, and $\gcd(m,n) = 1$, then $mn \mid c$; so the two solutions agree modulo $mn$. $\blacksquare$

## The general theorem

Concrete first, the Sunzi problem. Solve $x \equiv 2 \pmod 3$, $x \equiv 3 \pmod 5$, $x \equiv 2 \pmod 7$. The product is $N = 105$. The partial products are $N_1 = 35$, $N_2 = 21$, $N_3 = 15$. Each $N_i$ is inverted modulo its own $n_i$: $35 \equiv 2 \pmod 3$ with inverse $2$; $21 \equiv 1 \pmod 5$ with inverse $1$; $15 \equiv 1 \pmod 7$ with inverse $1$. The solution is $x = 2\cdot 35\cdot 2 + 3\cdot 21\cdot 1 + 2\cdot 15\cdot 1 = 140 + 63 + 30 = 233 \equiv 23 \pmod{105}$.

{% callout_tip() %}
**Theorem — CRT for k pairwise coprime moduli.**

Let $n_1, \dots, n_k$ be pairwise coprime, $N = n_1 \cdots n_k$, and $N_i = N/n_i$. For any $a_1, \dots, a_k$, the system $x \equiv a_i \pmod{n_i}$ has a unique solution modulo $N$, given by
$$x = \sum_{i=1}^{k} a_i\, N_i\, y_i, \qquad y_i = N_i^{-1} \bmod n_i. \tag{7}$$
{% end %}

`Type:` $N_i$ is the product of all moduli except $n_i$, and $y_i$ is the inverse of $N_i$ modulo $n_i$; this inverse exists because $\gcd(N_i, n_i) = 1$, since $n_i$ is coprime to every other modulus.
`Depends-on:` the inverse $y_i$ is computed by [Modular Inverses and Linear Congruences](Modular%20Inverses%20and%20Linear%20Congruences/). Reading $(7)$ modulo a fixed $n_j$: every term with $i \neq j$ contains the factor $n_j$ inside $N_i$, so it is $\equiv 0$; the term $i = j$ is $a_j N_j y_j \equiv a_j \cdot 1 = a_j$, because $N_j y_j \equiv 1 \pmod{n_j}$. So $x \equiv a_j \pmod{n_j}$ for every $j$. Uniqueness modulo $N$ follows by the same difference argument as the two-modulus case, applied across all $n_i$.

### Section summary

The construction $(7)$ turns any system of congruences with pairwise coprime moduli into a single explicit solution modulo the product. What is now true is that independent remainder constraints modulo coprime numbers never conflict and always combine to one class modulo $N$. What this hands forward is a structural reading: the map sending a residue modulo $N$ to its tuple of residues modulo the $n_i$ is a bijection, and it respects addition and multiplication, which is the ring-isomorphism statement next.

## The ring isomorphism

Concrete first. Modulo $15$, send each class to its pair of residues modulo $3$ and modulo $5$: $[8]_{15} \mapsto ([2]_3, [3]_5)$, $[7]_{15} \mapsto ([1]_3, [2]_5)$. There are $15$ classes on the left and $3 \cdot 5 = 15$ pairs on the right, and CRT says the correspondence is one to one. Addition and multiplication can be done either before or after the map with the same result: $[8]_{15} + [7]_{15} = [0]_{15} \mapsto ([0]_3, [0]_5)$, and the pairs add componentwise to $([2]+[1], [3]+[2]) = ([0]_3, [0]_5)$.

{% callout_tip() %}
**Theorem — CRT as a ring isomorphism.**

If $\gcd(m,n) = 1$, the map $[x]_{mn} \mapsto ([x]_m, [x]_n)$ is a ring isomorphism
$$\mathbb{Z}/mn\mathbb{Z} \;\cong\; \mathbb{Z}/m\mathbb{Z} \times \mathbb{Z}/n\mathbb{Z}. \tag{8}$$
{% end %}

**Proof.**

> `Depends-on:` the map is well-defined and respects $+$ and $\times$ because reducing modulo $mn$ then modulo $m$ agrees with reducing modulo $m$ directly. It is injective because $[x]_m = [x']_m$ and $[x]_n = [x']_n$ force $mn \mid (x - x')$, the uniqueness step $(6)$. Both sides have exactly $mn$ elements, so an injective map between them is a bijection; existence in CRT is exactly the surjectivity. So the map is a ring isomorphism.

`POV:` this recasts CRT from "solve a system" to "$\mathbb{Z}/mn\mathbb{Z}$ factors as a product of smaller rings," which is the form used to break a computation modulo a large composite into independent computations modulo its coprime factors.
`Cross-domain:` restricting $(8)$ to invertible elements gives $(\mathbb{Z}/mn\mathbb{Z})^\times \cong (\mathbb{Z}/m\mathbb{Z})^\times \times (\mathbb{Z}/n\mathbb{Z})^\times$; counting both sides yields the multiplicativity of the totient, $\varphi(mn) = \varphi(m)\varphi(n)$ for coprime $m, n$, proved in [Fermat's Little Theorem, Euler's Theorem, and the Totient](Fermat%27s%20Little%20Theorem%2C%20Euler%27s%20Theorem%2C%20and%20the%20Totient/) where $\varphi$ is defined.

## Computation

Mechanism by hand. Form $N = \prod n_i$, then for each $i$ compute $N_i = N/n_i$ and its inverse $y_i$ modulo $n_i$ by the extended Euclidean algorithm, then sum $\sum a_i N_i y_i$ and reduce modulo $N$. The work is $k$ inversions, each cheap.

```python
def ext_gcd(a: int, b: int) -> tuple[int, int, int]:
    """Return (g, x, y) with g = gcd(a, b) = a*x + b*y."""
    old_r, r = a, b
    old_x, x = 1, 0
    old_y, y = 0, 1
    while r != 0:
        q = old_r // r
        old_r, r = r, old_r - q * r
        old_x, x = x, old_x - q * x
        old_y, y = y, old_y - q * y
    return old_r, old_x, old_y


def crt(residues: list[int], moduli: list[int]) -> int:
    """Return the unique solution mod prod(moduli) of x = residues[i] (mod moduli[i]).

    Assumes the moduli are pairwise coprime. Uses the explicit CRT formula
    x = sum a_i * N_i * y_i, where N_i = N / n_i and y_i = N_i^{-1} mod n_i.
    """
    N = 1
    for n in moduli:
        N *= n
    total = 0
    for a_i, n_i in zip(residues, moduli):
        N_i = N // n_i
        _, inv, _ = ext_gcd(N_i % n_i, n_i)   # y_i = N_i^{-1} mod n_i
        total += a_i * N_i * (inv % n_i)
    return total % N
```

`Conditioning:` each inverse is computed modulo a small $n_i$, so the algorithm cost is dominated by the multiplications forming $N$ and the sum, all in exact integers; there is no error growth.
`Overflow:` the intermediate sum $\sum a_i N_i y_i$ can exceed $N$ before the final reduction, so in a fixed-width type one reduces modulo $N$ during accumulation; Python's unbounded integers make this a speed concern rather than a correctness one.

## Examples

**Easy, two moduli.** Solve $x \equiv 2 \pmod 3$, $x \equiv 3 \pmod 5$. By hand, testing $2, 5, 8$ gives $8 \equiv 3 \pmod 5$, so $x \equiv 8 \pmod{15}$.
```python
crt([2, 3], [3, 5])   # -> 8
```

**Moderate, the Sunzi system.** Solve $x \equiv 2 \pmod 3$, $x \equiv 3 \pmod 5$, $x \equiv 2 \pmod 7$. By hand, the formula gives $x = 140 + 63 + 30 = 233 \equiv 23 \pmod{105}$.
```python
crt([2, 3, 2], [3, 5, 7])   # -> 23
```

**Hard, larger coprime moduli.** Solve $x \equiv 1 \pmod 4$, $x \equiv 2 \pmod 9$, $x \equiv 3 \pmod{25}$. By hand, $N = 900$, $N_1 = 225$, $N_2 = 100$, $N_3 = 36$, with inverses $225^{-1} \equiv 1 \pmod 4$, $100^{-1} \equiv 1 \pmod 9$, $36^{-1} \equiv 11 \pmod{25}$; the sum is $1\cdot 225\cdot 1 + 2\cdot 100\cdot 1 + 3\cdot 36\cdot 11 = 225 + 200 + 1188 = 1613 \equiv 713 \pmod{900}$.
```python
crt([1, 2, 3], [4, 9, 25])   # -> 713
```

**Edge case, one modulus is 1.** A congruence modulo $1$ constrains nothing, since every integer is $\equiv 0 \pmod 1$. Solving $x \equiv 0 \pmod 1$, $x \equiv 4 \pmod 5$ gives simply $x \equiv 4 \pmod 5$.
```python
crt([0, 4], [1, 5])   # -> 4
```

**Counterexample A, non-coprime and inconsistent.** The system $x \equiv 1 \pmod 2$, $x \equiv 0 \pmod 4$ has no solution: the second says $x$ is a multiple of $4$, hence even, while the first says $x$ is odd. Failure mode: the moduli share the factor $2$, and $\gcd(2,4) = 2$ does not divide the residue difference $0 - 1$, so no common solution exists.
```python
# crt assumes coprime moduli; here gcd(2,4)=2, so its output is not a valid solution.
# A general solver checks gcd(m,n) | (a-b); that fails, so the true answer is "no solution".
```

**Counterexample B, non-coprime but consistent.** The system $x \equiv 2 \pmod 4$, $x \equiv 4 \pmod 6$ is consistent, because $\gcd(4,6) = 2$ divides $4 - 2 = 2$, but the solution is unique modulo $\mathrm{lcm}(4,6) = 12$, not modulo the product $24$. The solutions are $x \equiv 10 \pmod{12}$. Failure mode: without coprimality the uniqueness modulus is the lcm, so the product formula overcounts the solution set, a different failure from the inconsistency in A.
```python
[x for x in range(24) if x % 4 == 2 and x % 6 == 4]   # -> [10, 22], i.e. 10 mod 12
```

**Disguised use, splitting a modulus.** Computing a residue modulo a composite can be split into independent computations modulo its coprime factors, then recombined by CRT. To find $17^{2} \bmod 15$, compute modulo $3$ and modulo $5$: $17 \equiv 2 \pmod 3$ so $17^2 \equiv 1$; $17 \equiv 2 \pmod 5$ so $17^2 \equiv 4$; CRT on $([1]_3, [4]_5)$ gives $[4]_{15}$, matching $289 = 19\cdot 15 + 4$.
```python
crt([17**2 % 3, 17**2 % 5], [3, 5]), 17**2 % 15   # -> (4, 4)
```

**Application, RSA decryption speedup.** In RSA the modulus is $N = pq$ with $p, q$ distinct primes. Decryption computes $c^d \bmod N$; doing it directly is costly, so implementations compute $c^d \bmod p$ and $c^d \bmod q$ separately and recombine by CRT, which is several times faster because the exponentiations run modulo the smaller primes. Domain: public-key cryptography. By hand, with $p=3$, $q=5$, $N=15$, a value $[13]_{15}$ recombines from $([1]_3, [3]_5)$.
```python
crt([13 % 3, 13 % 5], [3, 5])   # -> 13
```

## Summary

`For:` the topic solves systems of congruences with pairwise coprime moduli, answering the opening need that independent remainder constraints combine to a single class modulo the product.

`Assumes:` [Bézout's Identity](../unique-factorization/Be%CC%81zout%27s%20Identity/) for the selectors, spent at line $(1)$; the coprime-multiple corollary from [GCD Properties and Coprimality](../unique-factorization/GCD%20Properties%20and%20Coprimality/) for uniqueness, spent at line $(6)$; and [Modular Inverses and Linear Congruences](Modular%20Inverses%20and%20Linear%20Congruences/) for the inverses $y_i$ in the general formula $(7)$.

`Produces:` the two-modulus theorem, the explicit $k$-modulus formula $(7)$, and the ring isomorphism $\mathbb{Z}/mn\mathbb{Z} \cong \mathbb{Z}/m\mathbb{Z} \times \mathbb{Z}/n\mathbb{Z}$, whose restriction to units gives totient multiplicativity.

`Pattern-match:` recognize CRT whenever remainders modulo coprime numbers are prescribed independently, whenever a computation modulo a composite is split over its coprime factors for speed (RSA-CRT), and whenever a ring modulo a composite is decomposed into a product of smaller rings; and check coprimality first, because without it the system may be inconsistent or unique only modulo the lcm.
