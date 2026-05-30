+++
title = "Linear Algebra Part 1"
slug = "vector_space"
toc = true
+++

# Vector Space

A vector space over a field $F$ is a set $V$ with two operations: vector addition and scalar multiplication. The set and the operations must follow eight rules. We call these rules axioms.

A vector is any member of $V$. This is the full meaning. A vector is not "an arrow with size and direction." A vector is anything that follows the eight axioms. The arrow is only one example.

There are two kinds of object here. They are different. Do not mix them.

- **Vectors:** The members of $V$. The things you add.
- **Scalars:** The plain numbers from $F$. For us, $F$ is the real numbers $\mathbb{R}$. The things you scale a vector by.

You can add a vector to a vector. You can multiply a scalar by a vector. You cannot add a vector to a scalar. That has no meaning.

## The eight axioms

For any vectors $u, v, w \in V$ and any scalars $a, b \in F$.

Four rules for addition:

- **A1 (Commutativity):** $u + v = v + u$. Order does not matter.
- **A2 (Associativity):** $(u + v) + w = u + (v + w)$. Grouping does not matter.
- **A3 (Identity):** There is a zero vector $\mathbf{0}$. Adding it changes nothing: $v + \mathbf{0} = v$.
- **A4 (Inverses):** Every vector $v$ has an inverse $(-v)$. They add to zero: $v + (-v) = \mathbf{0}$.

Four rules for scaling:

- **A5 (Distributivity 1):** $a(u + v) = au + av$.
- **A6 (Distributivity 2):** $(a + b)v = av + bv$.
- **A7 (Compatibility):** $a(bv) = (ab)v$.
- **A8 (Identity):** $1 \cdot v = v$. Scaling by one changes nothing.

{% callout_important() %}
## Relevance to Machine Learning
A4 is the rule the Gaussian distribution needs most. Subtraction is defined from it: $u - v$ means $u + (-v)$. Without A4 there is no subtraction. Then there is no "$x - \mu$". Then there is no Gaussian.
{% end %}

## How addition is done

The axioms say what addition must obey. They do not say how to compute it. How you compute it depends on the space.

- **In $\mathbb{R}^n$:** add by component: $(u_1, \dots, u_n) + (v_1, \dots, v_n) = (u_1+v_1, \dots, u_n+v_n)$. Example: $(3,0) + (0,4) = (3,4)$.
- **In function space:** add by point: $(f + g)(x) = f(x) + g(x)$. The sum is a new function.

$\mathbb{R}^n$ follows the axioms because each component is a real number, and real numbers already follow these rules.

## How a vector looks

- **Small:** a vector in $\mathbb{R}^n$ is a list of $n$ numbers. Example: $(3,4)$.
- **Large:** in $\mathbb{R}^{784}$ a vector is a list of $784$ numbers. A $28 \times 28$ gray image is one such vector. Each pixel brightness is one number in the list.
- **Other:** a function is a vector. You can think of a function as a vector with one number for every input point. So it has infinitely many numbers. The Gaussian lives in this function space.

## Axiom and theorem are different

This point is important.

- An **axiom** is assumed. To check that something is a vector space, you check that all eight axioms hold for it.
- A **theorem** is proved from the axioms. Once you prove it, it is true in every vector space. You never check it again.

So you check the eight axioms one time for a candidate. After that, every theorem comes for free.

## Two proofs we did

- **The zero vector is unique.**  
  *Method:* assume two zeros, $\mathbf{0}$ and $\mathbf{0}'$. Compute $\mathbf{0}' + \mathbf{0}$ in two ways. One way gives $\mathbf{0}'$. The other way gives $\mathbf{0}$. So $\mathbf{0}' = \mathbf{0}$. There is only one.
- **Zero scalar times any vector gives the zero vector:** $0 \cdot v = \mathbf{0}$.  
  *Method:* start from $0 + 0 = 0$ for numbers. Use A6 to get $0 \cdot v = (0+0) \cdot v = 0 \cdot v + 0 \cdot v$. Then add the inverse $-(0 \cdot v)$ (from A4) to both sides and cancel. You are left with $0 \cdot v = \mathbf{0}$.

## Where it came from

First came the geometric ideas. Hamilton and Grassmann worked on directed quantities in the 1840s. Then came matrix and determinant work later in the 1800s. The clean eight-axiom definition came last. Peano wrote it in 1888. So the examples came first and the abstract rules came last. We teach it the other way, rules first, because that is more exact. But that is the reverse of history.

---

# Linear Combination

Take some vectors $v_1, \dots, v_n$. Take some scalars $a_1, \dots, a_n$. A linear combination is:

