+++
title = "The Construction of the Integers from the Natural Numbers"
+++

# Failure of Natural Numbers

## The equation that has no answer
Work only inside $\mathbb{N}$. Take two equations.

**First equation.**

$$5 + x = 8 \tag{1}$$

Try $x = 3$. Then $5 + 3 = 8$, so the equation is satisfied. A solution exists inside $\mathbb{N}$.

**Second equation.**

$$8 + x = 5 \tag{2}$$

**Claim.**

Equation $(2)$ has no solution in $\mathbb{N}$.

**Proof.**

> Take any $n \in \mathbb{N}$. The order on $\mathbb{N}$ was defined by saying that $a \le b$ holds exactly when there is some $k \in \mathbb{N}$ with $a + k = b$. Apply that definition with $a = 8$, $k = n$, and $b = 8 + n$. It gives $8 \le 8 + n$. Also $5 < 8$ holds in $\mathbb{N}$. Chaining the two, $5 < 8 + n$, so $8 + n \neq 5$. Since $n$ was arbitrary, no natural number solves the equation. $\blacksquare$

This means the equation $a + x = b$ is solvable in $\mathbb{N}$ exactly when $a \le b$, and unsolvable otherwise.

## Why the obvious fix is not a fix

New symbols cannot simply be declared. Declaring $-3$ to be the solution of $8 + x = 5$ is not yet mathematics, for three reasons.

1. **The symbol has no definition.** Saying "$-3$ is the thing that solves the equation" names the thing without building it.
2. **The arithmetic has no definition.** What is $(-3) \times (-5)$? Each product and sum would have to be declared separately, and every declaration is a new assumption.
3. **The properties have to be re-assumed rather than proved.** Associativity on the enlarged system would be a new claim about new objects.

Declaring symbols moves the work rather than doing it. Building the integers out of material already in hand does the work instead: operations are defined coordinate-wise from addition and multiplication on $\mathbb{N}$, and every property is then proved rather than assumed.

## The working rule, we derive it later

1. An integer is written as a pair of natural numbers $(a, b)$, and the pair is read as "$a$ minus $b$". So $(8, 5)$ is the integer $3$ and $(5, 8)$ is the integer $-3$.
2. Two pairs stand for the same integer exactly when $$a + d = b + c \quad \text{for the pairs } (a,b) \text{ and } (c,d). \tag{3}$$ So $(5,8)$ and $(0,3)$ stand for the same integer, because $5 + 3 = 8 + 0$.
3. Addition is done coordinate by coordinate. $$(a, b) + (c, d) = (a + c,\ b + d) \tag{4}$$
4. Multiplication is done by this formula. $$(a, b) \cdot (c, d) = (ac + bd,\ ad + bc) \tag{5}$$
5. The negative of $(a,b)$ is $(b,a)$, which means the two coordinates swap places.

All theorems already proved about $\mathbb{N}$ remain valid and are the only facts used below.

**One full computation with the rule.**

Compute $(-2) \times 3$ using pairs. Write $-2$ as $(0,2)$ and $3$ as $(3,0)$. Apply formula $(5)$:

$$(0,2)\cdot(3,0) = (0\cdot 3 + 2 \cdot 0,\ 0 \cdot 0 + 2 \cdot 3) = (0,\ 6)$$

The pair $(0,6)$ is read as "$0$ minus $6$", which is $-6$.

**A second full computation, to show rule 2 doing work.**

Write $-2$ as $(4,6)$ and $3$ as $(9,6)$. Apply formula $(5)$:

$$(4,6)\cdot(9,6) = (4 \cdot 9 + 6 \cdot 6,\ 4 \cdot 6 + 6 \cdot 9) = (72,\ 78)$$

Check that $(72,78)$ stands for the same integer as $(0,6)$. Rule 2 asks whether $72 + 6 = 78 + 0$. Both sides equal $78$.

---

# Vocabulary you would need

## What is imported from Naturals

|\#|Imported fact|Statement|
|---|---|---|
|N1|Addition is associative and commutative|$a + (b+c) = (a+b)+c$ and $a+b = b+a$|
|N2|Multiplication is associative and commutative|$a(bc) = (ab)c$ and $ab = ba$|
|N3|Multiplication distributes over addition|$a(b+c) = ab + ac$|
|N4|Identities|$a + 0 = a$ and $a \cdot 1 = a$|
|N5|Additive cancellation|if $a + c = b + c$ then $a = b$|
|N6|Order and trichotomy|$a \le b$ means there is $k \in \mathbb{N}$ with $a + k = b$, and exactly one of $a<b$, $a=b$, $a>b$ holds|

Fact **N5** is the one to remember: it makes the whole construction work.

## Ordered pair

An **ordered pair** $(a,b)$ is two objects written in a fixed order, with the rule that $(a,b) = (c,d)$ holds exactly when $a = c$ and $b = d$.

So $(3,5) \neq (5,3)$.

## Cartesian product

The **Cartesian product** $\mathbb{N} \times \mathbb{N}$ is the set of all ordered pairs whose two coordinates are both natural numbers.

$$\mathbb{N} \times \mathbb{N} = \{(a,b) : a \in \mathbb{N} \text{ and } b \in \mathbb{N}\}$$

## Relation

