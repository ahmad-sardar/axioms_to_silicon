---
title: Fermat's Little Theorem, Euler's Theorem, and the Totient
date_created: 2026-07-06
---

# Fermat's Little Theorem, Euler's Theorem, and the Totient

## The need — collapsing large exponents

Computing $a^k \bmod n$ for a huge exponent $k$ is a basic operation, and [Congruence and Modular Arithmetic](Congruence%20and%20Modular%20Arithmetic/) left a gap about it: the base of a power may be reduced modulo $n$, but the exponent may not, so there is no rule yet for shrinking $k$ itself. The genuine problem is to find the structure that collapses the exponent. The answer is that for a base coprime to $n$, the powers cycle, and the cycle length divides a fixed number $\varphi(n)$, so exponents reduce modulo $\varphi(n)$. This is Euler's theorem; Fermat's little theorem is its prime case, and both rest on counting the units of $\mathbb{Z}/n\mathbb{Z}$.

## The Euler totient

Concrete first. Modulo $9$, the classes coprime to $9$ are $1, 2, 4, 5, 7, 8$, which is six of them; the classes sharing the factor $3$, namely $3, 6, 9$, are excluded. So the count is $6$. Modulo the prime $5$, all of $1, 2, 3, 4$ are coprime to $5$, so the count is $4$. Modulo $6$, only $1$ and $5$ are coprime, so the count is $2$.

{% callout_note() %}
**Definition — Euler totient.**

$\varphi(n)$ is the number of integers in $\{1, 2, \dots, n\}$ coprime to $n$. Equivalently, $\varphi(n) = |(\mathbb{Z}/n\mathbb{Z})^\times|$, the size of the group of units.
{% end %}

`Type:` $\varphi : \mathbb{Z}_{>0} \to \mathbb{Z}_{>0}$; the two descriptions agree because, by the inverse criterion in [Modular Inverses and Linear Congruences](Modular%20Inverses%20and%20Linear%20Congruences/), a class is a unit exactly when its representative is coprime to $n$.
`Convention:` $\varphi(1) = 1$, because the single class modulo $1$ is coprime to $1$ by the convention that $\gcd(k, 1) = 1$; this base case matters in the formulas below.

For a prime $p$, every one of $1, \dots, p-1$ is coprime to $p$, so $\varphi(p) = p - 1$. This one fact is what specializes Euler's theorem to Fermat's.

## Euler's theorem

Concrete first. Modulo $10$, the units are $1, 3, 7, 9$, so $\varphi(10) = 4$. Take $a = 3$: the powers are $3^1 = 3$, $3^2 = 9$, $3^3 = 27 \equiv 7$, $3^4 = 81 \equiv 1 \pmod{10}$. The fourth power returns to $1$, matching $\varphi(10) = 4$.

{% callout_tip() %}
**Theorem — Euler's theorem.**

If $\gcd(a, n) = 1$, then $a^{\varphi(n)} \equiv 1 \pmod n$.
{% end %}

Skeleton. List the units modulo $n$. The load-bearing step is that multiplying every unit by the fixed unit $a$ permutes the list, because $u \mapsto au$ sends units to units and is injective. Taking the product of the whole list before and after the permutation gives the same value, so $a^{\varphi(n)}$ times the product equals the product; cancelling the product, which is itself a unit, leaves $a^{\varphi(n)} \equiv 1$.

**Proof.**

> Let $u_1, \dots, u_{\varphi(n)}$ be the distinct units modulo $n$, and fix $a$ with $\gcd(a,n) = 1$.
> $$u \mapsto a u \text{ maps units to units and is injective} \tag{1}$$
> $$\{a u_1, \dots, a u_{\varphi(n)}\} = \{u_1, \dots, u_{\varphi(n)}\} \text{ as sets modulo } n \tag{2}$$
> $$\prod_{i} (a u_i) \equiv \prod_i u_i \pmod n \tag{3}$$
> $$a^{\varphi(n)} \prod_i u_i \equiv \prod_i u_i \pmod n \tag{4}$$
> $$a^{\varphi(n)} \equiv 1 \pmod n \tag{5}$$
>
> `Depends-on:` line $(1)$: a product of units is a unit, so $au_i$ is a unit; and $au_i \equiv au_j$ gives $u_i \equiv u_j$ after multiplying by $a^{-1}$, which exists because $a$ is a unit (inverse criterion, [Modular Inverses and Linear Congruences](Modular%20Inverses%20and%20Linear%20Congruences/)). So the map is an injection of the unit set into itself.
> `Theorem:` line $(2)$: an injective map from a finite set to itself is a bijection, so the multiplied list is the original list rearranged.
> `Algebra:` line $(3)$ takes the product over both equal sets.
> `Algebra:` line $(4)$ factors $\varphi(n)$ copies of $a$ out of the left product.
> `Algebra:` line $(5)$ cancels $\prod_i u_i$, legal because that product is a unit and therefore invertible modulo $n$. $\blacksquare$