$$a_1 v_1 + a_2 v_2 + \dots + a_n v_n$$

The scalars are the coefficients.

How to do it: scale each vector by its coefficient, then add the results. It uses only the two operations of the space. The result is always a vector in the same space. It never leaves.

Example: $3 \cdot (1,0) + 4 \cdot (0,1) = (3,0) + (0,4) = (3,4)$. In words: go $3$ along the first direction, $4$ along the second, and you land at $(3,4)$.

Two special cases:
- All coefficients zero. The result is the zero vector. We call this the *trivial combination*. It matters for independence.
- One coefficient is one, the rest zero. The result is that single vector.

One note: a linear combination is always a finite sum. Infinite sums need an extra idea about limits. We do not use that yet.

Vector and coefficient are different. This caused confusion before, so be careful.

- The **vectors** (like $e_1$) are fixed building blocks. You do not change them.
- The **coefficients** are the numbers in front. These are what you choose or solve for.

The same form $a \cdot e$ is used two ways. When you build a target, the coefficient is the amount you want. When you test independence, the coefficient is an unknown you solve for. The building block stays the same in both cases.

---

# Span

The span of $v_1, \dots, v_n$ is the set of all their linear combinations. It is everything you can reach by any choice of coefficients.

How to use it:
- To make the span: choose coefficients, form the combination. The span is all such results together.
- To test if a vector $w$ is in the span: ask if there are coefficients with $a_1 v_1 + \dots + a_n v_n = w$. This is a system of equations. If it has a solution, $w$ is in the span. If not, it is not.

Example: span of $(1,0)$ is the whole horizontal line, all points $(a,0)$. Add $(0,1)$. Now span of $(1,0)$ and $(0,1)$ is all of $\mathbb{R}^2$. You can reach any $(a,b)$.

Key fact: a span is itself a vector space inside $V$. It always contains the zero vector. It always passes through the origin.

Note: a line or plane that does not pass through the origin is not a span. The span always contains zero.

---

# Linear Independence

The vectors $v_1, \dots, v_n$ are linearly independent if the only way to get the zero vector is to use all-zero coefficients:

$$a_1 v_1 + \dots + a_n v_n = \mathbf{0} \implies a_1 = \dots = a_n = 0$$

If some nonzero coefficients give zero, the vectors are linearly dependent.

Plain meaning: independent means no vector is a wasteful copy of the others. Dependent means at least one is reachable from the others.

How to test: set the combination equal to zero. Write it component by component. This gives a system in the coefficients. Solve it.

- Only the all-zero solution: independent.
- Any nonzero solution: dependent. That solution shows you the waste.

Examples:
- $(1,0)$ and $(0,1)$. Set $a(1,0) + b(0,1) = (0,0)$. This forces $a = 0$ and $b = 0$. Independent.
- $(1,0)$, $(0,1)$, $(1,1)$. Set the sum to zero. You get $a + c = 0$ and $b + c = 0$. Take $c = 1$. Then $a = -1, b = -1$. These are nonzero. Dependent. The relation says $(1,1) = (1,0) + (0,1)$. This is the waste, shown clearly.

Shortcut for two vectors: two vectors are dependent exactly when one is a scalar multiple of the other. They lie on the same line through the origin. Example: $(1,2)$ and $(2,4)$. Since $(2,4) = 2 \cdot (1,2)$, they are dependent. Warning: this simple rule is only for two vectors. For three or more, dependence does not need one vector to be a multiple of one other.

Edge cases:
- Any set that contains the zero vector is automatically dependent.
- A single nonzero vector is always independent.

Word trap: dependent means you reach zero using nonzero coefficients. Independent means only the all-zero coefficients reach zero. This is easy to flip, so read it slowly.

---

# Basis

A set is a basis of $V$ if it does two things at once: it spans $V$, and it is linearly independent. Both must hold.

Plain meaning: the smallest set of building blocks that can build everything, with no waste. Here "smallest" means the fewest vectors. It does not mean the shortest vectors.

How to check: check both conditions. Spanning: you can solve for any target. Independence: only the all-zero combination gives zero. Both pass, it is a basis.

A space has many bases. For $\mathbb{R}^2$:
- Standard: $(1,0)$ and $(0,1)$.
- Diagonal: $(1,1)$ and $(1,-1)$.
- Stretched: $(2,0)$ and $(0,3)$.

All three are valid.

{% callout_warning() %}
## Mistake to Avoid
A basis does not need short vectors. Length does not matter. $(2,0)$ and $(0,3)$ is a fine basis. "Smallest" is about the number of vectors, never their length. The version that controls length is called an orthonormal basis. There the vectors have length one and are perpendicular. That is an extra condition. It comes later with the inner product.
{% end %}

