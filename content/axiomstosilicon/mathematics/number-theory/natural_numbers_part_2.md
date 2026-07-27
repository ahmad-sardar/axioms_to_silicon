+++
title = "Operations on Natural Numbers"
slug = "natural_numbers_part_2"
toc = true
+++

# Main Theorems of Addition

Having defined addition, we now prove its fundamental properties. Each theorem requires mathematical induction and builds on previous results.

## Theorem 1: Left Identity

{% callout_tip() %}
**Statement:**

For all $n \in \mathbb{N}$, we have $0 + n = n$.

**In words:**

Zero on the left is the additive identity.

**Why this needs proof:**

The definition only gives us $n + 0 = n$ (zero on the RIGHT). The left version must be proven.
{% end %}

### Proof

> We prove this by induction on $n$.
>
> **Base case ($n = 0$):**
>
> We need to show $0 + 0 = 0$.
>
> By the base case of the addition definition: $n + 0 = n$
>
> Setting $n = 0$: $0 + 0 = 0$ ✓
>
> **Inductive step:**
>
> Inductive Hypothesis (IH): Assume $0 + k = k$ for some $k \in \mathbb{N}$.
>
> Goal: Prove $0 + S(k) = S(k)$.
>
> $$
> \begin{aligned}
> 0 + S(k) &= S(0 + k) && \text{[definition: } n + S(m) = S(n+m)\text{]} \\
> &= S(k) && \text{[by IH: } 0 + k = k\text{]}
> \end{aligned}
> $$
>
> Therefore $0 + S(k) = S(k)$ ✓
>
> **Conclusion:** By the principle of mathematical induction (Axiom 5), we conclude that $0 + n = n$ for all $n \in \mathbb{N}$. ∎

### Key Insights

- The base case uses the definition directly
- The inductive step uses the recursive case of addition
- We apply the IH to simplify $S(0 + k)$ to $S(k)$
- The distinction between IH (our assumption) and Axiom 5 (justification of the method) is crucial

## Theorem 2: Left Successor Property

{% callout_tip() %}
**Statement:**

For all $m, n \in \mathbb{N}$, we have $S(m) + n = S(m + n)$.

**In words:**

Successor on the left behaves like successor on the right.

**Why this matters:**

The definition gives us $n + S(m) = S(n + m)$ (successor on RIGHT). This theorem establishes the symmetric property for successor on LEFT.
{% end %}

### Proof

> We prove this by induction on $n$, keeping $m$ fixed but arbitrary.
>
> **Base case ($n = 0$):**
>
> We need to show $S(m) + 0 = S(m + 0)$.
>
> Left side: $S(m) + 0 = S(m)$ [by definition: $n + 0 = n$]
>
> Right side: $S(m + 0) = S(m)$ [by definition: $m + 0 = m$]
>
> Therefore $S(m) + 0 = S(m) = S(m + 0)$ ✓
>
> **Inductive step:**
>
> IH: Assume $S(m) + k = S(m + k)$ for some $k \in \mathbb{N}$.
>
> Goal: Prove $S(m) + S(k) = S(m + S(k))$.
>
> Transform the left side:
> $$S(m) + S(k) = S(S(m) + k) \quad \text{[definition: } n + S(p) = S(n+p)\text{]}$$
>
> Transform the right side:
> $$
> \begin{aligned}
> S(m + S(k)) &= S(S(m + k)) && \text{[definition: } m + S(k) = S(m+k)\text{]}
> \end{aligned}
> $$
>
> Now we need to show: $S(S(m) + k) = S(S(m + k))$
>
> By IH, we know: $S(m) + k = S(m + k)$
>
> Applying the successor function to both sides: $S(S(m) + k) = S(S(m + k))$ ✓
>
> **Conclusion:** By mathematical induction, $S(m) + n = S(m + n)$ for all $m, n \in \mathbb{N}$. ∎

### Key Insights

