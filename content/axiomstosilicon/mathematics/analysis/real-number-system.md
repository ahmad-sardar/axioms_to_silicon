+++
title = "Real Number System"
slug = "real-number-system"
toc = true
+++

# Two constructions, one object

$\mathbb{R}$ can be built in two ways.

1. Dedekind's construction (cuts of $\mathbb{Q}$).
2. Cauchy's construction (equivalence classes of Cauchy sequences of rationals).

Either way, $\mathbb{R}$ is built on top of $\mathbb{Q}$, and the two constructions produce isomorphic results: the same field, the same order, the same completeness property, just built from different raw material. Because it doesn't matter which one you use, it makes sense to stop building and instead name the properties both constructions land on. From here on we work from those properties (the axioms below) directly, without going back to either construction.

# Required Vocabulary

## Field

{% callout_note() %}
A **field** is an abstract algebraic structure: a set equipped with two operations, addition and multiplication, satisfying the field axioms below.
{% end %}

## Total order

{% callout_note() %}
A **total order** on a set $S$ is a relation that, for every pair of elements $a, b \in S$, tells you which one is "less than" the other. $\mathbb{R}$ has a total order.
{% end %}

## Ordered field

{% callout_note() %}
An **ordered field** is a field together with a total order that is compatible with the field operations (see the order axioms below).
{% end %}

$\mathbb{R}$ is an ordered field. So is $\mathbb{Q}$. $\mathbb{C}$ is not: there is no total order on $\mathbb{C}$ consistent with its field structure. If there were, $i^2=-1$ would force $-1>0$, and then adding $-1>0$ to itself would give $-2>0$, contradicting $-2<0$.

## Upper bound and bounded above

{% callout_note() %}
A real number $M$ is an **upper bound** for a set $S$ if $s \le M$ for every $s \in S$. $S$ is **bounded above** if at least one upper bound for $S$ exists.
{% end %}

- Let $S = \{1,2,3\}$. Then $3$ is an upper bound, $4$ is an upper bound, and $100$ is an upper bound. $2$ is not an upper bound for $S$.
- Let $S = (0,1) = \{x \in \mathbb{R} : 0 < x < 1\}$. Then $1$ is an upper bound, and so is $1.5$. The number $0.99$ is not an upper bound, because $0.995 \in S$ and $0.995 > 0.99$.

$\mathbb{N}$ has no upper bound in $\mathbb{R}$ — that's the Archimedean property, proved below.

## Supremum (least upper bound)

**Statement:**

#### Let $S$ be a nonempty subset of $\mathbb{R}$ that is bounded above. $\alpha$ is the **supremum** of $S$, written **$\sup S$**, when:

{% callout_note() %}

(i) $\alpha$ is an upper bound for $S$: $s \le \alpha$ for every $s \in S$.

(ii) $\alpha$ is the *smallest* upper bound: if $M$ is any upper bound for $S$, then $\alpha \le M$. Said differently, no number smaller than $\alpha$ is an upper bound for $S$.
{% end %}

**Do not mix up maximum with supremum:**

A maximum must be an element of $S$; a supremum does not have to be. When the maximum exists, it equals the supremum — it's an upper bound by virtue of being the largest member, and no smaller number can be an upper bound without excluding the maximum itself. But the supremum can exist when the maximum doesn't: $(0,1)$ has no largest element (for any $x \in (0,1)$, $(x+1)/2$ is bigger and still in $(0,1)$), yet $\sup(0,1) = 1$.

## Infimum (greatest lower bound) and minimum

{% callout_note() %}
A real number $m$ is a **lower bound** for $S$ if $m \le s$ for every $s \in S$. The **infimum** of $S$, written $\inf S$, is the greatest lower bound: $\beta$ such that $\beta$ is a lower bound, and $\beta \ge m$ for every other lower bound $m$.
{% end %}

$\inf(0,1) = 0$. In general $\inf S = -\sup(-S)$, where $-S = \{-s : s \in S\}$.

