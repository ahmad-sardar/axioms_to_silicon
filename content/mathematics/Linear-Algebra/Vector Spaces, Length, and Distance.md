+++
title = "Vector Spaces, Length, and Distance"
slug = "Vector Spaces, Length, and Distance"
toc = true
+++

These notes build the math of measuring in a flat space. We start with what a vector space is. Then we look at coordinate systems in a picture-first way, so you have a concrete image of axes and a grid. Then we make everything exact: linear combinations, span, independence, basis, length, angle, distance. We prove the main facts and work through examples that climb from easy to a real machine learning case.


# Vector Space

## What problem it solves

Many different things behave the same way under two operations: you can add two of them, and you can scale one by a number. Arrows in the plane do this. Lists of numbers do this. Whole functions do this. Instead of proving facts again for each kind, we write down the shared rules once. Then any fact we prove holds for all of them at once.

## Definition

A vector space over a field $F$ is a set $V$ with two operations, vector addition $+ : V \times V \to V$ and scalar multiplication $\cdot : F \times V \to V$, satisfying the eight axioms below. A vector is any element of $V$.

A field $F$ is a set with addition, subtraction, multiplication, and division by any nonzero element, all behaving in the usual way; the real numbers $\mathbb{R}$ and the complex numbers $\mathbb{C}$ are fields. For these notes $F = \mathbb{R}$.

Vectors are the elements of $V$. Scalars are the elements of $F$. You may add a vector to a vector, and multiply a scalar by a vector. Adding a vector to a scalar is not defined.

The eight axioms, for all $u, v, w \in V$ and all $a, b \in F$:

- A1. $u + v = v + u$.
- A2. $(u + v) + w = u + (v + w)$.
- A3. There exists $\mathbf{0} \in V$ with $v + \mathbf{0} = v$ for all $v$.
- A4. For each $v$ there exists $-v \in V$ with $v + (-v) = \mathbf{0}$.
- A5. $a(u + v) = au + av$.
- A6. $(a + b)v = av + bv$.
- A7. $a(bv) = (ab)v$.
- A8. $1 \cdot v = v$.

Subtraction is defined from A4: $u - v := u + (-v)$.

## How addition is computed

The axioms state what addition must satisfy. How it is computed depends on the space. In $\mathbb{R}^n$, addition is componentwise:

$$ (u_1, \dots, u_n) + (v_1, \dots, v_n) = (u_1 + v_1, \dots, u_n + v_n). $$

Example: $(3, 0) + (0, 4) = (3, 4)$. $\mathbb{R}^n$ satisfies the eight axioms because each component is a real number, and $\mathbb{R}$ satisfies them.

## How a vector looks, small and large

In low dimension, a vector in $\mathbb{R}^n$ is a list of $n$ real numbers, like $(3, 4)$.

In high dimension, a vector in $\mathbb{R}^{784}$ is a list of 784 real numbers. A 28 by 28 gray image is one such vector; each pixel brightness is one entry.

A function $f : \mathbb{R} \to \mathbb{R}$ is also a vector, in the space of all such functions, with $(f + g)(x) = f(x) + g(x)$ and $(af)(x) = a \cdot f(x)$. A function is like a vector with one entry for each input point, so infinitely many entries.

## Two theorems from the axioms

**Theorem (the zero vector is unique).** Suppose $\mathbf{0}$ and $\mathbf{0}'$ both satisfy A3. Then $$ \mathbf{0}' = \mathbf{0}' + \mathbf{0} = \mathbf{0} + \mathbf{0}' = \mathbf{0}, $$ using A3 with $\mathbf{0}$, then A1, then A3 with $\mathbf{0}'$. So $\mathbf{0}' = \mathbf{0}$.

**Theorem ($0 \cdot v = \mathbf{0}$ for every $v$).** From $0 + 0 = 0$ in $\mathbb{R}$ and A6, $0 \cdot v = (0 + 0)v = 0 \cdot v + 0 \cdot v$. Add $-(0 \cdot v)$ to both sides (A4) and regroup (A2): $\mathbf{0} = 0 \cdot v$.

## Where it came from

The geometric ideas came first. Hamilton and Grassmann worked on directed quantities in the 1840s. Matrix and determinant work followed later in the 1800s. The eight-axiom definition came last, from Peano in 1888. Examples came first; the abstract axioms came last.

# Coordinate Systems, the Picture First

Before the exact chain of definitions, here is the picture to carry. It makes the rest concrete.

## Axes and a grid

Pick a point to be the center, the origin. Draw direction arrows out from it; these are the axes. To name any point, say how far you go along each axis. Those numbers are its coordinates.

In the plane, the usual setup has two axes, one pointing right and one pointing up. The point "3 right and 4 up" has coordinates $(3, 4)$. The axes draw a grid over the plane, like graph paper, and each point sits at a grid location given by its coordinates.

So a coordinate system is two choices: where the origin is, and which way the axes point and how long one step along each axis is. Once these are fixed, every point has a name.

## The clean grid: Cartesian

The nicest grid has axes perpendicular to each other, and one step on each axis equal to one unit of distance. This is a Cartesian coordinate system: the square graph paper you know, right angles and even spacing. In it, distance follows the Pythagorean rule. We make this exact later.