The standard basis: in $\mathbb{R}^n$ it is the vectors $e_i$, each with a single $1$ in position $i$ and $0$ in all other positions. We choose it by habit, not by law. We choose it because it is the easiest. With it, the coefficients are equal to the slot values directly. And independence and span are obvious, because each $e_i$ touches only its own slot, so they cannot interfere.

---

# Dimension

The dimension of $V$ is the number of vectors in a basis of $V$.

This only makes sense if every basis has the same number of vectors. That is the theorem.

**Theorem:** If $V$ has a basis of $n$ vectors, then every basis of $V$ has exactly $n$ vectors.

- It rests on a counting lemma. The lemma says: if one set spans, and another set is independent, then the independent set is not larger than the spanning set. In short, independent is at most spanning.
- Proof of the theorem from the lemma: take two bases, $B$ with $n$ vectors and $C$ with $m$ vectors. $B$ spans and $C$ is independent, so $m$ is at most $n$. $C$ spans and $B$ is independent, so $n$ is at most $m$. Both hold, so $n = m$.
- The lemma's method: feed the independent vectors in one at a time. Each one swaps out one vector from the spanning set, and the set still spans. If there were more independent vectors than spanning vectors, you would run out of vectors to swap, and that gives a contradiction. This is the replacement method.

Examples:
- $\dim \mathbb{R}^2 = 2$. $\dots$ $\dim \mathbb{R}^n = n$. $\dots$ $\dim \mathbb{R}^{784} = 784$.
- Polynomials of degree at most $3$. A basis is $\{1, x, x^2, x^3\}$. So the dimension is $4$. In general, degree at most $n$ gives dimension $n+1$, because there are $n+1$ free coefficients.
- The space with only the zero vector has dimension $0$. Its basis is the empty set.

High dimension view: in $2$ or $3$ dimensions you can see the axes, so the number feels like a picture. The strength of the definition is that it works without a picture. $\mathbb{R}^{4096}$, which is a $64 \times 64$ image, has dimension $4096$ by a counting argument. You do not need to see it. Dimension lets you compare spaces you cannot see: $4096$ is more than $784$, and that is exact. In high dimension, dimension is the only honest measure of size. Both spaces have infinitely many points, so counting points is useless. Counting directions tells you everything.

{% callout_tip() %}
## Two kinds of dimension (the deep point)
- **Number of vectors inside the space:** infinite for any space bigger than $\{\mathbf{0}\}$. This counts points.
- **Dimension:** the small basis count. This counts independent directions.

These two are equal only for the trivial space $\{\mathbf{0}\}$. The idea "polynomials are functions, so the dimension is infinite" is wrong. Polynomials of degree at most $3$ have only $4$ free choices, so dimension $4$. Being a function does not make the dimension infinite. Having infinitely many free choices makes it infinite.
{% end %}

# Pixels — A Worked Example

An image is a vector. A $2$-pixel image is (left brightness, right brightness), a vector in $\mathbb{R}^2$. A $4096$-pixel image is a vector in $\mathbb{R}^{4096}$. The $x,y$ location of a pixel is only its address. What is left in the vector is the brightness of each pixel.

Building blocks (the standard basis): $e_1 = (1,0)$ means "left pixel lit, right pixel dark." $e_2 = (0,1)$ means "left dark, right lit." The single $1$ picks which pixel is lit. The $0$ means the other pixel is dark.

- **Span:** any image $(\text{left}, \text{right}) = \text{left} \cdot e_1 + \text{right} \cdot e_2$. Each pixel brightness is the coefficient on that pixel's building block. So these building blocks span all images. To build any image, use each pixel brightness as its coefficient.
- **Independence:** $a e_1 + b e_2 = (a,b)$. For this to be $(0,0)$, you need $a = 0$ and $b = 0$. Each building block touches only its own pixel, so none can cancel another. They are independent. No waste.
- It scales to $4096$ with no change. One building block per pixel, each lighting one pixel. They span and stay independent by the same single argument. You never solve $4096$ equations. You argue once over all slots at the same time.

How to check span and independence in high dimension: never by brute force. Use one general argument over all coordinates at once.

- **Span:** take a general target $(t_1, \dots, t_n)$. Give a recipe for the coefficients that always works. For the standard basis, the coefficients are just the $t$ values.
- **Independence:** set the general combination to zero. Show only all-zero works. For the standard basis, the combination equals $(a_1, \dots, a_n)$, so all $a$ values are zero.
- **Shortcut:** in a space of known dimension $n$, any $n$ independent vectors automatically span. So you usually check only one condition.