- We induct on $n$ while treating $m$ as a fixed parameter
- The proof uses the definition twice (once for each side)
- We apply $S$ to both sides of the IH—this is basic logic about functions, NOT a theorem
- This theorem is essential for proving commutativity

## Theorem 3: Commutativity of Addition

{% callout_tip() %}
**Statement:**

For all $m, n \in \mathbb{N}$, we have $m + n = n + m$.

**In words:**

Order doesn't matter in addition.

**Dependency:**

This proof requires BOTH Theorem 1 and Theorem 2.
{% end %}

### Proof

> We prove this by induction on $n$, keeping $m$ fixed but arbitrary.
>
> Let $P(n)$ be the statement "$m + n = n + m$".
>
> **Base case ($n = 0$):**
>
> We need to show $m + 0 = 0 + m$.
>
> $$
> \begin{aligned}
> m + 0 &= m && \text{[definition]} \\
> 0 + m &= m && \text{[Theorem 1]}
> \end{aligned}
> $$
>
> Therefore $m + 0 = m = 0 + m$ ✓
>
> **Inductive step:**
>
> IH: Assume $m + k = k + m$ for some $k \in \mathbb{N}$.
>
> Goal: Prove $m + S(k) = S(k) + m$.
>
> Transform the left side:
> $$m + S(k) = S(m + k) \quad \text{[definition]}$$
>
> Transform the right side:
> $$S(k) + m = S(k + m) \quad \text{[Theorem 2]}$$
>
> Connect using IH:
>
> By IH, we have: $m + k = k + m$
>
> Therefore: $S(m + k) = S(k + m)$
>
> Thus: $m + S(k) = S(m + k) = S(k + m) = S(k) + m$ ✓
>
> **Conclusion:** By mathematical induction, $m + n = n + m$ for all $m, n \in \mathbb{N}$. ∎

### Key Insights

- The base case uses Theorem 1 (left identity)
- The inductive step uses Theorem 2 (left successor)
- This shows how theorems build on each other hierarchically
- Commutativity is NOT obvious from the definition—it requires proof

## Theorem 4: Associativity of Addition

{% callout_tip() %}
**Statement:**

For all $a, b, c \in \mathbb{N}$, we have $(a + b) + c = a + (b + c)$.

**In words:**

Grouping doesn't matter in addition.

**Interesting fact:**

This theorem does NOT require commutativity—they are independent properties.
{% end %}

### Proof

> We prove this by induction on $c$, keeping $a$ and $b$ fixed but arbitrary.
>
> **Base case ($c = 0$):**
>
> We need to show $(a + b) + 0 = a + (b + 0)$.
>
> Left side: $(a + b) + 0 = a + b$ [by definition]
>
> Right side: $a + (b + 0) = a + b$ [by definition]
>
> Therefore $(a + b) + 0 = a + b = a + (b + 0)$ ✓
>
> **Inductive step:**
>
> IH: Assume $(a + b) + k = a + (b + k)$ for some $k \in \mathbb{N}$.
>
> Goal: Prove $(a + b) + S(k) = a + (b + S(k))$.
>
> Transform the left side:
> $$(a + b) + S(k) = S((a + b) + k) \quad \text{[definition]}$$
>
> Transform the right side:
> $$
> \begin{aligned}
> a + (b + S(k)) &= a + S(b + k) && \text{[definition]} \\
> &= S(a + (b + k)) && \text{[definition again]}
> \end{aligned}
> $$
>
> Connect using IH:
>
> We have from IH: $(a + b) + k = a + (b + k)$
>
> Applying $S$ to both sides: $S((a + b) + k) = S(a + (b + k))$
>
> Therefore: $(a + b) + S(k) = S((a + b) + k) = S(a + (b + k)) = a + (b + S(k))$ ✓
>
> **Conclusion:** By mathematical induction, $(a + b) + c = a + (b + c)$ for all $a, b, c \in \mathbb{N}$. ∎