A grid need not be Cartesian. Axes can be non-perpendicular, or have uneven steps. You still get a valid naming of points, but the distance rule is messier.

## The picture to keep

The point is a fixed place. Its coordinates are its address in the grid you chose. Change the grid (move the origin, turn the axes, change the step size) and the address changes, but the point does not move.

# Linear Combination

## Definition

Given vectors $v_1, \dots, v_n \in V$ and scalars $a_1, \dots, a_n \in F$, a linear combination is

$$ a_1 v_1 + a_2 v_2 + \dots + a_n v_n. $$

The scalars are the coefficients. It uses only the two operations of the space, and the result is again a vector in $V$. A linear combination is a finite sum.

The vectors are fixed building blocks. The coefficients are the numbers in front, which you choose or solve for.

## Examples

Worked: $3 \cdot (1,0) + 4 \cdot (0,1) = (3,0) + (0,4) = (3,4)$.

Worked, other coefficients: $-2 \cdot (1,0) + 5 \cdot (0,1) = (-2, 5)$.

Edge case: all coefficients zero gives the zero vector, $0 \cdot v_1 + \dots + 0 \cdot v_n = \mathbf{0}$ (the trivial combination). One coefficient one and the rest zero gives that single vector back.

Functions: $a_1 f_1 + a_2 f_2$ is itself a function. For $f_1(x) = x^2$, $f_2(x) = 3x$, the combination $1 \cdot f_1 + 1 \cdot f_2$ is the function $x^2 + 3x$.

# Span

## Definition

The span of $v_1, \dots, v_n$ is the set of all their linear combinations:

$$ \operatorname{span}(v_1, \dots, v_n) = \{ a_1 v_1 + \dots + a_n v_n : a_1, \dots, a_n \in F \}. $$

To test whether $w$ is in the span, ask whether there exist coefficients with $a_1 v_1 + \dots + a_n v_n = w$. This is a linear system; if it has a solution, $w$ is in the span.

A span always contains $\mathbf{0}$ and is closed under addition and scaling, so it is itself a vector space inside $V$ (a subspace). It always passes through the origin.

## Examples

Worked: $\operatorname{span}((1,0)) = \{(a, 0) : a \in \mathbb{R}\}$, the horizontal line through the origin.

Worked: $\operatorname{span}((1,0), (0,1)) = \mathbb{R}^2$, since any $(a,b) = a(1,0) + b(0,1)$.

Worked, functions: $\operatorname{span}(1, x, x^2)$ is all polynomials of degree at most 2, since each such polynomial is $a + bx + cx^2$.

Counterexample: $(1,0)$ alone does not span $\mathbb{R}^2$; $(0,1)$ is not in $\operatorname{span}((1,0))$, because no $a$ gives $(a,0) = (0,1)$.

# Linear Independence

## Definition

Vectors $v_1, \dots, v_n$ are linearly independent if

$$ a_1 v_1 + \dots + a_n v_n = \mathbf{0} \implies a_1 = \dots = a_n = 0. $$

If some choice of coefficients, not all zero, gives $\mathbf{0}$, the vectors are linearly dependent.

To test: set the combination equal to $\mathbf{0}$, write it component by component, and solve. Only the all-zero solution means independent; any nonzero solution means dependent, and that solution exhibits the dependence.

## Examples

Worked, independent: $a(1,0) + b(0,1) = (0,0)$ forces $a = 0$, $b = 0$. Independent.

Worked, dependent: $a(1,0) + b(0,1) + c(1,1) = (0,0)$ gives $a + c = 0$, $b + c = 0$. Take $c = 1$: then $a = -1$, $b = -1$, not all zero. Dependent, and the relation is $(1,1) = (1,0) + (0,1)$.

Faded: are $(1,2)$ and $(2,4)$ independent? Since $(2,4) = 2(1,2)$, they are dependent. (Two vectors are dependent exactly when one is a scalar multiple of the other.)

Counterexample/edge: any set containing $\mathbf{0}$ is dependent, because $1 \cdot \mathbf{0} = \mathbf{0}$ uses a nonzero coefficient. A single nonzero vector is independent.

# Basis and Orthonormal Basis

## Basis

A set $\{v_1, \dots, v_n\}$ is a basis of $V$ if it spans $V$ and is linearly independent. Both conditions hold at once.

A space has many bases. For $\mathbb{R}^2$: the standard basis $(1,0), (0,1)$; the diagonal basis $(1,1), (1,-1)$; the stretched basis $(2,0), (0,3)$. All are bases. A basis is about the number of vectors, not their length.

## Orthonormal basis

The cleanest kind of basis is orthonormal. Its definition uses two ideas from measuring, perpendicular and length, which are defined in full in the inner product and norm sections below. Stated with the inner product $\langle \cdot, \cdot \rangle$:

A basis $\{e_1, \dots, e_n\}$ is orthonormal if

$$ \langle e_i, e_j \rangle = \begin{cases} 1 & i = j \\ 0 & i \ne j. \end{cases} $$

That is, the basis vectors are pairwise orthogonal ($\langle e_i, e_j \rangle = 0$ for $i \ne j$) and each has unit length ($\langle e_i, e_i \rangle = 1$). This is the basis behind every Cartesian grid: perpendicular axes, each one unit long.