A **relation** on a set $S$ is a rule that, given two elements of $S$, answers yes or no. On $\{1,2,3\}$ the relation "is less than" answers yes for $(1,2)$ and no for $(2,1)$.

## Equivalence relation

An **equivalence relation** on $S$, written $\sim$, is a relation with these three properties.

1. **Reflexive.** For every $x \in S$, $x \sim x$ holds.
2. **Symmetric.** For all $x, y \in S$, if $x \sim y$ then $y \sim x$.
3. **Transitive.** For all $x,y,z \in S$, if $x \sim y$ and $y \sim z$ then $x \sim z$.

## Equivalence class

$$[x] = \{y \in S : y \sim x\}$$

- **Type.** $[x]$ is a **set**, not an element. If $x$ is a pair, then $[x]$ is a set of pairs.

## Representative

A **representative** of the class $[x]$ is any element of that class. Writing $[(3,5)]$ means the class, and the pair $(3,5)$ written inside the brackets is a representative that was chosen in order to name the class.

## Quotient set

The quotient set $S/\sim$ is the set whose elements are the equivalence classes.

$$S/\sim \ = \ \{[x] : x \in S\}$$

- Under "same remainder on division by $3$" on the integers, the quotient set has exactly three elements, namely $[0]$, $[1]$, and $[2]$. It is a set of three sets, and each of those three sets is infinite.
- Read the slash aloud as "modulo", meaning "with the classes treated as single objects".

## Partition

A collection of subsets of $S$ is a **partition** of $S$ when three things hold. Every subset in it is non-empty, no two of them share an element, and their union is all of $S$.

## Well-defined

An operation on classes is **well-defined** when the answer does not change if you rename the inputs by choosing different representatives.

$$\text{if } x \sim x' \text{ and } y \sim y', \text{ then } f(x,y) \sim f(x',y'). \tag{6}
$$

"Well-defined" is not praise for the quality of a definition. It means the proposed rule really does determine one single output for each pair of inputs, instead of a different output depending on which names you happened to write down. A rule that fails this test is not a bad definition — it is not a definition at all.

## Cancellation

**Cancellation for addition in $\mathbb{N}$** is imported fact **N5**. If $a + c = b + c$ then $a = b$.

**Warning to carry forward.**

Cancellation is a theorem, not an act of subtraction. Subtraction does not exist yet. This distinction is exactly why the construction can use cancellation without becoming circular.

## Injective function, and embedding

A function $f : A \to B$ is **injective** when different inputs always give different outputs: if $f(m) = f(n)$ then $m = n$.

An **embedding** of one number system into another is an injective function that also turns sums into sums and products into products.

What actually happens is that a perfect copy of $\mathbb{N}$ is found sitting inside $\mathbb{Z}$, while the original $\mathbb{N}$ stays outside.

## The algebraic labels

1. A **commutative monoid** is a set with one operation that is associative and commutative, together with an identity element.
2. A **commutative group** is a commutative monoid in which every element $x$ has an inverse $y$ with $x + y = 0$.
3. A **commutative ring with unity** is a set with addition and multiplication such that it is a commutative group under addition, a commutative monoid under multiplication with identity $1$, and multiplication distributes over addition.
4. An **integral domain** is a commutative ring with unity in which $1 \neq 0$ and there are no zero divisors: $xy = 0$ forces $x = 0$ or $y = 0$.

---

# Building the Integers

## The raw material

Take the set $\mathbb{N} \times \mathbb{N}$, meaning all pairs of natural numbers.

## The intended reading, and a warning about it

Read the pair $(a,b)$ as standing for "$a$ minus $b$".

- $(8,5)$ stands for $3$.
- $(5,8)$ stands for $-3$.
- $(4,4)$ stands for $0$.

**Warning.**

That reading is motivation and nothing more. It cannot be used inside any proof. The minus sign has no meaning yet. Everything below uses only addition, multiplication, and order on $\mathbb{N}$.

## Turning the intended reading into a definition

**Concrete case.**

The pairs $(8,5)$ and $(13,10)$ should stand for the same integer $3$.

**Motivation only (illegal in proofs).**

$8 - 5 = 3$ and $13 - 10 = 3$.

**The legal test.**

Add in a cross pattern so only addition appears.

{% callout_note() %}
**Definition 3.1.**

For pairs $(a,b)$ and $(c,d)$ in $\mathbb{N}\times\mathbb{N}$, write $$(a,b) \sim (c,d) \quad \text{exactly when} \quad a + d = b + c. \tag{7}$$
{% end %}

Check: $(8,5) \sim (13,10)$ asks whether $8 + 10 = 5 + 13$. Both sides are $18$. And $(5,8) \sim (0,3)$ asks whether $5 + 3 = 8 + 0$. Both sides are $8$.

Notice which coordinates get added together. The first coordinate of the left pair is added to the second coordinate of the right pair. Writing $a + c = b + d$ instead is the standard slip, and it is wrong.

## Equality theorems

{% callout_tip() %}
**Theorem 3.2.**

The relation $\sim$ is reflexive, symmetric, and transitive on $\mathbb{N}\times\mathbb{N}$.
{% end %}

**Proof of reflexivity.**

> Take any pair $(a,b)$. Formula $(7)$ says that $(a,b)\sim(a,b)$ holds exactly when $a + b = b + a$. That equation is true by **N1**, since addition in $\mathbb{N}$ is commutative. So every pair is related to itself.

