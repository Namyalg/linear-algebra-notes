# What is a Field?

A **field** is a number system with rules for arithmetic. The easiest way to
understand it is to build it from the ground up — forget vectors entirely for now.

## 1. Start with a set

Suppose we have some collection of objects:

$$
F = \{0,1,2,3,\ldots\}
$$

A **field** is going to be a particular kind of set where we have defined ways to
**combine two elements**.

For a field, we define two operations:

$$
+ \qquad \text{and} \qquad \times
$$

So if $a,b\in F$, we can ask:

$$
a+b = ?
$$

and

$$
a\times b = ?
$$

These operations must produce elements that behave according to certain rules.

## 2. Why two operations?

Think of the field as a **number system with rules for arithmetic**.

For the real numbers:

$$
\mathbb R
$$

we know how to do:

$$
2+3=5
$$

and

$$
2\times3=6.
$$

But we also need the operations to behave nicely.

For example:

$$
2+3=3+2
$$

and

$$
(2+3)+4=2+(3+4).
$$

And multiplication interacts with addition:

$$
2(3+4)=2(3)+2(4).
$$

So a field is essentially saying:

> **Here is a collection of objects, here are two ways of combining them, and here
> are the rules those combinations must obey.**

## 3. The important part: inverses

The thing that really distinguishes a field from something like the integers is that
**you can undo the operations.**

For addition, every number needs an additive inverse:

$$
a+(-a)=0.
$$

For example:

$$
5+(-5)=0.
$$

For multiplication, every **nonzero** number needs a multiplicative inverse:

$$
a\cdot a^{-1}=1.
$$

For example:

$$
5\cdot\frac15=1.
$$

This is why division works:

$$
\frac{5}{3} = 5\cdot\frac13.
$$

## 4. Why aren't integers a field?

Consider:

$$
\mathbb Z=\{\ldots,-2,-1,0,1,2,\ldots\}.
$$

Addition works:

$$
2+3=5.
$$

Multiplication works:

$$
2\times3=6.
$$

You can also subtract:

$$
2-3=-1.
$$

But multiplication doesn't have an inverse **inside the integers**.

For example, what integer $x$ satisfies

$$
2x=1?
$$

There isn't one.

The answer would be

$$
x=\frac12,
$$

but

$$
\frac12\notin\mathbb Z.
$$

Therefore:

$$
\boxed{\mathbb Z\text{ is not a field}}
$$

## 5. Why are real numbers a field?

Consider:

$$
\mathbb R.
$$

Take any two real numbers $a,b$.

You can:

* add them → still real
* subtract them → still real
* multiply them → still real
* divide them, provided $b\neq0$ → still real

For example:

$$
7+3=10
$$

$$
7-3=4
$$

$$
7(3)=21
$$

$$
7/3\in\mathbb R.
$$

And all the required rules hold.

Therefore:

$$
\boxed{\mathbb R\text{ is a field}}
$$

Likewise:

$$
\boxed{\mathbb Q\text{ and }\mathbb C\text{ are fields}}
$$

## 6. So what does "field" really mean?

Don't memorize the formal axioms yet. Instead, keep this mental model:

> **A field is a set of objects that behaves like a complete number system for
> ordinary arithmetic: you can add and multiply, and you can undo addition and
> multiplication (except division by zero), with the operations obeying consistent
> rules.**

Formally, we write:

$$
\boxed{(F,+,\times)}
$$

because we're saying:

* $F$ = the set
* $+$ = one operation
* $\times$ = another operation

and the three together satisfy the field axioms.

**Only after this idea is solid should we bring vectors back in.** The connection to
vector spaces then becomes much easier: the field supplies the **scalars** you are
allowed to multiply vectors by.

---

## Reference & one step further: ordered fields and completeness

The formal definition here matches **Gressman, *Advanced Analysis*, "Complete
Ordered Fields"** (upenn.edu). It states the field axioms as a triple $(F,+,\cdot)$
with the five rules we used — commutativity, associativity, identities ($0\neq 1$),
inverses, and distributivity — and then *derives* consequences like $0\cdot a = 0$
and $-a = (-1)\cdot a$ from those axioms rather than assuming them. It also proves
the inverses are **unique** (there's only one $-a$ and one $a^{-1}$).

That page then adds **two things a bare field doesn't give you:**

1. **Ordered field** — a field *plus* a total order $<$ obeying trichotomy,
transitivity, and the rules that adding preserves $<$ and multiplying by a positive
$c$ preserves $<$. Key payoff: $0<1$ is *provable* from the axioms.
2. **Completeness** — every nonempty set bounded above has a least upper bound
(supremum). This is what makes **ℝ** special among fields.

**Why this matters for our earlier "gap-free" discussion:** ℚ is an *ordered* field,
but it is **not complete** — $\{x \in \mathbb Q : x^2 < 2\}$ has no supremum *in*
ℚ; the hole is $\sqrt 2$. ℝ is the complete ordered field, which is exactly why the
reals have no gaps and scalar closure always "lands inside". So the ladder is:

> field → ordered field → **complete** ordered field (ℝ vs ℚ vs ℂ)

(The complex numbers ℂ are a field but are *not* ordered — none of the order axioms
can be made to hold — so "order" is what separates ℝ/ℚ from ℂ, even though all three
are fields.)

Source: <https://www2.math.upenn.edu/~gressman/analysis/01-orderedfields.html>