Orthogonal means pairwise perpendicular. Orthonormal means orthogonal and unit length. The diagonal basis $(1,1), (1,-1)$ is orthogonal but not orthonormal, since each has length $\sqrt{2}$; dividing each by $\sqrt 2$ makes it orthonormal.

The key property of an orthonormal basis (proved in the inner product section): the coordinates of a vector are its inner products with the basis vectors, $c_i = \langle v, e_i \rangle$, with no system to solve. The standard basis is orthonormal, which is why it was always the easy one.

## Examples

Worked, is a basis: $\{(1,0),(0,1)\}$ spans $\mathbb{R}^2$ and is independent.

Worked, is a basis: $\{(1,1),(1,-1)\}$ spans ($a(1,1)+b(1,-1)=(p,q)$ solves as $a=(p+q)/2$, $b=(p-q)/2$) and is independent.

Counterexample: $\{(1,0),(0,1),(1,1)\}$ spans $\mathbb{R}^2$ but is dependent, so it is not a basis (too many). $\{(1,0)\}$ is independent but does not span, so not a basis (too few).

Orthonormal check: $\{(1,0),(0,1)\}$ is orthonormal; $\{(2,0),(0,1)\}$ is orthogonal but not orthonormal, since $\Vert(2,0)\Vert = 2 \ne 1$.

# Dimension

## Definition

The dimension of $V$, written $\dim V$, is the number of vectors in a basis of $V$. This is well defined because of the theorem below.

**Theorem (invariance of dimension).** If $V$ has a basis of $n$ vectors, every basis of $V$ has exactly $n$ vectors.

This rests on a lemma: if one set spans $V$ and another set is linearly independent, the independent set has at most as many vectors as the spanning set (independent $\le$ spanning).

Proof of the theorem from the lemma: let $B$ ($n$ vectors) and $C$ ($m$ vectors) both be bases. $B$ spans and $C$ is independent, so $m \le n$. $C$ spans and $B$ is independent, so $n \le m$. Hence $n = m$.

Proof idea of the lemma: feed the independent vectors in one at a time; each replaces one vector of the spanning set while the set still spans. If there were more independent vectors than spanning vectors, you would run out of vectors to replace, a contradiction.

## Examples

Worked: $\dim \mathbb{R}^2 = 2$, $\dim \mathbb{R}^n = n$, $\dim \mathbb{R}^{784} = 784$.

Worked: polynomials of degree at most 3 have basis $\{1, x, x^2, x^3\}$, so dimension 4. Degree at most $n$ gives dimension $n + 1$.

Edge case: the space ${\mathbf{0}}$ has dimension 0 (empty basis).

Counterexample to a common error: a nontrivial space has infinitely many vectors (points), but its dimension is the finite basis count. "Polynomials are functions, so the dimension is infinite" is false: degree at most 3 polynomials have 4 free coefficients, so dimension 4. Being a function does not force infinite dimension; infinitely many free coefficients does.

# Subspace

## Definition

A subset $W \subseteq V$ is a subspace of $V$ if $W$ is itself a vector space under the same two operations. Equivalently, $W$ is a subspace if it satisfies these axioms:

- $\mathbf{0} \in W$,
- $u, v \in W \implies u + v \in W$ (closed under addition),
- $u \in W$, $a \in F \implies au \in W$ (closed under scaling).

The other vector space axioms are inherited from $V$.

Every subspace contains $\mathbf{0}$: a subspace is closed under scaling, and scaling any $u \in W$ by $0$ gives $0 \cdot u = \mathbf{0}$, which is therefore in $W$. So a flat that misses the origin is never a subspace.

## Examples

Worked, is a subspace: $W = \{(t, t) : t \in \mathbb{R}\}$, the diagonal. It contains $(0,0)$, and adding or scaling vectors of the form $(t,t)$ stays of that form.

Counterexample: $W = \{(t, t+1) : t \in \mathbb{R}\}$, a shifted line, is not a subspace; $(0,0)$ is not in it, since $t = 0$ and $t + 1 = 0$ cannot both hold.

Edge cases: ${\mathbf{0}}$ and $V$ itself are always subspaces.

Geometric view: in $\mathbb{R}^2$ the subspaces are the origin, every line through the origin, and the whole plane. A subspace is a flat through the origin.

# The Coordinate System, Made Exact

Earlier we drew the picture of axes and a grid. Here is the exact definition.

## Definition

A coordinate system on a vector space $V$ is an origin (a chosen point assigned coordinates $(0, \dots, 0)$) together with a basis $\{b_1, \dots, b_n\}$ of $V$. The coordinates of a point $p$ are the unique coefficients $(c_1, \dots, c_n)$ with

$$ p - (\text{origin}) = c_1 b_1 + \dots + c_n b_n. $$

The coordinates are unique: the basis spans, so at least one such tuple exists; the basis is independent, so at most one does.

**Theorem (uniqueness of coordinates).** Fix a basis. If $v = \sum_i a_i b_i = \sum_i c_i b_i$, then subtracting gives $\sum_i (a_i - c_i) b_i = \mathbf{0}$, and independence forces $a_i - c_i = 0$ for all $i$, so $a_i = c_i$. The tuple is unique.

## Cartesian coordinate system