**Proof of symmetry.**

> Assume $(a,b) \sim (c,d)$, which by formula $(7)$ means $a + d = b + c$. We must show $(c,d)\sim(a,b)$, which by formula $(7)$ means $c + b = d + a$.
>
> Start from the assumption and rewrite each side using commutativity.
>
> $$c + b = b + c = a + d = d + a$$
>
> Reading that chain left to right, the first equality is commutativity, the second is the assumption read backwards, and the third is commutativity again. So $c + b = d + a$, which is what was needed.

**Proof of transitivity.**

> Assume both of the following.
>
> $$a + d = b + c \tag{8}$$ $$c + f = d + e \tag{9}$$
>
> The goal is to prove
>
> $$a + f = b + e. \tag{10}$$
>
> **Invented step, flagged.** Add equation $(8)$ and equation $(9)$ together, meaning add the two left sides to get one new left side and add the two right sides to get one new right side. This step is not forced by the previous line, and here is what it achieves. Equation $(8)$ mentions $a, b, c, d$ and equation $(9)$ mentions $c, d, e, f$. The goal mentions only $a, b, e, f$. So we need the letters $c$ and $d$ to leave. Adding the two equations puts $c$ and $d$ on both sides, and once a quantity sits on both sides, cancellation removes it. That is the whole plan.
>
> Adding gives
>
> $$(a + d) + (c + f) = (b + c) + (d + e). \tag{11}$$
>
> Now rearrange each side using **N1**, meaning associativity and commutativity of addition in $\mathbb{N}$. On the left, group $a$ with $f$ and group $c$ with $d$. On the right, group $b$ with $e$ and group $c$ with $d$.
>
> $$(a + f) + (c + d) = (b + e) + (c + d) \tag{12}$$
>
> Apply **N5**, cancellation in $\mathbb{N}$, with the cancelled quantity being $c + d$. That gives exactly
>
> $$a + f = b + e$$
>
> which is the goal $(10)$. $\blacksquare$

**Why this proof is the one to remember.**

Fact **N5**, cancellation, was used exactly once, and without it the transitivity part fails. Section 5.4 exhibits a small system where cancellation is false and where this exact proof collapses, and that example is the answer to the question of why $\mathbb{N}$ deserves this construction at all.

## The classes

Here are three classes written as explicit sets.

$$[(0,2)] = \{(0,2),\ (1,3),\ (2,4),\ (3,5),\ (4,6),\ \ldots\}$$ $$[(0,0)] = \{(0,0),\ (1,1),\ (2,2),\ (3,3),\ (4,4),\ \ldots\}$$ $$[(3,0)] = \{(3,0),\ (4,1),\ (5,2),\ (6,3),\ (7,4),\ \ldots\}$$

Every class is infinite in the up-and-right direction and has a first element on an axis: a pair with a zero in one coordinate.

## One standard name per class

{% callout_tip() %}
**Theorem 3.3.**

For every pair $(a,b)$ exactly one of the following three statements is true.

1. There is some $n \in \mathbb{N}$ with $n > 0$ such that $(a,b) \sim (n,0)$.
2. $(a,b) \sim (0,0)$.
3. There is some $n \in \mathbb{N}$ with $n > 0$ such that $(a,b) \sim (0,n)$.
{% end %}

**Proof, existence part:**

>  By **N6**, exactly one of $b < a$, $a = b$, $a < b$ holds. Take the  
  three cases in turn.

>  _Case $b < a$._ By the definition of order in **N6** there is some $n \in \mathbb{N}$ with $n > 0$ and $b + n = a$. Claim $(a,b)\sim(n,0)$. The test from formula $(7)$ asks whether $a + 0 = b + n$. The left side is $a$ by **N4**, and the right side is $a$ by the choice of $n$. So the test passes.

>  _Case $a = b$._ Claim $(a,b)\sim(0,0)$. The test asks whether $a + 0 = b + 0$, which reduces by **N4** to $a = b$, which is the case assumption. So the test passes.

>  _Case $a < b$._ There is some $n \in \mathbb{N}$ with $n > 0$ and $a + n = b$. Claim $(a,b)\sim(0,n)$. The test asks whether $a + n = b + 0$. The left side is $b$ by the choice of $n$, and the right side is $b$ by **N4**. So the test passes.

**Proof, uniqueness part:** 

>  Suppose two of the standard forms were related to each other.
>
>  - If $(n,0)\sim(m,0)$ then the test says $n + 0 = 0 + m$, so $n = m$ and the two forms are the same one.
>  - If $(n,0)\sim(0,m)$ then the test says $n + m = 0 + 0$, so $n + m = 0$. In $\mathbb{N}$ a sum of two naturals is zero only when both are zero, so $n = 0$ and $m = 0$. That contradicts the requirement $n > 0$ in statements 1 and 3.
>
>  So no pair satisfies two of the three statements. $\blacksquare$
>
**Worked Example:**

Take $(4,7)$. Since $4 < 7$ and $4 + 3 = 7$, case three applies with $n = 3$, so the standard name is $(0,3)$. Check directly with formula $(7)$. The test asks whether $4 + 3 = 7 + 0$, and both sides are $7$.

{% callout_note() %}
**Definition 3.4.**

