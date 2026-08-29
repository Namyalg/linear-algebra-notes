# Linear Algebra — Exploratory Notes

Working notes kept while teaching myself linear algebra basics. The point of this
repo is not to summarize a textbook — it's to record *where I got confused and how I
got unstuck*. Every topic here is one where I went back and forth until it clicked,
and the resources are the artifacts of that process: the confusion log, the proofs I
insisted on building from scratch, and the pictures I needed drawn.

## The map: why each topic got this deep

### 1. Vector spaces, dimension, and P (the "all polynomials" rabbit hole)
**Why it went deep:** "dimension" sounds like it should be about how long a vector is,
and every example until P agreed (R³ has 3-element vectors, P₂ has 3 coefficients).
Then P breaks that entirely — the basis {1, x, x², ...} never ends, and I kept
confusing "unbounded degree" with "infinite vectors."

**The resolution that stuck:** the degree is uncertain up front but every polynomial
you actually hold is finite. The infinity lives in the space's *directions*, never in
a single vector. And P contains *all* the Pₙ's at once — it's not "either P₃ or P₁₀₀₀".

**Where:** `lecture-1-confusions.md` (topics on P, dim(P) = ℵ₀, the ladder table).

### 2. Norms and the triangle inequality — the proof, not the statement
**Why it went deep:** everyone tells you ‖u+v‖ ≤ ‖u‖ + ‖v‖. I didn't want the
statement, I wanted to *see* why. The intuition that finally worked: split v into its
parallel part (which extends u) and its perpendicular part (which is wasted sideways) —
then only the parallel part ever counts as forward length. That single fact,
‖v‖ ≥ ‖v_∥‖, is the whole engine.

**The payoff:** I also discovered that this projection fact *is* Cauchy–Schwarz in
disguise, and that the dot product is the machinery behind the whole proof — which is
why inner products get promoted to the central tool later. Everything connects.

**Where:**
- `assets/triangle-inequality.tex` / `.pdf` — the full proof with figure, including
  the equality analysis (both inequalities must collapse, not one) and the C–S bridge.
  This doc went through two rounds of independent review — it's the sharp version
  underneath the casual one.
- `assets/triangle-intuition.html` — the two-case picture (parallel → equality,
  60° → strict) that the proof is built from.

### 3. Degrees of freedom and the unit sphere — why S^(n−1)?
**Why it went deep:** I kept thinking "moving along a circle changes both x and y, so
why is it 1-dimensional?" The answer that fixed it: DOF counts *independent knobs*, not
how many readouts change. The constraint ‖x‖ = 1 welds x and y together — nudge x and
y is forced — so one knob is all you get.

**The takeaway:** each constraint equation strips exactly one direction of motion, so
the sphere lives one dimension below its ambient space: S^(n−1) = the surface in Rⁿ
minus the one direction the norm equation locked down.

**Where:** `assets/unit-spheres.tex` / `.pdf` — the DOF argument, the S⁰/S¹/S² table,
and the four unit-sphere shapes (circle / diamond / square / ellipse) showing that
changing the norm changes what "distance 1" means.

### 4. Free vs fixed vectors — and whether [3,5] needs a reference
**Why it went deep:** the notes say "we just call them both vectors," but I couldn't
let it go — writing [3,5] feels like it needs a reference point. Turns out it has two
readings: as a *position* it needs an origin (and that origin is a free choice), as a
*displacement* it's a complete recipe — "3 along e₁, 5 along e₂" — that works from any
start. The math runs entirely on the displacement reading, which is why no formula
ever mentions an origin.

**Worth knowing:** this got checked by an independent review, which corrected me on
one point (the origin is *not* structurally special as a point — no point is) and
added a nice payoff: rigid transforms act on points as Rp + t but on free vectors as
just Rv. That's when the distinction stops being philosophy.

**Where:** `lecture-1-confusions.md` (free/fixed topic, incl. the norm
reference-dependence subtlety: same formula √(x₁²+x₂²), opposite meaning).

### 5. Norm = distance to the origin?
**Why it went deep:** it *is* true — every norm induces a metric d(x,y) = ‖x−y‖, and
setting y = 0 gives d(x,0) = ‖x‖, guaranteed for every norm because the zero vector
exists by axiom. But it's an intuition/corollary, not the definition (the definition
is the 3 axioms), and the book says it "on an intuitive level" before giving the
rigorous version. Keeping those apart matters.

**Where:** `assets/norm-section-deeplearningbook.txt` (verbatim §2.5 with the settled
reading), `lecture-1-confusions.md` (citation included).

### 6. The dot product — why xᵀy is secretly a projection
**Why it went deep:** the coordinate formula (multiply matching coordinates, add)
gives no hint that the dot product is about *projection* — how much of one vector
lies along another. The bridge is the law of cosines on the u, v, u−v triangle, and
the cleanest example is (2,1)·(1,√3): each axis contributes its own agreement
(2·1 = 2 along x, 1·√3 along y), and the dot product is the total. Also settled:
vectors are drawn tail-to-tail for reading θ, but u·v itself needs no picture — the
vectors are free.

**Where:** `assets/dot-product-axes.html` (the visualization), `lecture-1-confusions.md`
(the settled thread).

### The canonical reference

Everything in the norm / inner-product thread has a clean textbook home:
**Axler, *Linear Algebra Done Right*, 4e, Chapter 6** (free at
linear.axler.net/LADR4e.pdf). A snapshot of §6A with a quick-reference map
(definitions 6.1-6.21: dot product, inner product axioms, norm, orthogonal
projection, Cauchy-Schwarz, triangle inequality, parallelogram equality)
is in `assets/axler-ladr-ch6-inner-products.txt`, and `lecture-1-confusions.md`
cross-references each settled point to Axler's numbering.

---

## The one-line philosophy

> Surface-level understanding leaks the moment a problem looks slightly different.
> Every deep-dive in this repo is a place where the surface version failed me — the
> proof, the picture, and the gotcha log are the repairs.