### Key Insights

- The right side requires applying the definition TWICE
- We never used commutativity in this proof
- The induction is on the rightmost variable (matching the recursive structure)
- This completes the characterization of addition as a commutative, associative operation

## Summary: Addition is Fully Characterized

We have proven:

1. **Left identity:** $0 + n = n$
2. **Left successor:** $S(m) + n = S(m + n)$
3. **Commutativity:** $m + n = n + m$
4. **Associativity:** $(a + b) + c = a + (b + c)$

Together with the definition (which gives right identity and right successor), we have completely characterized addition on $\mathbb{N}$.

# Defining Multiplication

With addition fully characterized, we define multiplication recursively using addition.

## Definition of Multiplication

{% callout_note() %}
**For any $n, m \in \mathbb{N}$, we define $n \times m$ by recursion on $m$:**

**Base case:**
$$n \times 0 = 0$$

**Meaning:**

Anything times zero is zero.

**Intuition:**

"n groups of 0 things = 0 things total"

**Recursive case:**
$$n \times S(m) = (n \times m) + n$$

**Meaning:**

To multiply $n$ by one-more-than-$m$, take the result of multiplying by $m$ and add $n$.

**Intuition:**

"n groups of (m+1) things = (n groups of m things) + (n more things)"
{% end %}

### Example: Computing $3 \times 2$

$$
\begin{aligned}
3 \times 2 &= 3 \times S(1) \\
&= (3 \times 1) + 3 && \text{[recursive case]} \\
&= (3 \times S(0)) + 3 \\
&= ((3 \times 0) + 3) + 3 && \text{[recursive case again]} \\
&= (0 + 3) + 3 && \text{[base case]} \\
&= 3 + 3 && \text{[Theorem 1]} \\
&= 6
\end{aligned}
$$

## What Must Be Proven

From the definition alone:

- ✓ We **know** $n \times 0 = 0$ (base case)
- ✓ We **know** $n \times S(m) = (n \times m) + n$ (recursive case)
- ✗ We **don't know** $0 \times n = 0$ (must prove!)
- ✗ We **don't know** $S(m) \times n = (m \times n) + n$ (must prove!)
- ✗ We **don't know** $m \times n = n \times m$ (must prove!)
- ✗ We **don't know** $(a \times b) \times c = a \times (b \times c)$ (must prove!)
- ✗ We **don't know** $a \times (b + c) = (a \times b) + (a \times c)$ (must prove!)

# Main Theorems of Multiplication

## Theorem 5: Left Identity for Multiplication

{% callout_tip() %}
**Statement:**

For all $n \in \mathbb{N}$, we have $0 \times n = 0$.

**In words:**

Zero times anything is zero.
{% end %}

### Proof

> We prove this by induction on $n$.
>
> **Base case:** $0 \times 0 = 0$ [by definition] ✓
>
> **Inductive step:**
>
> IH: Assume $0 \times k = 0$ for some $k \in \mathbb{N}$.
>
> Goal: Prove $0 \times S(k) = 0$.
>
> $$
> \begin{aligned}
> 0 \times S(k) &= (0 \times k) + 0 && \text{[definition]} \\
> &= 0 + 0 && \text{[by IH]} \\
> &= 0 && \text{[definition of addition]}
> \end{aligned}
> $$
>
> **Conclusion:** By induction, $0 \times n = 0$ for all $n \in \mathbb{N}$. ∎

## Theorem 6: Left Successor for Multiplication

{% callout_tip() %}
**Statement:**

For all $m, n \in \mathbb{N}$, we have $S(m) \times n = (m \times n) + n$.

**In words:**

Multiplying the successor of $m$ by $n$ equals $(m \times n) + n$.

**Dependency:**

This proof requires associativity and commutativity of addition.
{% end %}

### Proof (Sketch)

