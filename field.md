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