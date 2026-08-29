# Lecture 1 — Confusions & Gotchas

## Topic: Vector Space Axioms
**Mistake:** Listing "additive closure" twice — once as a property, once as an axiom.
**Gotcha:** The 3 properties (additive closure, scalar closure, zero vector) *define* a
vector space. The axioms (commutativity, associativity, distributivity, additive
inverse) *follow from* that definition — not a separate checklist.

## Topic: "A vector is a stack of numbers"
**Mistake:** Treating that as the *definition*.
**Gotcha:** It's a *representation*, only for Rⁿ. A vector is any element of a vector
space. Pₙ = polynomial as a function, but representable by its coefficient stack ∈ Rⁿ⁺¹.

## Topic: P = all polynomials is "infinite"
**Mistake:** Thinking that makes individual vectors infinite.
**Gotcha:** Infinity lives in the *space*, never in a single vector. Every polynomial has
finite degree → finite coefficient stack. C is the step beyond: sin(x) escapes
representation entirely.

## Topic: Is dim(P) "anything" / "either P₃ or P₁₀₀₀"?
**Mistake:** Reading unboundedness as ambiguity.
**Gotcha:** P contains *all* Pₙ at once (strictly bigger than every finite floor). Its
dimension is well-defined: **ℵ₀** (countably infinite). Unbounded degree = cause; ℵ₀ =
precise effect.

## Topic: Is P a matrix? a collection?
**Mistake:** Calling a collection a matrix.
**Gotcha:** Matrix = rectangular array of *numbers* (not a space). Vector space = a
*set* + addition + scalar multiplication with axioms.

## Topic: "No bound on degree"
**Mistake:** Reading that as "anything goes."
**Gotcha:** Membership is still sharp: you must BE a polynomial (sin x, 2ˣ ∉ P). Only
the *degree* is unbounded (5, 500, 5,000,000 — all welcome).

## Topic: Mapping notation `p : R → R`
**No mistake — get this right for free:**
- `: A → B` = domain left, range right (used again in norms: ‖·‖ : Rⁿ → R)
- `: x ↦ ...` = "maps to," the rule that computes

---

### The ladder (memorize the two boundaries)
| Space | Dimension | Why |
|---|---|---|
| Rⁿ | n | fixed length |
| Pₙ | n+1 (**off-by-one trap!**) | degree ≤ n → n+1 coefficients |
| P | ℵ₀ (countably infinite) | no degree cap |
| C | uncountably infinite | single vectors escape representation |

**One idea:** dimension = count of independent directions (basis size), NOT vector
length. In finite spaces they look the same; in P the basis {1, x, x², ...} never ends.

---

## Topic: "Degrees of freedom" of a shape (S⁰, S¹, ...)
**Confusion:** Moving along a circle changes both x and y (in R²), so why only 1 DOF?
**Core definition:** **DOF = being able to *independently* move / change the value of
that axis.** If changing x forces y to change too, they are *not* independent — so y is
not a separate DOF.
**Gotcha (the knob model):** DOF counts *independent knobs*, not how many readouts
change. On the circle there's only ONE knob — how far around the loop you are. Turning
it moves x AND y together because the constraint x² + y² = 1 *welds* them: nudge x and
y is forced to adjust. In free R² there are two knobs (x-slider, y-slider) that move
independently — that's why 2 DOF.
**Sharp test:** in how many directions can you step and stay on the surface? On the
circle: one tangent direction. In free R²: infinitely many in two perpendicular senses.
**Formula:** dim of surface = n − (number of independent constraints). For S¹ in R²:
2 − 1 = **1**. Dimension = motion *between* points (neighbors in a continuum), NOT how
many points the set contains — S⁰ = {−1, +1} has two elements but no continuum of
motion, so 0 DOF.

**Why the −1 in S^(n−1):** each independent constraint equation strips exactly ONE
direction of free motion. Sⁿ⁻¹ lives in Rⁿ: ambient dim (n) minus the norm equation
(one constraint) = n − 1. The superscript is "the surface in Rⁿ, minus the one
direction the constraint locked down."