> We prove by induction on $n$.
>
> Base case: Both sides equal $0$.
>
> Inductive step uses the fact that:
> $$S(m) \times S(k) = (S(m) \times k) + S(m) = ((m \times k) + k) + S(m)$$
>
> And we need to show this equals:
> $$(m \times S(k)) + S(k) = ((m \times k) + m) + S(k)$$
>
> This requires rearranging the sum using commutativity and associativity of addition. ∎

## Theorem 7: Commutativity of Multiplication

{% callout_tip() %}
**Statement:**

For all $m, n \in \mathbb{N}$, we have $m \times n = n \times m$.

**In words:**

Order doesn't matter in multiplication.

**Dependency:**

Requires Theorems 5 and 6.
{% end %}

### Proof

> We prove by induction on $n$.
>
> **Base case ($n = 0$):**
>
> $$
> \begin{aligned}
> m \times 0 &= 0 && \text{[definition]} \\
> 0 \times m &= 0 && \text{[Theorem 5]}
> \end{aligned}
> $$
>
> Therefore $m \times 0 = 0 \times m$ ✓
>
> **Inductive step:**
>
> IH: Assume $m \times k = k \times m$ for some $k \in \mathbb{N}$.
>
> Goal: Prove $m \times S(k) = S(k) \times m$.
>
> $$
> \begin{aligned}
> m \times S(k) &= (m \times k) + m && \text{[definition]} \\
> &= (k \times m) + m && \text{[by IH]} \\
> &= S(k) \times m && \text{[Theorem 6]}
> \end{aligned}
> $$
>
> **Conclusion:** By induction, $m \times n = n \times m$ for all $m, n \in \mathbb{N}$. ∎

## Theorem 8: Distributivity

{% callout_tip() %}
**Statement:**

For all $a, b, c \in \mathbb{N}$, we have $a \times (b + c) = (a \times b) + (a \times c)$.

**In words:**

Multiplication distributes over addition.

**Dependency:**

Requires associativity of addition (Theorem 4).
{% end %}

### Proof

> We prove by induction on $c$.
>
> **Base case ($c = 0$):**
>
> $$
> \begin{aligned}
> a \times (b + 0) &= a \times b && \text{[addition definition]} \\
> (a \times b) + (a \times 0) &= (a \times b) + 0 = a \times b && \text{[multiplication definition]}
> \end{aligned}
> $$
>
> Both sides equal $a \times b$ ✓
>
> **Inductive step:**
>
> IH: Assume $a \times (b + k) = (a \times b) + (a \times k)$.
>
> Goal: Prove $a \times (b + S(k)) = (a \times b) + (a \times S(k))$.
>
> Left side:
> $$
> \begin{aligned}
> a \times (b + S(k)) &= a \times S(b + k) && \text{[addition definition]} \\
> &= (a \times (b + k)) + a && \text{[multiplication definition]}
> \end{aligned}
> $$
>
> Right side:
> $$
> \begin{aligned}
> (a \times b) + (a \times S(k)) &= (a \times b) + ((a \times k) + a) && \text{[multiplication definition]}
> \end{aligned}
> $$
>
> Using IH: $(a \times (b + k)) + a = ((a \times b) + (a \times k)) + a$
>
> By associativity of addition: $((a \times b) + (a \times k)) + a = (a \times b) + ((a \times k) + a)$ ✓
>
> **Conclusion:** By induction, distributivity holds for all $a, b, c \in \mathbb{N}$. ∎

## Theorem 9: Associativity of Multiplication

{% callout_tip() %}
**Statement:**

For all $a, b, c \in \mathbb{N}$, we have $(a \times b) \times c = a \times (b \times c)$.

**In words:**

Grouping doesn't matter in multiplication.

**Dependency:**

Requires distributivity (Theorem 8).
{% end %}

### Proof (Sketch)