Minimum versus infimum works exactly like maximum versus supremum: a minimum must be a member of $S$ and may not exist; the infimum doesn't have to be a member and exists whenever $S$ is nonempty and bounded below. $(0,1)$ has no minimum but $\inf(0,1) = 0$. $[0,1]$ has both a minimum and an infimum, and they agree: $0$.

Side by side: maximum and minimum must live in $S$ and can fail to exist; supremum and infimum don't have to live in $S$ and (given completeness, below) always exist for nonempty bounded sets. When the max/min exists it equals the sup/inf.

# The axioms of $\mathbb{R}$

#### $\mathbb{R}$ is defined by three groups of axioms.

## Field axioms

{% callout_note() %}
A1. Commutativity: $a+b=b+a$.

A2. Associativity: $(a+b)+c = a+(b+c)$.

A3. Distributivity: $a(b+c) = ab+ac$.

A4. Additive identity: $0$ is the additive identity for $\mathbb{R}$.

A5. Additive inverse: for every $a \in \mathbb{R}$, there is a unique $b \in \mathbb{R}$ such that $a+b=0$.

A6. Multiplicative identity: $1$ is the multiplicative identity for $\mathbb{R}$, and $1 \neq 0$.

A7. Multiplicative inverse: for every $a \in \mathbb{R}$ with $a \neq 0$, there is a unique $b \in \mathbb{R}$ such that $a \cdot b = 1$.

A8. Commutativity of multiplication: $a \cdot b = b \cdot a$.

A9. Associativity of multiplication: $(a \cdot b) \cdot c = a \cdot (b \cdot c)$.
{% end %}

These nine hold for $\mathbb{Q}$ and $\mathbb{C}$ too. The field axioms alone don't distinguish $\mathbb{R}$ from either — the next two groups do the distinguishing.

## Order axioms

{% callout_note() %}
There is a relation $<$ on $\mathbb{R}$ satisfying:

o1. Trichotomy: for every $a,b \in \mathbb{R}$, exactly one of $a<b$, $a=b$, $a>b$ holds.

o2. Transitivity: if $a<b$ and $b<c$, then $a<c$.

o3. Compatibility with addition: for all $a,b,c \in \mathbb{R}$, if $a<b$, then $a+c < b+c$.

o4. Compatibility with multiplication: for all $a,b,c \in \mathbb{R}$, if $a<b$ and $c>0$, then $ac<bc$. If instead $c<0$, the inequality flips: $ac>bc$.
{% end %}

A field with both groups (field + order) is an ordered field. $\mathbb{Q}$ and $\mathbb{R}$ both qualify. $\mathbb{C}$ doesn't, for the reason given above under "ordered field." But ordered-field axioms alone still don't separate $\mathbb{R}$ from $\mathbb{Q}$ — that takes one more axiom.

## Completeness axiom (least upper bound property)

{% callout_note() %}
Every nonempty subset of $\mathbb{R}$ that is bounded above has a supremum in $\mathbb{R}$.
{% end %}

$\mathbb{Q}$ fails this. Take $S = \{q \in \mathbb{Q} : q^2 < 2\}$: nonempty ($1 \in S$), bounded above (by $2$), but its least upper bound would have to be $\sqrt{2}$, which isn't rational. So $S$ has upper bounds in $\mathbb{Q}$ but no *least* one in $\mathbb{Q}$ — there's a hole where $\sqrt{2}$ should be. $\mathbb{R}$ fills it: $\{x \in \mathbb{R} : x^2 < 2\}$ has supremum $\sqrt{2} \in \mathbb{R}$.

That is exactly why $\mathbb{R}$ repairs the incompleteness of $\mathbb{Q}$.

# Consequences of completeness

## The supremum characterization lemma

**Statement.**

Let $S$ be a nonempty subset of $\mathbb{R}$ that is bounded above, and let $\alpha = \sup S$. Then:

{% callout_tip() %}


i. $s \le \alpha$ for every $s \in S$.

ii. for every $\varepsilon > 0$, there is some $s \in S$ with $\alpha - \varepsilon < s \le \alpha$.
{% end %}