The pair produced by Theorem 3.3 is called the **canonical representative** of the class. Its defining feature is that at least one of its two coordinates is zero.
{% end %}

The word **canonical** means official or standard, and here it means one form fixed in advance by a rule rather than chosen freshly each time. The exact code equivalent is normalization, such as reducing a fraction to lowest terms before comparing or hashing it.

## The definition of the integers

{% callout_note() %}
**Definition 3.5.**

The set of integers is the quotient set $$\mathbb{Z} \ = \ (\mathbb{N}\times\mathbb{N})/{\sim}.$$ An **integer** is one equivalence class, and the class of the pair $(a,b)$ is written $[(a,b)]$.
{% end %}

**Types**

The integer named $-2$ is not a pair. It is the set $\{(0,2),(1,3),(2,4),\ldots\}$, which is an infinite set of pairs of natural numbers. The pair $(0,2)$ is a member of that set and is not itself an integer.

1. $(3,5)$ is a pair, and $[(3,5)]$ is an integer.
2. Asking whether $(3,5)$ equals $-2$ is a type error.
3. The pair is a name written on the page, and the integer is the class that the name refers to.

|The integer|Its canonical representative|Three of its members|
|---|---|---|
|$-3$|$(0,3)$|$(0,3)$, $(1,4)$, $(2,5)$|
|$-1$|$(0,1)$|$(0,1)$, $(5,6)$, $(9,10)$|
|$0$|$(0,0)$|$(0,0)$, $(1,1)$, $(6,6)$|
|$2$|$(2,0)$|$(2,0)$, $(3,1)$, $(10,8)$|
|$5$|$(5,0)$|$(5,0)$, $(6,1)$, $(12,7)$|

Check one row. Is $(12,7)$ a member of the integer $5$? The canonical representative of $5$ is $(5,0)$, and the test asks whether $12 + 0 = 7 + 5$. Both sides are $12$, so yes.

---

# The mechanism

## Addition

**Step 1, propose a rule.**

$$[(a,b)] + [(c,d)] \ \stackrel{?}{=} \ [(a+c,\ b+d)] \tag{13}$$

I wrote a question mark above the equals sign because this is not yet a definition. It is a proposal, and a proposal becomes a definition only after the well-definedness check passes.

**Step 2, see why the check is needed, on numbers.**

The integer $-2$ can be named by $(0,2)$ or by $(4,6)$. The integer $5$ can be named by $(5,0)$ or by $(9,4)$.

- First naming. $(0,2) + (5,0) = (5,2)$.
- Second naming. $(4,6) + (9,4) = (13,10)$.

Test whether they are the same integer using formula $(7)$. The test asks whether $5 + 10 = 2 + 13$. Both sides are $15$, so both name the integer $3$.

**Step 3, the general proof.**

{% callout_tip() %}
**Theorem 4.1.**

If $(a,b)\sim(a',b')$ and $(c,d)\sim(c',d')$, then $(a+c,\ b+d) \sim (a'+c',\ b'+d')$.
{% end %}

**Proof.**

> The two assumptions, written out by formula $(7)$, are
>
> $$a + b' = b + a' \tag{14}$$ $$c + d' = d + c' \tag{15}$$
>
> The goal is
>
> $$(a+c) + (b'+d') = (b+d) + (a'+c'). \tag{16}$$
>
> **Invented step, flagged.** Add equation $(14)$ and equation $(15)$ together.
>
> $$(a + b') + (c + d') = (b + a') + (d + c'). \tag{17}$$
>
> Regroup both sides using **N1**. On the left, group $a$ with $c$ and group $b'$ with $d'$. On the right, group $b$ with $d$ and group $a'$ with $c'$.
>
> $$(a+c) + (b'+d') = (b+d) + (a'+c')$$
>
> That is exactly the goal $(16)$. $\blacksquare$

{% callout_note() %}
**Definition 4.2.**

Addition on $\mathbb{Z}$ is given by $$[(a,b)] + [(c,d)] \ = \ [(a+c,\ b+d)].$$
{% end %}

Note the three different jobs of the symbol $+$. The two $+$ signs on the right, inside the pair, are addition in $\mathbb{N}$. The $+$ sign on the left, between two classes, is the new operation being defined.

**Worked check.**

Compute $(-3) + 5$. Use $(0,3)$ and $(5,0)$.

$$[(0,3)] + [(5,0)] = [(5,3)]$$

Since $3 < 5$ and $3 + 2 = 5$, the canonical form is $(2,0)$, the integer $2$. Matches $-3 + 5 = 2$.

## Multiplication

**Motivation only.**

Using the intended reading, $(a-b)(c-d) = ac - ad - bc + bd = (ac + bd) - (ad + bc)$. So the product pair should be $(ac + bd,\ ad + bc)$.

That derivation used subtraction, so it proves nothing. It only tells which formula to write down. The formula itself mentions only multiplication and addition in $\mathbb{N}$.

**Check on numbers.**

Compute $(-2) \times 3$ with $(0,2)$ and $(3,0)$:

$$(0\cdot 3 + 2 \cdot 0,\ 0 \cdot 0 + 2 \cdot 3) = (0,\ 6)$$

which is $-6$. Compute $(-2)\times(-3)$ with $(0,2)$ and $(0,3)$:

$$(0 \cdot 0 + 2 \cdot 3,\ 0 \cdot 3 + 2 \cdot 0) = (6,\ 0)$$

which is $6$. A negative times a negative being positive is a consequence of the formula, not an extra assumption.

**Rename and recompute.**

Use $(4,6)$ for $-2$ and $(7,4)$ for $3$:

$$(4 \cdot 7 + 6 \cdot 4,\ 4 \cdot 4 + 6 \cdot 7) = (52,\ 58)$$

Test $(52,58) \sim (0,6)$: $52 + 6 = 58 + 0$. Both sides $58$.

{% callout_tip() %}
**Theorem 4.3, first half.**

If $(a,b)\sim(a',b')$, then for every pair $(c,d)$, $$(ac+bd,\ ad+bc) \ \sim \ (a'c+b'd,\ a'd+b'c).$$
{% end %}

**Proof.**

> The assumption is
>
> $$a + b' = b + a'. \tag{18}$$
>
> The goal is
>
> $$(ac+bd) + (a'd + b'c) \ = \ (ad+bc) + (a'c + b'd). \tag{19}$$
>
> **Invented step, flagged.** Multiply the assumed equation $(18)$ through by $c$, and separately by $d$. Multiplying both sides of a true equation by the same natural number keeps it true; expanding uses **N3**.
>
> $$ac + b'c = bc + a'c. \tag{20}$$
>
> $$ad + b'd = bd + a'd. \tag{21}$$
>
> Read $(21)$ backwards:
>
> $$bd + a'd = ad + b'd \tag{22}$$
>
> Add $(20)$ and $(22)$:
>
> $$(ac + b'c) + (bd + a'd) \ = \ (bc + a'c) + (ad + b'd) \tag{23}$$
>
> Regroup with **N1**:
>
> $$(ac + bd) + (a'd + b'c) \ = \ (ad + bc) + (a'c + b'd)$$
>
> That is the goal $(19)$. $\blacksquare$

{% callout_tip() %}
**Theorem 4.3, second half and conclusion.**

If $(a,b)\sim(a',b')$ and $(c,d)\sim(c',d')$, then $$(ac+bd,\ ad+bc) \ \sim \ (a'c'+b'd',\ a'd'+b'c').$$
{% end %}

**Proof.**

> The product formula is unchanged when the two input pairs swap places: swapping gives $(ca + db,\ cb + da)$, and by **N2** that is the same pair as $(ac + bd,\ ad + bc)$.
>
> Therefore the first half, applied with the roles exchanged, gives the second half: if $(c,d)\sim(c',d')$ then
>
> $$(a'c + b'd,\ a'd + b'c) \ \sim \ (a'c' + b'd',\ a'd' + b'c').$$
>
> Chain with the first half and close by transitivity (Theorem 3.2). $\blacksquare$

{% callout_note() %}
**Definition 4.4.**

Multiplication on $\mathbb{Z}$ is given by $$[(a,b)] \cdot [(c,d)] \ = \ [(ac + bd,\ ad + bc)].$$
{% end %}

**Why the split into two halves.**

If both inputs are renamed at once, the regrouping is hard to control. Renaming one input at a time keeps each half short. This one-slot-at-a-time pattern reappears in the construction of $\mathbb{Q}$ from $\mathbb{Z}$.

## The arithmetic laws

**Posture note.**

The laws form one family. Every member is proved by unfolding both sides with the definitions and applying the matching law in $\mathbb{N}$. Two members are proved in full; the rest are a table of one-line reductions.

{% callout_tip() %}
**Theorem 4.5.**

For all integers $x$, $y$, $z$, we have $x(y+z) = xy + xz$.
{% end %}

**Proof.**

> Write $x = [(a,b)]$, $y = [(c,d)]$, $z = [(e,f)]$. Unfold the left side.
>
> $$x(y+z) = [(a,b)] \cdot [(c+e,\ d+f)] = [(a(c+e) + b(d+f),\ \ a(d+f) + b(c+e))]$$
>
> Expand each coordinate using **N3**:
>
> $$= [(ac + ae + bd + bf,\ \ ad + af + bc + be)] \tag{24}$$
>
> Unfold the right side:
>
> $$xy + xz = [(ac+bd,\ ad+bc)] + [(ae+bf,\ af+be)] = [(ac+bd+ae+bf,\ \ ad+bc+af+be)] \tag{25}$$
>
> Compare $(24)$ and $(25)$. Each coordinate contains the same four products, in a different order, so the two pairs are equal by **N1**. Since the pairs are equal, their classes are equal. $\blacksquare$

This proof did not need the equivalence relation. The two pairs came out literally equal.

**Check on numbers.**

Take $x = -2$, $y = 5$, $z = -1$, using $(0,2)$, $(5,0)$, $(0,1)$. Then $y + z = [(5,1)]$, and $x(y+z) = [(2,10)]$, canonical form $(0,8)$, the integer $-8$. Separately $xy = [(0,10)]$ and $xz = [(2,0)]$, so $xy + xz = [(2,10)]$. Ordinary arithmetic: $-2 \times 4 = -8$ and $-10 + 2 = -8$.

{% callout_tip() %}
**Theorem 4.6.**

For every integer $x$ there is an integer $y$ with $x + y = 0_{\mathbb{Z}}$, where $0_{\mathbb{Z}} = [(0,0)]$.
{% end %}