A Cartesian coordinate system is a coordinate system whose basis is orthonormal and whose origin is fixed: the axes are pairwise orthogonal and each has unit length. This is the exact form of the square, even grid. In a Cartesian system on a flat space, the distance between two points equals the Pythagorean formula in the coordinates, $$ d(p, q) = \sqrt{(p_1 - q_1)^2 + \dots + (p_n - q_n)^2}. $$

Where the dimensions live. The number of perpendicular axes is the dimension. The plane $\mathbb{R}^2$ has two perpendicular axes. Ordinary space $\mathbb{R}^3$ has three: right, up, and forward, all at right angles, the space we live in. $\mathbb{R}^4$ has four mutually perpendicular axes; you cannot picture the fourth, but the math is identical, and the same Pythagorean distance formula applies with four terms under the square root. In machine learning, $\mathbb{R}^{784}$ (a small image) has 784 perpendicular pixel-axes. The picture stops at three, but the formula does not; the only thing that grows is the number of terms in the sum. Each new dimension is one more direction perpendicular to all the others.

What "straight" means here. In a Cartesian system, "straight" means the axes are straight lines and the grid lines never bend or bunch up. One step along an axis covers the same real distance everywhere on that axis. The grid spacing is uniform: a unit square near the origin is the same size as a unit square far away. This uniform, never-bending grid is what lets one coordinate system cover the whole space and makes the Pythagorean distance formula hold everywhere. The next section says what happens when this fails.

## Examples

Worked: the point $(3,2)$ in the standard basis $(1,0),(0,1)$ has coordinates $(3,2)$.

Worked: the same point $(3,2)$ in the diagonal basis $(1,1),(1,-1)$. Solve $a(1,1)+b(1,-1)=(3,2)$: $a+b=3$, $a-b=2$, so $a=2.5$, $b=0.5$. Coordinates $(2.5, 0.5)$. Same point, different coordinates, because the axes changed.

Non-Cartesian example: the basis $(1,0),(1,1)$ gives a valid coordinate system, but it is not Cartesian (the vectors are not orthogonal: $\langle (1,0),(1,1)\rangle = 1 \ne 0$), so the plain Pythagorean distance formula does not apply in those coordinates.

# Flat Space

Cartesian coordinates name the grid; flatness is the property of the space that lets one such grid cover it everywhere.

## Definition

A space is flat if it admits one global, undistorted Cartesian coordinate system in which the distance between any two points $P, Q$ is

$$ d(P, Q)^2 = (x_1 - y_1)^2 + \dots + (x_n - y_n)^2, $$

where $(x_i)$ and $(y_i)$ are the coordinates of $P$ and $Q$, and the grid is uniform everywhere (one coordinate-unit equals one distance-unit at every point and in every direction).

From this definition the Pythagorean distance formula holds everywhere, as a consequence.

## Examples

A plane is flat: the usual axes give a global undistorted Cartesian grid, and distance is $\sqrt{(x_1-y_1)^2 + (x_2-y_2)^2}$ everywhere.

A sphere is not flat: no single undistorted Cartesian grid covers it. Every flat map of the Earth distorts areas or angles. A right triangle on a sphere does not satisfy the Pythagorean relation, because the surface curves.

## What flat means, compared to curved spaces

"Flat" is easiest to understand by what it is not. In a flat space, "straight" lines stay straight and parallel lines stay the same distance apart forever. The angles of a triangle add up to exactly 180 degrees. The Pythagorean formula holds everywhere. $\mathbb{R}^2$, $\mathbb{R}^3$, and every $\mathbb{R}^n$ with the dot product are flat in this sense.

A curved space breaks these. On a curved surface, the shortest path between two points is not a straight line in the usual sense but a curved one called a geodesic, the straightest path the surface allows. Parallel lines can meet or spread apart. Triangle angles do not add to 180 degrees. The Pythagorean formula fails, except in an infinitely small patch.

A few named spaces, for curiosity:

- The sphere (positive curvature). The surface of a ball. Triangle angles add to more than 180 degrees. Two paths heading "straight north" meet at the pole, even though they started parallel. This is the geometry of the Earth's surface and of navigation.
- The hyperbolic plane, or saddle (negative curvature). Shaped like a saddle or a Pringle. Triangle angles add to less than 180 degrees. Parallel lines spread apart. This geometry shows up in special relativity and in some models of networks.
- The cylinder. Interesting case: it looks curved, but it is actually flat. You can unroll it into a flat sheet without stretching, so its internal distances obey the Pythagorean formula. Curvature is about stretching, not about looking bent. This is why "flat" is defined by measurement inside the space, not by how it looks from outside.
- Spacetime (varying curvature). In general relativity, gravity is the curvature of four-dimensional spacetime. Mass bends it, and the bending is what we feel as gravity. The measuring rule changes from point to point.

The tool that records curvature at each point is the metric tensor, and these notes do not build it. The point for now: flat space, where we work, is the simplest case, the one where a single Cartesian grid covers everything and the Pythagorean formula never fails. Curved spaces are the general case, and they need heavier machinery.

The deeper equivalent definition of flat, stated for completeness: a Riemannian manifold is flat if its Riemann curvature tensor is zero everywhere, where the curvature tensor is built from the derivatives of the metric tensor. The existence of a global Cartesian coordinate system is equivalent to vanishing curvature.

# Inner Product

## What problem it solves

A vector space has addition and scaling but no length, angle, or distance. The inner product is one operation that adds length and angle.

