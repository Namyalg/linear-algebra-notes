# Vector Spaces — the "vectors" are whatever you say they are

A vector space $V$ is a set of objects you can add and scale (per the axioms), but the
objects themselves can be almost anything. The word "vector" doesn't mean "arrow" — it
means **an element of the space**, whatever form that takes. This is the table that
makes that concrete.

| Vector space $V$          | What the "vectors" actually are                     |
|---------------------------|-----------------------------------------------------|
| $\mathbb R^3$             | 3D numerical vectors                                |
| $\mathbb R^n$             | Arrays of $n$ numbers                               |
| Matrices                  | Matrices of a fixed size                            |
| Polynomials               | Polynomials such as $2x^3-x+4$                      |
| Functions                 | Functions such as $f(x)=\sin x$                     |
| Signals                   | Time-varying signals                                |
| Images                    | Pixel-value functions/arrays                        |
| Sequences                 | Infinite sequences such as $(1,\frac12,\frac14,\ldots)$ |
| Geometric vectors         | Arrows/displacements                                |
| Tensors                   | Higher-order numerical objects                      |

## Why this echoes the first lecture

The very first conversations were versions of exactly this table:

- **"All polynomials" = infinite-dimensional** — the space of *all* polynomials $P$
  needs the infinite basis $\{1, x, x^2, \ldots\}$; each $P_n$ (degree ≤ $n$) is a
  finite-dimensional slice. Every polynomial in the list above is just an element of
  one of those spaces.
- **"sin x can't be represented discretely"** — a function like $\sin x$ is a single
  element of the space of functions; it isn't a finite "stack of numbers" the way
  $[3,5] \in \mathbb R^2$ is. Same for signals, images, and sequences.
- **Geometric vectors are just one example** — the "arrows/displacements" row. The
  free-vs-fixed discussion lives there.

So the takeaway: **the axioms don't care what the objects are.** The moment a
collection of things supports addition and scaling that obey the field rules, it's a
vector space — whether the elements are arrows, polynomials, sine waves, or infinite
sequences.

## Scalar connection (ties to `field.md`)

In every row the *scalars* multiplying the vectors come from a field ($\mathbb R$,
$\mathbb C$, ...). The field supplies the multiplication coefficients; $V$ supplies
the objects. That's why `field.md` and this note are siblings — together they answer
"what do I multiply" (field) and "what can I multiply" (this table).