**Proof.**

> Write $x = [(a,b)]$ and propose $y = [(b,a)]$, the class of the pair with coordinates swapped.
>
> $$[(a,b)] + [(b,a)] = [(a+b,\ b+a)]$$
>
> By **N1**, $b + a = a + b$, so the pair is $(a+b,\ a+b)$. Test whether that pair is in $[(0,0)]$: $(a+b) + 0 = (a+b) + 0$, which is true. So the sum is $0_{\mathbb{Z}}$. $\blacksquare$

**Check.**

For $x = 3$, use $(3,0)$. Then $y = [(0,3)]$, which is $-3$. The sum is $[(3,3)]$, in the class of $(0,0)$.

|Law in $\mathbb{Z}$|Statement|Reduces to|
|---|---|---|
|Addition is commutative|$x + y = y + x$|**N1** in each coordinate|
|Addition is associative|$(x+y)+z = x+(y+z)$|**N1** in each coordinate|
|Zero is an identity|$x + 0_{\mathbb{Z}} = x$|**N4**, since $[(a,b)] + [(0,0)] = [(a,b)]$|
|Multiplication is commutative|$xy = yx$|**N2**, swapping slots in the product formula|
|Multiplication is associative|$(xy)z = x(yz)$|**N1**, **N2**, **N3**, both sides expand to the same eight products|
|One is an identity|$x \cdot 1_{\mathbb{Z}} = x$|**N4**, with $1_{\mathbb{Z}} = [(1,0)]$|

Collecting Theorem 4.5, Theorem 4.6, and the table $\mathbb{Z}$ with the two operations is a commutative ring with unity.

## Subtraction, and the Integers delivered

{% callout_note() %}
**Definition 4.7.**

For an integer $x = [(a,b)]$, write $-x$ for the integer $[(b,a)]$, and write $y - x$ for $y + (-x)$.
{% end %}

The minus sign now exists as a defined operation rather than an assumption.

{% callout_tip() %}
**Theorem 4.8.**

For all integers $u$ and $v$, the equation $u + x = v$ has exactly one solution $x$ in $\mathbb{Z}$.
{% end %}

**Proof, existence.**

> Take $x = v + (-u)$. Then $$u + x = u + (v + (-u)) = (u + (-u)) + v = 0_{\mathbb{Z}} + v = v,$$ using associativity, commutativity, Theorem 4.6, and the zero identity.

**Proof, uniqueness.**

> Suppose $u + x = v$ and $u + x' = v$. Then $u + x = u + x'$. Add $-u$ to both sides and regroup: $x = x'$. $\blacksquare$

**The original breakage, revisited.**

Section 1.1 proved that $8 + x = 5$ has no solution in $\mathbb{N}$. Solve it in $\mathbb{Z}$. Write $u = [(8,0)]$ and $v = [(5,0)]$. Then $-u = [(0,8)]$, so

$$x = v + (-u) = [(5,0)] + [(0,8)] = [(5,8)].$$

By Theorem 3.3 the canonical form of $(5,8)$ is $(0,3)$, since $5 < 8$ and $5 + 3 = 8$. So $x$ is the integer $-3$.

Verify: $[(8,0)] + [(0,3)] = [(8,3)]$, and $(8,3) \sim (5,0)$ because $8 + 0 = 3 + 5$. Both sides are $8$.

That is the repair, delivered and verified.

## Cancellation in $\mathbb{Z}$, and the absence of zero divisors

{% callout_tip() %}
**Theorem 4.9, cancellation for addition in $\mathbb{Z}$.**

If $x + z = y + z$ then $x = y$.
{% end %}

**Proof.**

> Add $-z$ to both sides and regroup. The left becomes $x + (z + (-z)) = x + 0_{\mathbb{Z}} = x$, and the right becomes $y$. $\blacksquare$

In $\mathbb{N}$ cancellation required induction. In $\mathbb{Z}$ it follows in two lines from inverses.

{% callout_tip() %}
**Theorem 4.10, no zero divisors.**

If $x \cdot y = 0_{\mathbb{Z}}$ then $x = 0_{\mathbb{Z}}$ or $y = 0_{\mathbb{Z}}$.
{% end %}

**Proof.**

> Suppose $x \neq 0_{\mathbb{Z}}$ and $y \neq 0_{\mathbb{Z}}$. By Theorem 3.3 each has a canonical representative with a non-zero natural in one coordinate and zero in the other. Four cases, computed with Definition 4.4:
>
> |Canonical form of $x$|Canonical form of $y$|Product pair|Result|
> |---|---|---|---|
> |$(m,0)$|$(n,0)$|$(mn, 0)$|non-zero|
> |$(m,0)$|$(0,n)$|$(0, mn)$|non-zero|
> |$(0,m)$|$(n,0)$|$(0, mn)$|non-zero|
> |$(0,m)$|$(0,n)$|$(mn, 0)$|non-zero|
>
> In every case $mn > 0$ when $m > 0$ and $n > 0$. A pair $(mn, 0)$ or $(0, mn)$ with $mn > 0$ is not in the class of $(0,0)$. That proves the contrapositive. $\blacksquare$

**Check.**

$x = -2$, $y = 3$: product pair $(0, 6)$, the integer $-6$, not zero.

So $\mathbb{Z}$ is an integral domain.