## Definition

An inner product on a real vector space $V$ is a map $\langle \cdot, \cdot \rangle : V \times V \to \mathbb{R}$ satisfying, for all $u, v, w \in V$ and $a, b \in \mathbb{R}$:

- P1 (symmetry): $\langle u, v \rangle = \langle v, u \rangle$.
- P2 (linearity in the first argument): $\langle au + bw, v \rangle = a\langle u, v \rangle + b\langle w, v \rangle$.
- P3 (positive-definiteness): $\langle v, v \rangle \ge 0$, with equality if and only if $v = \mathbf{0}$.

By symmetry, linearity holds in the second argument too. P3 makes $\langle v, v \rangle \ge 0$, which permits the square root used to define length.

## The dot product

In $\mathbb{R}^n$ the standard inner product is the dot product:

$$ \langle u, v \rangle = u_1 v_1 + u_2 v_2 + \dots + u_n v_n. $$

It satisfies the three axioms: symmetry from commutativity of multiplication; linearity term by term; positive-definiteness since $\langle v, v \rangle = v_1^2 + \dots + v_n^2 \ge 0$, zero only when every $v_i = 0$.

## Why multiply matching components, then add

The product of two numbers measures agreement: positive if same sign, negative if opposite, zero if one is zero, larger when both are large. So $u_i v_i$ measures whether the two vectors agree in direction $i$. Matching positions are used because comparing position $i$ of one with position $j \ne i$ of the other compares unrelated directions. Adding the products totals the per-direction agreements into one number. You add the products $u_i v_i$, not the components.

## Two distinct zeros

$\langle v, v \rangle = 0$ holds only for $v = \mathbf{0}$ (a vector with itself). $\langle u, v \rangle = 0$ means $u$ and $v$ are orthogonal; neither need be zero. Example: $\langle (1,0),(0,1)\rangle = 0$, both nonzero, orthogonal.

## The orthonormal-coordinate theorem

**Theorem.** If $\{e_1, \dots, e_n\}$ is orthonormal and $v = c_1 e_1 + \dots + c_n e_n$, then $c_i = \langle v, e_i \rangle$.

Proof: $\langle v, e_i \rangle = \sum_j c_j \langle e_j, e_i \rangle$. By orthonormality every term vanishes except $j = i$, which is $c_i \cdot 1$. So $\langle v, e_i \rangle = c_i$.

This is why the standard basis is easy: the coordinates of $(3,4)$ are $\langle (3,4),(1,0)\rangle = 3$ and $\langle (3,4),(0,1)\rangle = 4$.

## Examples

Worked: $\langle (3,4),(1,2)\rangle = 3 + 8 = 11$.

Worked, with itself: $\langle (3,4),(3,4)\rangle = 9 + 16 = 25 = 5^2$ (length squared).

Worked, agreement and cancellation: $\langle (3,4),(4,-3)\rangle = 12 - 12 = 0$. The agreement in one direction cancels the disagreement in the other; the vectors are orthogonal.

Edge case: $\langle \mathbf{0}, \mathbf{0}\rangle = 0$, the only vector with zero self-inner-product.

# Length (The Norm)

## Definition

The norm (length) of a vector is

$$ \Vert v \Vert = \sqrt{\langle v, v \rangle}, $$

defined because P3 gives $\langle v, v \rangle \ge 0$. In $\mathbb{R}^n$, $\Vert v \Vert = \sqrt{v_1^2 + \dots + v_n^2}$, the Pythagorean length.

A norm satisfies:

- N1: $\Vert v \Vert \ge 0$, with equality if and only if $v = \mathbf{0}$.
- N2: $\Vert av \Vert = |a| \cdot \Vert v \Vert$.
- N3 (triangle inequality): $\Vert u + v \Vert \le \Vert u \Vert + \Vert v \Vert$ (proved below).

Proof of N2: $\Vert av \Vert = \sqrt{\langle av, av \rangle} = \sqrt{a^2 \langle v, v \rangle} = |a| \sqrt{\langle v, v \rangle} = |a| \cdot \Vert v \Vert$; the square root of $a^2$ is $|a|$.

## Examples

Worked: $\Vert (3,4) \Vert = \sqrt{9 + 16} = 5$.

Worked: $\Vert (1,1) \Vert = \sqrt{2}$.

Worked, scaling: $\Vert 2 \cdot (3,4) \Vert = \Vert (6,8) \Vert = \sqrt{36 + 64} = 10 = |2| \cdot 5$, confirming N2.

Edge case: $\Vert (0,0) \Vert = 0$, the only vector of length zero.

# Cauchy-Schwarz Inequality

## Statement

$$ |\langle u, v \rangle| \le \Vert u \Vert \cdot \Vert v \Vert, $$

with equality if and only if one vector is a scalar multiple of the other.

## Proof

If $v = \mathbf{0}$, both sides are 0. Assume $v \ne \mathbf{0}$, so $\langle v, v \rangle > 0$. For every real $t$,

$$ 0 \le \langle u - tv, u - tv \rangle = \langle u, u \rangle - 2t\langle u, v \rangle + t^2 \langle v, v \rangle. $$