Part (i) is just the statement that $\alpha$ is an upper bound. Part (ii) says: no matter how small a positive $\varepsilon$ you pick, some element of $S$ is within $\varepsilon$ of $\alpha$ — nothing less than $\alpha$ can be an upper bound.

**Proof.**

> Part (i) is immediate from the definition of supremum.
>
> Part (ii): suppose, for contradiction, that there is no such $s$. Then $s \le \alpha - \varepsilon$ for every $s \in S$, which makes $\alpha - \varepsilon$ an upper bound for $S$ smaller than $\alpha$. That contradicts $\alpha$ being the *least* upper bound. So no such $\varepsilon$ exists, and part (ii) holds.

**Example.**

Let $S=(0,1)$, so $\sup S = 1$. Pick $\varepsilon=0.01$: then $\alpha-\varepsilon=0.99$, and $s=0.995 \in S$ beats it. Pick $\varepsilon = 0.0001$: then $\alpha - \varepsilon = 0.9999$, and $s = 0.99995 \in S$ beats it. However small $\varepsilon$ is, some element of $S$ is that close to the supremum.

## The Archimedean property

**Statement.**

{% callout_tip() %}
For every real number $x$, there exists a natural number $n$ such that $x < n$.
{% end %}

It isn't obvious up front that $\mathbb{R}$ contains arbitrarily large integers — the axioms only say $\mathbb{R}$ is a complete ordered field. The Archimedean property says $\mathbb{R}$ has no "infinitely large" elements that outrun every natural number.

**Proof by contradiction.**

> Assume $\mathbb{N}$ is bounded above. $\mathbb{N}$ is nonempty, so by the completeness axiom it has a supremum $\alpha = \sup \mathbb{N}$.
>
> Apply the supremum characterization lemma with $\varepsilon = 1$: there is some $n_0 \in \mathbb{N}$ with $\alpha - 1 < n_0$, i.e. $\alpha < n_0 + 1$.
>
> But $n_0 \in \mathbb{N}$ means $n_0 + 1 \in \mathbb{N}$ too, and it exceeds $\alpha$. That contradicts $\alpha$ being an upper bound for $\mathbb{N}$.
>
> So $\mathbb{N}$ is not bounded above: for every $x \in \mathbb{R}$, some $n \in \mathbb{N}$ has $n > x$. $\blacksquare$

**Equivalent form, used constantly in $\varepsilon$-$\delta$ proofs later:** for any $\varepsilon > 0$, there exists $n \in \mathbb{N}$ with $1/n < \varepsilon$. (Apply the theorem to $x = 1/\varepsilon$ to get $n > 1/\varepsilon$, then divide.)

## Density of $\mathbb{Q}$ in $\mathbb{R}$

**Statement.**

{% callout_tip() %}
For every pair of real numbers $a, b$ with $a < b$, there exists a rational number $q$ such that $a < q < b$.
{% end %}

The rationals are "dense" in $\mathbb{R}$: no interval, however small, is free of rational numbers.

**Proof by construction.**

> Since $b - a > 0$, the Archimedean property gives a natural number $n$ with $1/n < b-a$.
>
> Let $m$ be the smallest integer with $m > na$ (the Archimedean property guarantees such integers exist, and the smallest one exists because that set of integers is bounded below). Since $m$ is smallest, $m - 1 \le na$, so $m \le na + 1$.
>
> Verify $a < m/n < b$. First, $m > na$ gives $m/n > a$ directly. Second, $m \le na+1$ gives $m/n \le a + 1/n < a + (b-a) = b$, since $1/n < b - a$.
>
> So $q = m/n$ is rational and satisfies $a < q < b$. $\blacksquare$

**Worked Example.**

Let $a = 3.141$, $b = 3.142$, so $b-a = 0.001$. Take $n = 10000$ (since $1/10000 < 0.001$). The smallest integer above $na = 31410$ is $m = 31411$. Check: $31411/10000 = 3.1411$, and indeed $3.141 < 3.1411 < 3.142$.