## Order

{% callout_note() %}
**Definition 4.11.**

For integers $[(a,b)]$ and $[(c,d)]$, define $$[(a,b)] \ \le \ [(c,d)] \quad \text{exactly when} \quad a + d \ \le \ b + c \ \text{ in } \mathbb{N}.$$
{% end %}

**Motivation only.**

Wish $a - b \le c - d$. Adding $b$ and $d$ to both sides turns it into $a + d \le b + c$.

**Check.**

Is $-3 \le 2$? Use $(0,3)$ and $(2,0)$: $0 + 0 \le 3 + 2$, so $0 \le 5$, true. Is $2 \le -3$? $2 + 3 \le 0 + 0$, so $5 \le 0$, false.

{% callout_tip() %}
**Theorem 4.12.**

The relation in Definition 4.11 is well-defined.
{% end %}

**Proof.**

> Assume
>
> $$a + b' = b + a' \tag{26}$$ $$c + d' = d + c' \tag{27}$$ $$a + d \ \le \ b + c \tag{28}$$
>
> By **N6**, $(28)$ means there is some $k \in \mathbb{N}$ with
>
> $$a + d + k = b + c. \tag{29}$$
>
> **Invented step, flagged.** Add $b' + d'$ to both sides of $(29)$.
>
> $$a + d + k + b' + d' \ = \ b + c + b' + d' \tag{30}$$
>
> Regroup and apply $(26)$ and $(27)$ to trade unprimed letters for primed ones, then regroup again:
>
> $$(b + d) + (a' + d' + k) \ = \ (b + d) + (c' + b') \tag{31}$$
>
> Apply **N5** with cancelled quantity $b + d$:
>
> $$a' + d' + k \ = \ b' + c'$$
>
> which is $a' + d' \le b' + c'$. $\blacksquare$

**Order properties.**

1. **Trichotomy.** Exactly one of $x < y$, $x = y$, $x > y$ holds (**N6** on $a+d$ and $b+c$).
2. **Compatible with addition.** If $x \le y$ then $x + z \le y + z$.
3. **Compatible with multiplication by a non-negative integer.** If $x \le y$ and $0_{\mathbb{Z}} \le z$ then $xz \le yz$.

Call $x$ positive when $0_{\mathbb{Z}} < x$, and negative when $x < 0_{\mathbb{Z}}$. Theorem 3.3's three canonical forms are exactly positive, zero, and negative.

## The copy of $\mathbb{N}$ that lives inside $\mathbb{Z}$

{% callout_note() %}
**Definition 4.13.**

Define $\iota : \mathbb{N} \to \mathbb{Z}$ by $\iota(n) = [(n,0)]$.
{% end %}

{% callout_tip() %}
**Theorem 4.14.**

The function $\iota$ is injective, and for all $m, n \in \mathbb{N}$:

1. $\iota(m+n) = \iota(m) + \iota(n)$
2. $\iota(mn) = \iota(m)\cdot\iota(n)$
3. $m \le n$ in $\mathbb{N}$ iff $\iota(m) \le \iota(n)$ in $\mathbb{Z}$
4. $\iota(0) = 0_{\mathbb{Z}}$ and $\iota(1) = 1_{\mathbb{Z}}$
{% end %}

**Proof of injectivity.**

> $\iota(m) = \iota(n)$ means $(m,0) \sim (n,0)$, so $m + 0 = 0 + n$, hence $m = n$ by **N4**.
>
> **Item 1.** $\iota(m) + \iota(n) = [(m+n,\ 0)] = \iota(m+n)$.
>
> **Item 2.** $\iota(m)\cdot\iota(n) = [(mn,\ 0)] = \iota(mn)$.
>
> **Item 3.** $\iota(m) \le \iota(n)$ asks whether $m + 0 \le 0 + n$, i.e. $m \le n$.
>
> **Item 4.** Immediate from the definitions. $\blacksquare$

**Statement about subsets.**

Literally, after this construction, $\mathbb{N} \subseteq \mathbb{Z}$ is false. The natural number $3$ and the integer $\iota(3)$ are different objects.

What is true:

1. The image $\iota(\mathbb{N})$ is a subset of $\mathbb{Z}$.
2. $\iota$ is injective, so the image is a faithful copy.
3. The copy has the same arithmetic and order as the original.

Mathematicians therefore stop writing $\iota$ and write $3$ for $\iota(3)$. That renaming is justified by Theorem 4.14. Once adopted, $\mathbb{N}\subseteq\mathbb{Z}$ is legitimate shorthand.

**Note on the other convention.**

If $\mathbb{N}$ starts at $1$, the embedding is $\iota(n) = [(n+1, 1)]$ with $0_{\mathbb{Z}} = [(1,1)]$. Structure of every proof is unchanged.

## Summary

1. $\mathbb{Z}$ is the set of equivalence classes of pairs of natural numbers under $a + d = b + c$.
2. $\mathbb{Z}$ with addition and multiplication is a commutative ring with unity.
3. $\mathbb{Z}$ has no zero divisors, so it is an integral domain.
4. $\mathbb{Z}$ carries a total order compatible with the operations.
5. Every equation $u + x = v$ has exactly one solution (the repair).
6. $\mathbb{Z}$ contains a faithful copy of $\mathbb{N}$.
7. No new assumption was made. Every property was derived from the six imported facts about $\mathbb{N}$.