This is an upward parabola in $t$, nowhere negative, with minimum at $t = \langle u, v \rangle / \langle v, v \rangle$. Writing $A = \langle u, u \rangle$, $B = \langle u, v \rangle$, $C = \langle v, v \rangle$, the minimum value is $A - B^2/C \ge 0$. Multiply by $C > 0$: $AC - B^2 \ge 0$, so $B^2 \le AC$, i.e. $\langle u, v \rangle^2 \le \Vert u \Vert^2 \Vert v \Vert^2$. Taking square roots gives $|\langle u, v \rangle| \le \Vert u \Vert \Vert v \Vert$. Equality occurs when $u - tv = \mathbf{0}$, i.e. $u = tv$.

## Examples

Worked: $u=(3,4)$, $v=(1,0)$: $|3| \le 5 \cdot 1$. True, not tight.

Worked, equality: $u=(3,4)$, $v=(6,8)=2u$: $|50| \le 5 \cdot 10 = 50$. Equality, since parallel.

Worked, slack: $u=(1,1)$, $v=(1,-1)$: $|0| \le \sqrt 2 \cdot \sqrt 2 = 2$. The vectors are orthogonal, giving the slackest case.

# Triangle Inequality

## Statement

$$ \Vert u + v \Vert \le \Vert u \Vert + \Vert v \Vert, $$

for all vectors, any angle.

## Proof

$$ \Vert u + v \Vert^2 = \Vert u \Vert^2 + 2\langle u, v \rangle + \Vert v \Vert^2 \le \Vert u \Vert^2 + 2\Vert u \Vert\Vert v \Vert + \Vert v \Vert^2 = (\Vert u \Vert + \Vert v \Vert)^2, $$

using $\langle u, v \rangle \le |\langle u, v \rangle| \le \Vert u \Vert\Vert v \Vert$ (Cauchy-Schwarz). Take square roots: $\Vert u + v \Vert \le \Vert u \Vert + \Vert v \Vert$. Equality when $u$ and $v$ are parallel and point the same way.

The triangle inequality holds for all vectors (an inequality with plain lengths). The Pythagorean theorem below holds only for orthogonal vectors (an equality with squared lengths). They are different statements.

## Examples

Worked: $u=(3,0)$, $v=(0,4)$: $5 \le 3 + 4 = 7$.

Worked, equality: $u=(3,0)$, $v=(6,0)$: $9 \le 9$.

Worked: $u=(1,0)$, $v=(1,1)$: $\sqrt 5 \approx 2.24 \le 1 + \sqrt 2 \approx 2.41$.

# Orthogonality and the Pythagorean Theorem

## Orthogonality

Vectors $u$ and $v$ are orthogonal when $\langle u, v \rangle = 0$. Example: $(1,1)$ and $(1,-1)$, since $\langle (1,1),(1,-1)\rangle = 0$.

## Pythagorean theorem

**Theorem.** If $\langle u, v \rangle = 0$, then $\Vert u + v \Vert^2 = \Vert u \Vert^2 + \Vert v \Vert^2$.

Proof: $\Vert u + v \Vert^2 = \Vert u \Vert^2 + 2\langle u, v \rangle + \Vert v \Vert^2$; orthogonality kills the middle term.

The middle term $2\langle u, v \rangle$ is the cross term, measuring directional agreement. A right angle makes it zero, so the squared lengths add. At any other angle it is nonzero and the squared lengths do not simply add.

In area terms: $\langle v, v \rangle = v_1^2 + \dots + v_n^2$ is the area of the square on $v$. The theorem says the area of the square on the resultant equals the sum of the areas of the squares on the two orthogonal pieces. The square root returns from area to length.

## Examples

Worked, orthogonal: $u=(3,0)$, $v=(0,4)$: $\langle u,v\rangle = 0$, and $\Vert u+v \Vert^2 = 25 = 9 + 16$.

Counterexample, not orthogonal: $u=(3,0)$, $v=(1,1)$: $\langle u,v\rangle = 3 \ne 0$. Then $\Vert u+v \Vert^2 = 17$ but $\Vert u \Vert^2 + \Vert v \Vert^2 = 11$; they differ by the cross term $2\cdot 3 = 6$.

Worked: $u=(2,0)$, $v=(0,5)$: orthogonal, $\Vert u+v \Vert^2 = 29 = 4 + 25$.

High-dimensional case: for pairwise orthogonal $v_1, \dots, v_k$, $\Vert v_1 + \dots + v_k \Vert^2 = \Vert v_1 \Vert^2 + \dots + \Vert v_k \Vert^2$, since all cross terms vanish. The standard basis of $\mathbb{R}^n$ is pairwise orthogonal, so the norm formula $\Vert v \Vert^2 = v_1^2 + \dots + v_n^2$ is the Pythagorean theorem applied to $n$ orthogonal pieces.

# Angle Between Two Vectors

## Definition

This is some handwaving here, but not incorrect:

Two vectors "agree in direction" a lot, a little, or not at all, and that degree of agreement is the angle between them. Small angle means strong agreement, right angle means none, straight-opposite means negative.

For nonzero $u, v$,

$$ \cos\theta = \frac{\langle u, v \rangle}{\Vert u \Vert \cdot \Vert v \Vert}, \qquad 0 \le \theta \le \pi. $$
 

Cauchy-Schwarz gives $-1 \le \langle u, v \rangle / (\Vert u \Vert\Vert v \Vert) \le 1$, so this is a valid cosine and $\theta$ always exists.