**Density of the irrationals.**

The same holds for irrationals: between any two distinct reals there's an irrational one too (apply density of $\mathbb{Q}$ to $a/\sqrt2$ and $b/\sqrt2$, then multiply the resulting rational by $\sqrt2$). $\mathbb{Q}$ and $\mathbb{R} \setminus \mathbb{Q}$ are both dense in $\mathbb{R}$, thoroughly interleaved: between any two rationals sits an irrational, and between any two irrationals sits a rational.

# Absolute value and distance

## Absolute value

{% callout_note() %}
For $x \in \mathbb{R}$, the **absolute value** is $$|x| = \begin{cases} x & x \ge 0 \\ -x & x < 0 \end{cases}$$
{% end %}

$-x$ here just means "flip the sign of $x$," so when $x$ is already negative, $-x$ comes out positive — the definition always produces a nonnegative number. $|x-a|$ measures the distance between $x$ and $a$ on the number line: $|7-3|=4$, $|2-5|=|-3|=3$.

## The triangle inequality

{% callout_tip() %}
**Statement.** For all $a, b \in \mathbb{R}$, $$|a+b| \le |a| + |b|.$$
{% end %}

This is the single most used inequality in analysis: the distance from the origin to $a+b$ is at most the distance to $a$ plus the distance to $b$. Equality holds exactly when $a$ and $b$ share a sign.

**Proof.**

> By definition, $-|a| \le a \le |a|$ and $-|b| \le b \le |b|$. Adding these gives $-(|a|+|b|) \le a+b \le |a|+|b|$, which is exactly $|a+b| \le |a|+|b|$. $\blacksquare$

**Example.**

$a=3, b=-5$: $|a+b|=|-2|=2 \le |a|+|b|=8$. And $a=3,b=5$ (same sign): $|a+b|=8=|a|+|b|$, equality.

A companion, the **reverse triangle inequality**, says $\big||a|-|b|\big| \le |a-b|$ — it bounds the difference of the sizes by the size of the difference, and shows up whenever you need to bound something like $||f(x)|-|f(a)||$.

The distance function $|a-b|$ satisfies: nonnegativity ($|a-b|\ge 0$, zero only when $a=b$), symmetry ($|a-b|=|b-a|$), and the triangle inequality for distance ($|a-c|\le|a-b|+|b-c|$). These three properties are exactly the axioms of a metric space later on — the absolute value on $\mathbb{R}$ is the first example of a metric.

# What ordered-field axioms alone cannot do

Field and order axioms give you all of ordinary arithmetic and every inequality manipulation. What they *cannot* guarantee is that limits exist, that bounded sets have suprema, or that $\mathbb{N}$ is unbounded — that's all completeness's job.

Concretely: in $\mathbb{Q}$, define $a_1 = 1$, $a_{n+1} = \frac{a_n}{2} + \frac{1}{a_n}$ (the Babylonian method for computing $\sqrt2$).

- $a_1 = 1$
- $a_2 = 1/2 + 1/1 = 3/2 = 1.5$
- $a_3 = 3/4 + 2/3 = 17/12 \approx 1.4167$
- $a_4 = 17/24 + 12/17 = 577/408 \approx 1.41422$

Every term is rational, and the terms crowd closer and closer together — the sequence is Cauchy. But in $\mathbb{Q}$ it has nowhere to converge to, because $\sqrt2 \notin \mathbb{Q}$. In $\mathbb{R}$, the same sequence converges to $\sqrt2$, because $\mathbb{R}$ is complete. That gap is exactly what the completeness axiom closes.

# What completeness costs

Completeness isn't free. $\mathbb{Q}$ is countable — you can list every rational in a sequence $q_1, q_2, q_3, \ldots$. $\mathbb{R}$ is uncountable: Cantor's diagonal argument shows no list can ever contain every real number. So completing $\mathbb{Q}$ to $\mathbb{R}$ doesn't just patch a few holes — the holes are everywhere, and the irrationals vastly outnumber the rationals even though the rationals are dense.