## Fermat's little theorem

Concrete first. Modulo the prime $7$, take $a = 2$: $2^6 = 64 = 9 \cdot 7 + 1 \equiv 1 \pmod 7$, and $6 = 7 - 1$.

{% callout_tip() %}
**Theorem — Fermat's little theorem.**

For a prime $p$ and any integer $a$ with $p \nmid a$, $a^{p-1} \equiv 1 \pmod p$. For every integer $a$, $a^p \equiv a \pmod p$.
{% end %}

**Proof.**

> `Depends-on:` the first statement is Euler's theorem at $n = p$, where $\varphi(p) = p - 1$ and $p \nmid a$ gives $\gcd(a, p) = 1$.
> `Algebra:` the second statement multiplies the first by $a$ when $p \nmid a$, giving $a^p \equiv a$; when $p \mid a$, both sides are $\equiv 0 \pmod p$, so $a^p \equiv a$ holds for every $a$.

### Section summary

For a base coprime to $n$, raising to the power $\varphi(n)$ returns to $1$, so the powers of that base cycle with a length dividing $\varphi(n)$. What is now true is that the exponent of a coprime base is only meaningful modulo $\varphi(n)$. What this hands forward is a way to evaluate $\varphi(n)$ from the factorization of $n$, and the exponent-reduction rule that both theorems make possible.

## The totient formula

Concrete first. $\varphi(12)$: with $12 = 4 \cdot 3$ and $\gcd(4,3) = 1$, split as $\varphi(4)\varphi(3) = 2 \cdot 2 = 4$; directly, the units modulo $12$ are $1, 5, 7, 11$, four of them. Also $\varphi(12) = 12(1 - \tfrac12)(1 - \tfrac13) = 12 \cdot \tfrac12 \cdot \tfrac23 = 4$.

{% callout_tip() %}
**Theorem — Multiplicativity and the prime-power value.**

For coprime $m, n$, $\varphi(mn) = \varphi(m)\varphi(n)$. For a prime power, $\varphi(p^k) = p^k - p^{k-1}$. Combining over the canonical form, $\varphi(n) = n \prod_{p \mid n}\left(1 - \tfrac{1}{p}\right)$.
{% end %}

**Proof.**

> `Depends-on:` multiplicativity is the count of both sides of the units isomorphism from [The Chinese Remainder Theorem](The%20Chinese%20Remainder%20Theorem/), $(\mathbb{Z}/mn\mathbb{Z})^\times \cong (\mathbb{Z}/m\mathbb{Z})^\times \times (\mathbb{Z}/n\mathbb{Z})^\times$; a bijection between finite sets forces equal sizes, so $\varphi(mn) = \varphi(m)\varphi(n)$.
> `Theorem:` for $\varphi(p^k)$, the integers in $\{1, \dots, p^k\}$ not coprime to $p^k$ are exactly the multiples of $p$, of which there are $p^{k-1}$; subtracting gives $\varphi(p^k) = p^k - p^{k-1} = p^k(1 - \tfrac1p)$.
> `Algebra:` writing $n = \prod p_i^{a_i}$ (canonical form, from [Canonical Form and Divisor Structure](../unique-factorization/Canonical%20Form%20and%20Divisor%20Structure/)) and applying multiplicativity across the coprime prime powers gives $\varphi(n) = \prod_i p_i^{a_i}(1 - \tfrac1{p_i}) = n \prod_{p \mid n}(1 - \tfrac1p)$.