---

# Meaning

## Exactly what broke, exactly what the integers preserve, exactly what it costs

**What broke.**

Addition on $\mathbb{N}$ never decreases anything, so $a + x = b$ is solvable exactly when $a \le b$. The failure is that one operation was not invertible.

**What the repair preserves.**

1. All the arithmetic laws.
2. The order, still total.
3. The old system inside the new one without distortion.

**What the repair costs.**

1. **Well-ordering is lost.** Every non-empty subset of $\mathbb{N}$ has a least element. In $\mathbb{Z}$ the set of negative integers has no least element. Proofs that use well-ordering cannot move from $\mathbb{N}$ to $\mathbb{Z}$ unchanged; they usually restrict to non-negative integers.
2. **Elements stopped being simple objects.** In $\mathbb{Z}$ each element is an infinite set of pairs, so every statement about an integer must be checked for independence from the representative.

## What an integer does not depend on

**A rule that fails.**

"The first coordinate of an integer is the first coordinate of any representative." For $-2$: $(0,2)$ gives representative $0$, $(1,3)$ gives representative $1$. Different answers, so the rule defines nothing.

**A rule that works.**

"The sign of an integer is read off its canonical representative." Theorem 3.3 gives uniqueness, so one answer per integer.

**The general statement.**

An integer determines its class and nothing more. Any quantity computed from a representative is a property of the integer only when unchanged by every legal renaming.



## Where the construction fails, worked on a two-element example

Let $B = \{0, 1\}$ with Boolean OR $\vee$. Operation table: $0 \vee 0 = 0$, $0 \vee 1 = 1$, $1 \vee 0 = 1$, $1 \vee 1 = 1$. This is a commutative monoid with identity $0$.

**Cancellation fails.**

$1 \vee 1 = 1 \vee 0$ while $1 \neq 0$.

**Run the construction.**

Define $(s,t) \sim (u,v)$ when $s \vee v = t \vee u$.

1. $(1,0) \sim (1,1)$? $1 \vee 1 = 0 \vee 1$: both $1$, yes.
2. $(1,1) \sim (0,0)$? $1 \vee 0 = 1 \vee 0$: both $1$, yes.
3. $(1,0) \sim (0,0)$? $1 \vee 0 = 0 \vee 0$: $1 \neq 0$, no.

Items 1 and 2 plus transitivity would force item 3, which is false. So $\sim$ is not transitive.

**Trace.**

Transitivity in Theorem 3.2 used **N5** once, at the move from $(12)$ to the conclusion. Cancellation is false in $B$, so that line is unavailable.

**General repair.**

For an arbitrary commutative monoid, declare $(s,t) \sim (u,v)$ when there exists $r$ with $s + v + r = t + u + r$. That makes the relation transitive; the result is the Grothendieck group.

**Price on $B$.**

With the extra clause, $(1,0) \sim (0,0)$ via $r = 1$. In fact every pair becomes equivalent to every other, so the group has one element. The construction succeeded and produced nothing.

**The general fact.**

The map from a commutative monoid into its Grothendieck group is injective exactly when the monoid satisfies cancellation. $\mathbb{N}$ deserves this construction because it satisfies cancellation, so formula $(7)$ is already transitive and the copy of $\mathbb{N}$ inside $\mathbb{Z}$ is faithful.

## Equivalent versus equal

1. The pairs $(0,2)$ and $(1,3)$ are **equivalent**.
2. The integers $[(0,2)]$ and $[(1,3)]$ are **equal**.

Both true, not the same sentence. Equivalence is a relation between two distinct pairs. Equality after quotienting is what equivalence becomes once you work with classes. If a sentence has brackets on both sides, the verb is _equals_. If no brackets, the verb is _is equivalent to_. Writing $(0,2) = (1,3)$ is false. Writing $[(0,2)] \sim [(1,3)]$ is a type error.

## Why not simply attach a sign to each natural number

**Competing construction.**

An integer is a sign and a natural number, $\{+, -\} \times \mathbb{N}$, with $+0$ and $-0$ identified. Addition and multiplication are defined by cases on signs.

**It works.**

It produces a correct copy of the integers and is closer to how machines store integers.

**What it costs.**

Addition is defined by cases. Every subsequent proof, including associativity, runs through those cases; a three-term sum multiplies the case count again.

**Comparison.**

The pair construction pays well-definedness once up front; then every law is a short computation with no cases. Look at the distributivity proof: no case split, because negatives are not a separate kind of object. The sign construction pays nothing up front and then pays repeatedly in every proof forever.

**Transferable lesson.**

Choosing a representation that removes case splits from later proofs is worth an initial cost—the same trade as choosing a data representation that makes invariants automatic.

## Why this relation and not a different one

Formula $(7)$ is the unique addition-only restatement of the intended condition $a - b = c - d$: add $b$ and $d$ to both sides.

**Two wrong alternatives.**

1. Try $a + c = b + d$. On $(8,5)$ and $(11,8)$, which should be equivalent: $8 + 11 = 5 + 8$ fails. Incorrect.
2. Try $a + b = c + d$. This is an equivalence relation, but merges $(8,5)$ with $(5,8)$, i.e. every integer with its negative. Being an equivalence relation is necessary and not sufficient.