> We prove by induction on $c$.
>
> Base case: Both sides equal $0$.
>
> Inductive step uses distributivity to expand:
> $$a \times (b \times S(k)) = a \times ((b \times k) + b) = (a \times (b \times k)) + (a \times b)$$
>
> Combined with the IH, this gives the desired result. ∎

## Summary: Multiplication is Fully Characterized

We have proven:

5. **Left identity:** $0 \times n = 0$
6. **Left successor:** $S(m) \times n = (m \times n) + n$
7. **Commutativity:** $m \times n = n \times m$
8. **Distributivity:** $a \times (b + c) = (a \times b) + (a \times c)$
9. **Associativity:** $(a \times b) \times c = a \times (b \times c)$

**All 9 theorems proven from just the 5 Peano Axioms using induction!**

# Examples

Examples that illuminate subtle aspects of the theory.

## Why Order Matters in Recursive Definition

**Question:**

Why did we define addition as recursive on the RIGHT argument instead of the LEFT?

Consider trying to define it recursively on the LEFT:

$$
\begin{aligned}
0 + n &= n \\
S(m) + n &= S(m + n)
\end{aligned}
$$

**Problem:**

How would you compute $3 + 2$ using these rules?

$$S(S(S(0))) + S(S(0)) = ?$$

You cannot apply either rule! The left side has $S(\ldots)$, not $0$.

**With our definition (recursive on RIGHT):**

$$
\begin{aligned}
3 + 2 &= 3 + S(1) \\
&= S(3 + 1) \\
&= S(3 + S(0)) \\
&= S(S(3 + 0)) \\
&= S(S(3)) \\
&= 5 \checkmark
\end{aligned}
$$

The successor is on the RIGHT, so we can successfully recurse.

## Why We Needed to Prove $0 + n = n$

**It seems obvious:**

"Zero plus anything is that thing!"

**But look carefully at what we have:**

- Definition gives: $n + 0 = n$ (zero on RIGHT)
- We want: $0 + n = n$ (zero on LEFT)

**These are DIFFERENT statements!**

To see this, try computing $0 + 2$ using ONLY the definition:

$$
\begin{aligned}
0 + 2 &= 0 + S(1) \\
&= S(0 + 1) && \text{[definition: } n + S(m) = S(n+m)\text{]} \\
&= S(0 + S(0)) \\
&= S(S(0 + 0)) && \text{[definition again]} \\
&= S(S(0)) && \text{[base case: } n + 0 = n\text{]} \\
&= 2
\end{aligned}
$$

It works, but we had to COMPUTE it through multiple steps—it's not immediate from the definition!

That's why we proved it as Theorem 1.

## Non-Example: Clock Arithmetic Modulo 5

Consider the numbers $\{0, 1, 2, 3, 4\}$ with successor wrapping around:

**Successor function:**
- $S(0) = 1, S(1) = 2, S(2) = 3, S(3) = 4, S(4) = 0$

```
    0
   ↗ ↖
  4   1
  ↓   ↑
    3-2
```

**Which Peano Axioms does this violate?**

- Axiom 1: 0 exists ✓
- Axiom 2: $S(n)$ always in the set ✓
- Axiom 3: Injectivity? All successors are different ✓
- Axiom 4: $S(n) \neq 0$? **FAILS!** We have $S(4) = 0$ ✗
- Axiom 5: Minimality/Induction? **FAILS!** Can't reach all from 0 via repeated succession without cycles ✗

**Arithmetic is different in this structure:**
- In $\mathbb{Z}/5\mathbb{Z}$: $3 + 2 = 0$ (mod 5)
- In $\mathbb{N}$: $3 + 2 = 5$

This is a DIFFERENT mathematical structure (called a cyclic group), not the natural numbers!

## Edge Case: Subtraction Doesn't Always Exist

**In $\mathbb{N}$, we can add any two numbers. But can we always subtract?**

**Question:**

What is $3 - 5$ in $\mathbb{N}$?

**Problem:**