## Exponent reduction

Concrete first. Compute $7^{222} \bmod 10$. Since $\gcd(7,10) = 1$ and $\varphi(10) = 4$, the exponent reduces modulo $4$: $222 = 4 \cdot 55 + 2$, so $7^{222} \equiv 7^{2} = 49 \equiv 9 \pmod{10}$.

{% callout_tip() %}
**Theorem — Exponent reduction.**

If $\gcd(a, n) = 1$ and $k \equiv r \pmod{\varphi(n)}$, then $a^k \equiv a^r \pmod n$. $\tag{6}$
{% end %}

**Proof.**

> `Depends-on:` write $k = q\,\varphi(n) + r$; then $a^k = (a^{\varphi(n)})^q a^r \equiv 1^q a^r = a^r \pmod n$ by Euler's theorem. This is precisely the rule missing in [Congruence and Modular Arithmetic](Congruence%20and%20Modular%20Arithmetic/): an exponent on a coprime base reduces modulo $\varphi(n)$, not modulo $n$.

`Note:` the smallest exponent returning $a$ to $1$ is the order of $a$, which divides $\varphi(n)$ but can be strictly smaller; $\varphi(n)$ is a correct reduction modulus for every coprime base, and the order is the sharpest one for a particular base.

A second use, inverses by exponentiation: from $a^{\varphi(n)} \equiv 1$, the inverse is $a^{-1} \equiv a^{\varphi(n)-1} \pmod n$, and for a prime modulus $a^{-1} \equiv a^{p-2} \pmod p$.

## Computation

Mechanism by hand. To evaluate $a^k \bmod n$, reduce the exponent modulo $\varphi(n)$ when $\gcd(a,n) = 1$, then raise by square-and-multiply: repeatedly square the base and multiply in the factors picked out by the binary digits of the exponent, reducing modulo $n$ after each step. To evaluate $\varphi(n)$, factor $n$ and apply the prime-power formula.

```python
from math import isqrt


def totient(n: int) -> int:
    """Return Euler's totient phi(n) via the prime-power product formula.

    Factor n by trial division (the factorize routine from the FTA unit),
    then phi(n) = n * prod(1 - 1/p) over distinct primes p dividing n.
    """
    result = n
    m = n
    p = 2
    while p <= isqrt(m):
        if m % p == 0:
            while m % p == 0:
                m //= p
            result -= result // p        # multiply by (1 - 1/p)
        p += 1
    if m > 1:                            # a remaining prime factor
        result -= result // m
    return result


def mod_pow(a: int, k: int, n: int) -> int:
    """Return a**k mod n by square-and-multiply, O(log k) multiplications.

    Reduces modulo n after every squaring and multiplication, so intermediates
    stay below n*n. Matches Python's built-in pow(a, k, n).
    """
    result = 1
    base = a % n
    while k > 0:
        if k & 1:                        # current binary digit of the exponent
            result = (result * base) % n
        base = (base * base) % n
        k >>= 1
    return result
```

`Conditioning:` square-and-multiply uses about $\log_2 k$ multiplications instead of $k$, so exponents with hundreds of digits are feasible; this is what makes modular exponentiation, and therefore RSA, practical.
`Error-accumulation:` there is none, because every operation is exact integer arithmetic reduced modulo $n$; unlike floating-point powers, repeated modular squaring introduces no drift.

## Examples

**Easy, Fermat.** Modulo $7$, $2^6 = 64 \equiv 1$. By hand, $64 = 9 \cdot 7 + 1$.
```python
mod_pow(2, 6, 7)   # -> 1
```

**Moderate, Euler.** Modulo $10$, $\varphi(10) = 4$ and $3^4 = 81 \equiv 1$. By hand, $81 = 8 \cdot 10 + 1$.
```python
totient(10), mod_pow(3, 4, 10)   # -> (4, 1)
```

**Hard, exponent reduction.** Compute $7^{222} \bmod 10$. By hand, $\varphi(10) = 4$, $222 \equiv 2 \pmod 4$, so $7^{222} \equiv 7^2 = 49 \equiv 9$.
```python
mod_pow(7, 222 % totient(10), 10), mod_pow(7, 222, 10)   # -> (9, 9)
```