## Topic: Free vs fixed vectors
**Gotcha:** Free = direction + magnitude only (location ignored, may translate freely);
fixed = same arrow but pinned to a start point (moving it makes a *different* vector).
Linear algebra uses free vectors (that's why a vector is just a "stack of
numbers" — no location). Real-world picks depend on context: velocity = free,
position = fixed, force = depends (fixed on a beam, loose on a free body).

**Fair question asked (settled, verified by independent review): does [3,5] need a
reference point?** Two readings: as a *position* (point) it needs an origin (and that
origin is a *free choice* — no point is canonical in position space); as a *displacement*
("3 along e₁, 5 along e₂") it's a complete recipe needing no origin. Cleanest framing:
**free-vector coordinates need a basis (axes) — no origin; point coordinates need a basis
AND an origin.** Operations (+, ·, ‖·‖) are defined on the *displacement* space; feeding
them points silently means feeding p − o. (So dotting two *positions* IS origin-dependent
— the formulas don't consult an origin, but the inputs may encode one.) ‖v‖ is invariant
under origin changes (and orthonormal basis changes).

**The notes' own conflation (the real source of the confusion):** calling a point a
"fixed vector" — affinely, a point isn't a vector at all. The notes use one word for
objects living in two different spaces; the student's confusion is legitimate, not a
reading failure. The distinction matters in practice: a rigid transform (R, t) acts on
points as Rp + t but on free vectors as just Rv — no translation (homogeneous coords:
[x,y,z,1] vs [x,y,z,0]; that trailing 0 kills the translation).

**Norm subtlety (settled): same formula √(x₁²+x₂²), opposite reference-dependence.** For
a *free* vector the norm is intrinsic length — 0,0 is just the parking spot we compute
from; move the origin, nothing changes. For a *fixed* point the same formula computes
distance-from-origin, which genuinely depends on the reference. In this course norms are
always taken on free vectors.

**"Norm = distance to the origin" — settled with citation.** The claim is TRUE but it is
an *intuition/corollary*, not the definition. Rigorous form: every norm induces a metric
d(x,y) = ‖x−y‖, and setting y = 0 gives d(x,0) = ‖x‖ — well-defined for every norm
because the zero vector is guaranteed by the vector-space axioms. What a norm *is*: the
3 axioms (definiteness, triangle inequality, homogeneity). The "distance to origin"
phrasing is the *position-reading* of x — the book literally says "the distance from the
origin to the point identified by x" — so keep "norm = length of a displacement" as the
primary reading. Primary reading: displacement length. Special case (position-reading):
distance to origin.

  Citation: Goodfellow, Bengio & Courville, *Deep Learning*, §2.5 "Norms" (free online:
  deeplearningbook.org). Verbatim section saved in `assets/norm-section-deeplearningbook.txt`.
  Also consistent with Wikipedia "Norm (mathematics)" and USC Math 555 lecture notes
  ("distance from x to 0"). Independent check (Claude CLI): verdict matches — corollary,
  not definition; zero vector guaranteed so claim holds for every norm.

## Topic: dot product = projection, and why the formula doesn't look like it
**The thing that clicked:** the dot product is really trying to get the projection of one
vector over another. cosθ shows it — ‖v‖cosθ *is* the part of v along u. The coordinate
formula xᵀy doesn't intuitively show that at all, but it's the same thing in disguise:
multiplying matching coordinates and adding is just the fast way to compute the
projection, and they speak the same language. The proof that they're equal is the law of
cosines on the triangle with sides u, v and u−v.

**Where they're placed:** tail to tail. That's the drawing convention for reading θ —
the angle is measured at the shared tail. But u·v itself doesn't need a picture; the
vectors are free, so any common tail gives the same answer.

**The worked example that made the sum visible:** we kept using (2,0) and (1,√3), but the
y-term was 0·√3 = 0, so only one axis was voting. With (2,1) and (1,√3):
- 2,1 is the decomposition of some vector, and so is (1,√3) — components along each axis.
- The idea is to get the measure of sameness along all axes: x-axis agrees by 2·1 = 2,
y-axis agrees by 1·√3 ≈ 1.73.
- u·v = 2 + √3 ≈ 3.73 = ‖u‖‖v‖cosθ = √5·2·cos(33.4°) — same number, both languages.
- Each axis contributes one rectangle of area; the dot product is the total area.
  Visual: `assets/dot-product-axes.html`.

**The whole arc at a glance (inner product ⟷ norm):**
- **Inner product** = a *generic* two-vectors-into-a-scalar operation, constrained by
  the 4 axioms (positivity, definiteness, additivity + homogeneity in first slot,
  conjugate symmetry). It measures *alignment*.
- **Dot product** = the flagship inner product: the case M = I (identity weighting),
  i.e. x·y = Σxᵢyᵢ. Every inner product on Rⁿ is xᵀMy for some symmetric
  positive-definite M; the dot product is M = I.
- **It induces the L2 norm:** ‖x‖₂ = √⟨x,x⟩ = √(x₁²+...+xₙ²). That's why they pair so
  well — the dot product was designed so its diagonal reproduces Euclidean length.
- **L2 is the only rotation-invariant norm** (up to scale). That's the deep payoff:
  the dot product ↔ L2 match is *the* geometry that stays put under rotation, which is
  why it's our everyday notion of space. The weighted norms (M ≠ I) are just L2
  recoordinatized (‖x‖_M = ‖M^½ x‖₂).
- **One-directional:** inner product ⟹ norm (always, via √⟨x,x⟩); norm ⟹ inner product
  only when the parallelogram law holds (Jordan–von Neumann; polarization recovers it).
  L₁, L∞ have no inner product — their length data is incompatible with any pairwise
  alignment.

---

## Reference: Axler, "Linear Algebra Done Right" 4e, Ch. 6 (inner products)

The canonical textbook treatment of everything in the norm / inner-product
thread. Free online: https://linear.axler.net/LADR4e.pdf. Snapshot of §6A
saved in `assets/axler-ladr-ch6-inner-products.txt`. Quick map:

- **6.1 dot product** — x·y = Σxᵢyᵢ, and the design fact: x·x = ‖x‖².
- **6.2 inner product axioms** — positivity, definiteness, additivity +
  homogeneity in first slot, conjugate symmetry (complex case; over R it's
  plain symmetry).
- **6.3(b) weighted inner products** — c₁w₁z₁ + ... + cₙwₙzₙ with cᵢ > 0.
  This is our made-up M norm, generalized — the book confirms it's legitimate.
- **6.7 norm** — ‖v‖ = √⟨v,v⟩, *defined* not assumed.
- **6.10 orthogonal** — ⟨u,v⟩ = 0.
- **6.12 Pythagorean theorem** — u ⟂ v ⟹ ‖u+v‖² = ‖u‖² + ‖v‖².
- **6.13 orthogonal decomposition** — u = (⟨u,v⟩/‖v‖²)v + w with w ⟂ v. This is
  the projection split our triangle-inequality proof was built from.
- **6.14 Cauchy–Schwarz** — |⟨u,v⟩| ≤ ‖u‖‖v‖; equality iff one is a scalar
  multiple of the other. Axler's proof uses the orthogonal decomposition,
  exactly the route our triangle-inequality doc takes.
- **6.17 triangle inequality** — ‖u+v‖ ≤ ‖u‖+‖v‖; equality iff one of u,v is a
  *nonnegative real* multiple of the other (the same fix Claude applied to our
  triangle-inequality.tex: parallel alone is not enough, v = −u breaks it).
- **6.21 parallelogram equality** — ‖u+v‖² + ‖u−v‖² = 2(‖u‖²+‖v‖²); one-line
  proof via the inner product (cross terms cancel), which is why it's the test
  separating inner-product norms from the rest.

---

### ✅ ARRIVED AT THIS SESSION: norms derived from an inner product

*(Was flagged "to revisit"; we worked through it — see the "inner product ⟷ norm"
summary above and the concept map.)* The made-up M norm ‖x‖_M = √(x₁² + 2x₂²) on R²
is a *weighted* ℓ₂ — first component squared (weight 1), second squared (weight 2).
It is an example of a **norm derived from an inner product**:

- ⟨x, y⟩_M = x₁y₁ + 2x₂y₂ (Lecture 2 §3.3 "Revisiting the Norm")
- ‖x‖_M² = ⟨x, x⟩_M = x₁² + 2x₂² — the norm comes *from* the inner product
- Some norms have inner products behind them (ℓ₂, M); some do NOT (ℓ₁, ℓ∞ — no
  inner product derives them)
- Consequences to revisit: a different inner product changes **what orthogonal means**
  (⟨x, y⟩_M = 0 is not the same as 90° in the usual picture), and changes the unit
  sphere shape (M → ellipse, vs circle for ℓ₂)

**Where it will show up:** Lecture 2 §3.3 (made-up inner product), and later in the
course when a different norm/inner product becomes genuinely useful (the notes say
"there are a few important cases where it is useful to have a different norm and inner
product"). Revisit when Lecture 2's norm section comes up.