There is no natural number $n$ that satisfies $5 + n = 3$.

Why not?
- $5 + 0 = 5 > 3$
- $5 + 1 = 6 > 3$
- $5 + 2 = 7 > 3$
- All sums $5 + n$ satisfy $5 + n \geq 5 > 3$

**Conclusion:**

Subtraction is NOT always defined in $\mathbb{N}$! The set is not closed under subtraction.

This fundamental limitation is why we need to construct the **integers $\mathbb{Z}$** (coming in Domain 1.2).

## Comparison Across Number Systems

| Property | $\mathbb{N}$ | $\mathbb{Z}$ | $\mathbb{Q}$ | $\mathbb{R}$ |
|----------|--------------|--------------|--------------|--------------|
| Has 0 | ✓ | ✓ | ✓ | ✓ |
| Closed under + | ✓ | ✓ | ✓ | ✓ |
| Closed under × | ✓ | ✓ | ✓ | ✓ |
| Closed under − | ✗ | ✓ | ✓ | ✓ |
| Closed under ÷ | ✗ | ✗ | ✓ (except ÷0) | ✓ (except ÷0) |
| Has negatives | ✗ | ✓ | ✓ | ✓ |
| Has fractions | ✗ | ✗ | ✓ | ✓ |
| Well-ordered | ✓ | ✗ | ✗ | ✗ |
| Has minimum | ✓ (it's 0) | ✗ | ✗ | ✗ |
| Induction works | ✓ | ✗ | ✗ | ✗ |
| Discrete | ✓ | ✓ | ✓ | ✗ |
| Complete | ✗ | ✗ | ✗ | ✓ |

**Key insight:**

$\mathbb{N}$ is the MOST RESTRICTED but has the MOST STRUCTURE (well-ordering, induction, minimality).

## Why Induction Only Works in $\mathbb{N}$

**Try proving "for all integers $n$, $P(n)$" by standard induction:**

**Problem:**

Where do you start the induction?
- Start at 0? What about $-1, -2, -3, \ldots$?
- Start at the minimum? There IS NO minimum in $\mathbb{Z}$!

**Induction requires:**
1. A starting point (base case at 0 in $\mathbb{N}$)
2. A way to reach all elements from that starting point (successor function)

$\mathbb{Z}$ has no minimum element, so standard induction fails.

Note: We CAN use modified induction techniques (separate induction on positive and negative integers, or strong induction), but these are different from the natural induction available in $\mathbb{N}$.

## The Complete Hierarchy

```
ℕ (Peano axioms)
  ↓ (ordered pairs + equivalence relation)
ℤ (integers - adds subtraction)
  ↓ (ordered pairs + equivalence relation)
ℚ (rationals - adds division)
  ↓ (Dedekind cuts OR Cauchy sequences)
ℝ (reals - fills holes, adds continuity)
  ↓ (ordered pairs)
ℂ (complex numbers - adds √-1)
```

**Remarkable fact:**

ALL of mathematics is built on the foundation of the 5 Peano Axioms!

# Further Exploration

Open-ended investigations and creative mathematical thinking.

## What If We Modified Axiom 4?

**Original Axiom 4:**

$S(n) \neq 0$ for all $n \in \mathbb{N}$

**Modified version:**

$S(4) = 0$, but $S(n) \neq 0$ for $n < 4$

**What structure results?**

Answer: A cyclic group of order 5, denoted $\mathbb{Z}/5\mathbb{Z}$ or $\mathbb{Z}_5$

**Properties:**
- **Finite:** Exactly 5 elements: $\{0, 1, 2, 3, 4\}$
- **Cyclic:** Applying successor repeatedly cycles back to 0
- **Addition mod 5:** $3 + 3 = 6 \equiv 1 \pmod{5}$
- **No well-ordering:** The usual order breaks down in cycles
- **Induction fails:** Can't reach all elements from 0 without repeating