**Edge case, prime power totient.** $\varphi(8) = 8 - 4 = 4$, the units modulo $8$ being $1, 3, 5, 7$. By hand, $2^k$ removes the even numbers, leaving four odd residues.
```python
totient(8)   # -> 4
```

**Counterexample A, Fermat needs a prime modulus.** For composite $n = 4$ and $a = 3$, $a^{n-1} = 3^3 = 27 \equiv 3 \pmod 4$, not $1$. Failure mode: $n$ is not prime, so $\varphi(4) = 2 \neq n - 1 = 3$, and raising to $n-1$ is the wrong exponent.
```python
mod_pow(3, 4 - 1, 4)   # -> 3, not 1
```

**Counterexample B, Euler needs coprimality.** For $n = 6$ and $a = 2$ with $\gcd(2,6) = 2$, $a^{\varphi(6)} = 2^2 = 4 \not\equiv 1 \pmod 6$. Failure mode: the base is not coprime to the modulus, so the permutation-of-units argument does not apply; this is a different failure from A, which had a coprime base but a composite modulus and the wrong exponent.
```python
mod_pow(2, totient(6), 6)   # -> 4, not 1
```

**Disguised use, last digit of a power.** The last decimal digit of $m$ is $m \bmod 10$, so the last digit of $2^{2026}$ is a modular exponentiation. By hand, $\gcd(2,10) \neq 1$, so reduce differently: the last digits of powers of $2$ cycle $2, 4, 8, 6$ with length $4$, and $2026 \equiv 2 \pmod 4$, giving last digit $4$.
```python
mod_pow(2, 2026, 10)   # -> 4
```

**Application, RSA correctness.** RSA picks $N = pq$, an encryption exponent $e$, and a decryption exponent $d$ with $ed \equiv 1 \pmod{\varphi(N)}$. Decryption raises the ciphertext to $d$: since $ed = 1 + t\varphi(N)$, the recovered value is $m^{ed} = m \cdot (m^{\varphi(N)})^{t} \equiv m \pmod N$ by Euler's theorem, so decryption inverts encryption. Domain: public-key cryptography. By hand, with $p=3$, $q=11$, $N=33$, $\varphi(N)=20$, $e=3$, $d=7$ (since $3\cdot 7 = 21 \equiv 1 \pmod{20}$), the message $m=5$ encrypts to $5^3 = 125 \equiv 26$ and decrypts as $26^7 \equiv 5 \pmod{33}$.
```python
mod_pow(mod_pow(5, 3, 33), 7, 33)   # -> 5
```

## Summary

`For:` the topic collapses large exponents by showing that a base coprime to $n$ has powers cycling with length dividing $\varphi(n)$, answering the opening need to compute $a^k \bmod n$ and to reduce the exponent, which earlier notes could not.

`Assumes:` the unit group and inverse criterion from [Modular Inverses and Linear Congruences](Modular%20Inverses%20and%20Linear%20Congruences/), spent at the permutation step $(1)$ and the cancellation $(5)$; the CRT units isomorphism from [The Chinese Remainder Theorem](The%20Chinese%20Remainder%20Theorem/), spent at totient multiplicativity; and the canonical form from [Canonical Form and Divisor Structure](../unique-factorization/Canonical%20Form%20and%20Divisor%20Structure/), spent at the product formula.

`Produces:` the totient $\varphi(n) = |(\mathbb{Z}/n\mathbb{Z})^\times|$ with its formula $n\prod(1 - 1/p)$; Euler's theorem $a^{\varphi(n)} \equiv 1$; Fermat's little theorem $a^{p-1} \equiv 1$ and $a^p \equiv a$; the exponent-reduction rule $(6)$; and inverses by exponentiation.

`Pattern-match:` recognize Euler and Fermat wherever a large power is taken modulo $n$ (reduce the exponent modulo $\varphi(n)$ for a coprime base), wherever a modular inverse is written as a power, and wherever RSA correctness or a Fermat primality test appears; and check the two hypotheses first, a coprime base for Euler and a prime modulus for Fermat, since dropping either makes the congruence fail.