(for now accept this. we will open this pandora box once we do geometry and lie )
## Examples

Worked: $(1,0)$ and $(1,1)$: $\cos\theta = 1/\sqrt 2$, $\theta = 45^\circ$.

Worked: $(1,0)$ and $(0,1)$: $\cos\theta = 0$, $\theta = 90^\circ$.

Worked: $(1,0)$ and $(3,0)$: $\cos\theta = 1$, $\theta = 0^\circ$.

Worked: $(1,0)$ and $(-1,0)$: $\cos\theta = -1$, $\theta = 180^\circ$.

ML rung (cosine similarity): in $\mathbb{R}^{300}$, two text or image embeddings $u, v$ are compared by $\cos\theta = \langle u,v\rangle / (\Vert u \Vert\Vert v \Vert)$. Near 1 means similar direction (similar meaning); near 0 means unrelated; near $-1$ means opposite. The angle is well defined in 300 dimensions because Cauchy-Schwarz holds there. Dividing by the lengths removes the effect of vector size, leaving direction.

# Orthogonal Projection

## What problem it solves

The dot product measures directional agreement. Projection makes this exact: it gives, as a vector, the part of $u$ that lies along the direction of $v$. It is the seed of least squares.

## Definition

For a vector $u$ and a nonzero direction $v$, the orthogonal projection of $u$ onto $v$ is

$$ \operatorname{proj}_v(u) = \frac{\langle u, v \rangle}{\langle v, v \rangle} \cdot v, $$

a scalar multiple of $v$.

**Defining property.** The leftover $w = u - \operatorname{proj}_v(u)$ is orthogonal to $v$: $$ \langle w, v \rangle = \langle u, v \rangle - \frac{\langle u, v \rangle}{\langle v, v \rangle}\langle v, v \rangle = \langle u, v \rangle - \langle u, v \rangle = 0. $$ So $u$ splits into a part along $v$ and a part orthogonal to $v$. If $v$ has unit length, $\operatorname{proj}_v(u) = \langle u, v \rangle \cdot v$, and $\langle u, v \rangle$ is the length of the shadow.

## Examples

Worked: $u = (3,4)$ onto $v = (1,0)$: scalar $3/1 = 3$, projection $(3,0)$, leftover $(0,4)$, and $\langle (0,4),(1,0)\rangle = 0$. So $(3,4) = (3,0) + (0,4)$.

Worked: $u = (2,0)$ onto $v = (1,1)$: scalar $2/2 = 1$, projection $(1,1)$, leftover $(1,-1)$, and $\langle (1,-1),(1,1)\rangle = 0$.

Connection: since the two pieces are orthogonal, Pythagoras gives $\Vert u \Vert^2 = \Vert \operatorname{proj} \Vert^2 + \Vert \text{leftover} \Vert^2$.

ML rung (dimensionality reduction): given data points $(2,2), (4,4), (6,6) on the diagonal, project each onto $v = (1,1)$. Each projection scalar is $4/2 = 2$, $8/2 = 4$, $12/2 = 6$; each leftover is $\mathbf{0}$. Keeping only the projection scalar describes each point by one number. The data is one-dimensional inside the plane. Choosing the projection direction to capture the most spread is the core of PCA.

# Euclidean Space

A Euclidean space is a finite-dimensional real vector space with the standard inner product (the dot product). $\mathbb{R}^n$ with the dot product is the Euclidean space of dimension $n$.

Three properties, all consequences of flatness:

- Pythagoras holds globally, for every orthogonal pair, at every scale.
- The inner product (the measuring rule) is the same at every point.
- Length, angle, and distance agree with ordinary physical measurement.

# Distance (The Metric)

## Definition

The distance between $x, y \in V$ is

$$ d(x, y) = \Vert x - y \Vert. $$

A function $d$ is a metric if, for all $x, y, z$:

- M1: $d(x, y) \ge 0$, with equality if and only if $x = y$.
- M2: $d(x, y) = d(y, x)$.
- M3 (triangle inequality): $d(x, z) \le d(x, y) + d(y, z)$.

A set with a metric is a metric space.

## Proof that $\Vert x - y \Vert$ is a metric

M1 from N1: $\Vert x - y \Vert \ge 0$, zero only when $x - y = \mathbf{0}$, i.e. $x = y$.

M2 from N2: $\Vert y - x \Vert = \Vert -(x - y) \Vert = |-1| \cdot \Vert x - y \Vert = \Vert x - y \Vert$.

M3 from N3: $x - z = (x - y) + (y - z)$, so $\Vert x - z \Vert \le \Vert x - y \Vert + \Vert y - z \Vert$ by the norm triangle inequality.

## Why "norm of the difference" means how different

For one number, 3 and 7 differ by $|7 - 3| = 4$; the absolute value is the one-dimensional norm. For vectors, the difference $x - y$ records the difference in every component; its norm is the straight-line gap between the two points. Two equal points give the zero vector and distance 0; small differences give a small norm; large differences give a large norm. Squaring and rooting give the straight-line gap $\sqrt{3^2 + 4^2} = 5$, not the component sum $3 + 4 = 7$.

## Examples

Worked: $x = (1,1)$, $y = (4,5)$: difference $(-3,-4)$, distance $\sqrt{9 + 16} = 5$. Reverse direction gives $(3,4)$, also 5, confirming M2.