{% callout_important() %}
## The two zeros and A3
- Brightness $0$, a dark pixel. This is a $0$ inside one slot of a vector. It is fine.
- The zero vector, the all-black image. A3 requires this to exist in the space. This is about the whole space, not about one vector.
- A coefficient being $0$ in the test. This is a third thing, about coefficients, not about brightness.

A3 does not say every vector must contain a zero. An image with no dark pixels is a valid vector. A3 says the whole space must contain the all-black image. Think of a team. The rule "the team must include a person named Zero" is about the roster having that member. It is not a rule that every member has a zero in their name.

A separate rule: do not use the zero vector as a building block. A set that contains the zero vector is always dependent. So the zero vector lives in the space, but we leave it out of the basis.
{% end %}

The $0$ to $255$ range is a real-photo limit. It does not matter for the vector space math. The space $\mathbb{R}^{4096}$ allows any real numbers, even negative ones and ones above $255$. Coefficients can be anything.

---

# Coordinates

Once you fix a basis, every vector has one unique list of coefficients that builds it. That list is its coordinates in that basis.

- Span gives at least one such list.
- Independence gives at most one.
- Together: exactly one. So coordinates are unique once the basis is fixed.

You choose the target vector. The coordinates are then forced. You compute them, you do not pick them freely. With the standard basis the coordinates happen to equal the slot values, so it looks like you choose them. But they are still forced.

Same vector, different bases, different coordinates. Example: the point $(3,2)$.

- Standard basis $(1,0), (0,1)$: coordinates $(3,2)$.
- Diagonal basis $(1,1), (1,-1)$: solve $a(1,1) + b(1,-1) = (3,2)$. You get $a = 2.5, b = 0.5$. So coordinates $(2.5, 0.5)$.

The point did not move. The numbers changed because the directions changed.

---

# The Basis-Change Idea

Why bases and coordinates matter: a good basis shows hidden structure and lets you drop the coordinates that do not matter.

Data cloud example. Points lie roughly along a tilted line in $\mathbb{R}^2$.

- **Standard basis (east, north):** both coordinates of every point are large. The structure is hidden.
- **Tilted basis:** $u_1 = (1,1)$ along the spread, $u_2 = (1,-1)$ across it. Now each point's first coordinate (along $u_1$) is large and different for each point. The second coordinate (along $u_2$) is tiny for every point.
- Drop the tiny second coordinate. Now each point is just one number. The data is, in effect, one-dimensional.

{% callout_tip() %}
## Two kinds of dimension in data
- **Dimension of the space:** still $2$. The new basis still has two vectors. A basis change never changes the dimension of the space. This is exact.
- **Effective dimension of the data:** about $1$. The points nearly sit on a line, so one coordinate is nearly enough. This is approximate. Dropping the small coordinate adds a small error.
{% end %}

The basis change did not shrink the space. It revealed that the data was already nearly one-dimensional, and it lined up the coordinates so the important direction got its own coordinate.

New features are made from old ones:
- Original features: the raw coordinates. East, north. Or height, weight. Or pixel values.
- After the rotation: new features. Each one is a mix of the originals. The $u_1$ coordinate is "east plus north," a blend, not either original.
- The rotation does not rename old features. It builds better ones by mixing them, then keeps the useful ones.

The useful direction is not the old $x$ and not the old $y$. It is a new direction, the diagonal, with a new name, the first principal direction or $u_1$.

Forward link: finding that tilted basis on its own, in any dimension, is what PCA does. The first principal component is the direction of most spread. The tool that finds it is the SVD. So this example is a preview of the SVD knot. The gap between a large space dimension and a small effective data dimension is what makes dimensionality reduction possible.

---

# Concept Map

$$\text{vector space (8 axioms; set + field + 2 operations)} \to \text{linear combination (scale and add)} \to \text{span (all linear combinations)} \to \text{linear independence (no waste)}$$
$$\downarrow$$
$$\text{basis (spans and independent)} \to \text{dimension (size of any basis)} \to \text{coordinates (unique coefficient list)}$$
$$\downarrow$$
$$\text{subspace} \to \text{inner product} \to \text{norm} \to \text{metric} \to \text{squared distance} \to \text{Gaussian}$$

---

# Anchors

- **Vector space:** "anything that follows the eight axioms."
- **Linear combination:** "scale and add."
- **Span:** "everything those vectors can reach."
- **Linear independence:** "no vector is a wasteful copy of the others."
- **Basis:** "the fewest building blocks that build everything."
- **Dimension:** "count of independent directions, not points."
- **Coordinates:** "the one recipe for a vector in a chosen basis."
- **Basis change:** "rotate to where the information is, then drop the rest."