Worked: $x = (2,1)$, $y = (5,5)$: difference $(-3,-4)$, distance 5.

Edge case: $d(x,x) = \Vert \mathbf{0} \Vert = 0$.

ML rung (image distance and its limit): a 4-pixel image is a vector in $\mathbb{R}^4$. For $u = (10,20,30,40)$ and $v = (12,18,30,44)$, the difference is $(-2,2,0,-4)$ and the distance is $\sqrt{4 + 4 + 0 + 16} = \sqrt{24} \approx 4.9$. The squaring makes one large pixel difference count more than several small ones. This is why pixel distance is not the same as how different two images look to a human, which is a central problem in computer vision.

# Clarifications

These are the questions worth slowing down on. They came up while building the material and are easy to get wrong.

## A basis cares about count and direction, not length

"Smallest" in the idea of a basis means the fewest vectors, not the shortest vectors. The basis $\{(2,0),(0,3)\}$ is a perfectly good basis of $\mathbb{R}^2$, even though its vectors are not unit length. Length only matters for the special kind called orthonormal. A plain basis has no length requirement.

## Dimension counts directions, not points

A nontrivial space has infinitely many vectors (points), but its dimension is the finite number of basis vectors, the number of independent directions. These are different. In high dimensions, counting points is useless (every space has infinitely many), so dimension is the only honest measure of size: $\mathbb{R}^{4096}$ is larger than $\mathbb{R}^{784}$ because $4096 > 784$ directions.

## The dimension of the space versus the effective dimension of the data

Changing the basis never changes the dimension of the space; a basis of $\mathbb{R}^2$ always has two vectors. But data living in that space can be effectively lower-dimensional. If points lie near a line, a good basis puts almost all their spread into one coordinate and nearly zero into the other, so you can drop the second coordinate with little loss. The space stays two-dimensional; the data is effectively one-dimensional. A basis change does not shrink the space; it reveals that the data was already nearly flat in one direction. This gap is what makes dimensionality reduction possible.

## Reverse-engineering a basis

You cannot recover a basis from a single vector; the same vector has coordinates in infinitely many bases, so the basis is a free choice, not a hidden property. But from a cloud of many vectors you can find a good basis, the directions the data spreads along. Finding that basis automatically is what PCA does, and the tool that computes it is the SVD.

# Common Errors

- Confusing a vector with its coordinates. The vector is a fixed point; coordinates are its address in a chosen basis, and they change with the basis.
- Confusing orthogonal and orthonormal. Orthogonal is perpendicular; orthonormal is perpendicular and unit length.
- Confusing a zero entry, the zero vector, and a zero coefficient. A dark pixel is a zero entry in a vector. The zero vector is the all-zero vector, required in the space by A3. A zero coefficient is a separate thing in the independence test. A3 requires the space to contain the zero vector; it does not require every vector to contain a zero entry.
- Using the Pythagorean formula without a right angle. The squares add only for orthogonal vectors; otherwise there is a cross term.
- Mismatched components for distance. Subtract matching components $u_i - v_i$.

# Connections

Every definition here builds toward an exact notion of distance. The eight axioms give addition and scaling. The inner product adds length and angle. From length comes distance, and the metric axioms make it behave like real distance. Cosine similarity uses the angle; dimensionality reduction uses projection and basis change; least squares uses projection onto a subspace; image comparison uses the metric.

# Practice Problems

## Problem 1

Compute $\langle u, v \rangle$, $\Vert u \Vert$, and $\Vert v \Vert$ for $u = (2,1)$, $v = (3,4)$.

## Problem 2

Are $(1,2)$ and $(2,4)$ linearly independent? Justify.

## Problem 3

Is $\{(2,0),(0,1)\}$ orthonormal? Check both conditions.

## Problem 4

Find the coordinates of $(4,0)$ in the basis $\{(1,1),(1,-1)\}$.

## Problem 5

Project $u = (4,2)$ onto $v = (1,0)$. Give the projection and leftover, and check orthogonality.

## Problem 6

For embeddings $u = (1,0,1)$, $v = (1,1,0)$ in $\mathbb{R}^3$, compute the cosine similarity.

# Solutions

## Solution 1

$\langle u,v\rangle = 2\cdot 3 + 1\cdot 4 = 10$. $\Vert u \Vert = \sqrt{5}$. $\Vert v \Vert = 5$.

## Solution 2

Dependent: $(2,4) = 2(1,2)$, a scalar multiple, so they lie on one line through the origin.

## Solution 3

Orthogonal ($\langle (2,0),(0,1)\rangle = 0$) but not orthonormal, since $\Vert (2,0) \Vert = 2 \ne 1$.

## Solution 4

$a(1,1) + b(1,-1) = (4,0)$ gives $a + b = 4$, $a - b = 0$, so $a = b = 2$. Coordinates $(2,2)$.

## Solution 5

Scalar $4/1 = 4$, projection $(4,0)$, leftover $(0,2)$, and $\langle (0,2),(1,0)\rangle = 0$.

## Solution 6

$\langle u,v\rangle = 1$. $\Vert u \Vert = \Vert v \Vert = \sqrt 2$. $\cos\theta = 1/2$, so $\theta = 60^\circ$; somewhat similar.
