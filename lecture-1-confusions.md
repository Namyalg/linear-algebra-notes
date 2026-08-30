# Lecture 1 — Confusions & Gotchas

## How topics build on each other (and where each has a home)

**One-glance map:** [`assets/concept-map.pdf`](assets/concept-map.pdf) — mind map + the
exact concept-à-concept chain (editable source kept locally at `assets/concept-map.tex`).
This section is the text version. The boxed items (▸) are the canonical textbook
references that match what's settled here.

1. **Vector space** → dimension → free/fixed
   - Vector space axioms: **Axler LADR 4e, §1** (free: linear.axler.net/LADR4e.pdf).
   - Dimension: Axler Ch. 2. Note Axler only says "infinite-dimensional" — he never
     assigns cardinalities, so dim(P) = ℵ₀ (correct in its own right, any Hamel basis
     has that size) isn't sourced from him; it's our own (verified) claim.
   - Free vs fixed, [3,5] reference: settled here (see topic below).
2. **Norm** → unit sphere → unit vector
   - Norm, map/range notation: **Axler §6A (6.7)**; **Goodfellow et al., *Deep
     Learning*, §2.5** (snapshot: `assets/norm-section-deeplearningbook.txt`).
   - Unit sphere, DOF, S^(n−1): `assets/unit-spheres.tex`-derived PDF.
3. **Triangle inequality** ← projection split ← Cauchy–Schwarz
   - Proof + figure + engine (‖v_∥‖ ≤ ‖v‖ = C–S): `assets/triangle-inequality.tex`
     (PDF) and `assets/triangle-intuition.html`.
   - Textbook match: **Axler §6A (6.14, 6.17)**.
4. **Inner product** ↔ **norm** (the whole arc) → parallelogram law
   - Dot product = projection, xᵀy = ‖x‖‖y‖cosθ, parallelogram: `assets/dot-product-axes.html`,
     `assets/parallelogram.html`.
   - The arc summary and L2 = only rotation-invariant norm: in this doc (below).
   - Textbook match: **Axler §6A (6.1, 6.2, 6.10–6.21)** — snapshot
     `assets/axler-ladr-ch6-inner-products.txt`.
   - Also **Strang, *Introduction to Linear Algebra*** (Ch. 1–2) and **Lay**, *Linear
     Algebra and its Applications* (Ch. 6) for the same material at a gentler pace.

Everything referenced here lives in this repo (notes + assets) except the textbooks,
which are the external canonical sources.

---

## Topic: Vector Space Axioms
**Mistake:** Listing "additive closure, scalar closure, zero vector" as if they alone
*define* a vector space, and the axioms follow from them.
**Gotcha:** That 3-item list is the **subspace criterion** — it only works when an
*ambient* vector space already exists, in which case the other axioms are *inherited*.
As a standalone definition it's insufficient: e.g. define a·v = 0 for all scalars a;
closure + zero hold and yet 1·v = v fails, so it's not a vector space. The full set of
axioms (including the linking ones 1·v = v and (ab)v = a(bv)) IS the definition of a
vector space; the 3-property check is the subspace test.

## Topic: "A vector is a stack of numbers"
**Mistake:** Treating that as the *definition*.
**Gotcha:** It's a *representation*, and it works in *any* finite-dimensional space
once a basis is fixed — not just Rⁿ. A vector is any element of a vector space. Pₙ =
polynomial as a function, but representable by its coefficient stack ∈ Rⁿ⁺¹.

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
- `: A → B` = domain left, **codomain** right (range ⊆ codomain: e.g. ‖·‖ : Rⁿ → R has
  range [0,∞), not all of R)
- `: x ↦ ...` = "maps to," the rule that computes

---

### The ladder (memorize the two boundaries)
| Space | Dimension | Why |
|---|---|---|
| Rⁿ | n | fixed length |
| Pₙ | n+1 (**off-by-one trap!**) | degree ≤ n → n+1 coefficients |
| P | ℵ₀ (countably infinite) | no degree cap |
| C | uncountably infinite | no countable basis (Hamel basis uncountable) |

**One idea:** dimension = count of independent directions (basis size), NOT vector
length. In finite spaces they look the same; in P the basis {1, x, x², ...} never ends.
(For C: no countable basis exists; e.g. {e^{λx} : λ ∈ R} is an uncountable independent
family. A single function like sin(x) isn't "unrepresentable" — it just isn't a finite
combination of powers of x.)

---

## Topic: "Degrees of freedom" of a shape (S⁰, S¹, ...)
**Confusion:** Moving along a circle changes both x and y (in R²), so why only 1 DOF?
**Core definition:** **DOF = dimension of the space of allowed/motions — how many
independent directions you can move, i.e. how many knobs you can turn on their own.**
If changing x forces y to change too, they are *not* independent — one knob, one DOF
(so the circle's single DOF is an *angle*, not an axis).
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
- Each axis contributes one rectangle of *signed* area; the dot product is the total
  (terms can be negative — (−1,√3)·(2,1) < 0).
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
  L₁, L∞ have no inner product (for n ≥ 2); in dimension 1 every L_p coincides with L₂.
  Their length data is incompatible with any pairwise alignment.

**The closing statement (verbatim, as settled):** *The dot product and the norm answer
different questions but carry the same information. The dot product asks "how similar are
two vectors, summed over every axis" — decompose each into components, multiply
axis-by-axis, add. Point it at the same vector and everything aligns, so you get the sum
of its squared components; the norm is the square root of that — its size. The dot product
is one inner product (the identity-weighting one, pairwise multiply); the norm is what
that inner product induces when you feed a vector to itself.*

## Topic: What makes an ``inner product space''
**Gotcha:** "inner product space" = **a vector space PLUS an inner product on it**
(Axler 6.4). The vector space supplies the set + addition + scalar multiplication; the
inner product is *additional* structure layered on top — a function that takes an
ordered pair of vectors to a scalar (Axler 6.2) and satisfies the 4 inner-product
axioms: positivity, definiteness, additivity + homogeneity in the first slot, and
conjugate symmetry. Both parts are required: an inner product without a vector space
is meaningless (you must be able to add/scale its inputs), and a vector space without
an inner product is just a vector space (no angles, no length).

So the chain of "spaces," each adding structure:
- **vector space** = set + addition + scalar mult (the 8 axioms)
- **normed space** = vector space + a norm ‖·‖ (size)
- **inner product space** = vector space + an inner product ⟨·,·⟩ (alignment), which
  also induces a norm ‖v‖ = √⟨v,v⟩ — so every inner product space is automatically a
  normed space.
- **metric space** = set + a distance d(x,y) (needs no vector structure at all).

Slight abuse of language to be aware of: when people say "V is an inner product
space," the inner product is "lurking nearby or clear from context" — for "Fⁿ" it's
the Euclidean inner product unless otherwise stated (Axler 6.4/6.5).

## Topic: Orthogonal decomposition (formalized, Axler 6.13)
**The statement.** For u, v ∈ V with v ≠ 0, u splits *uniquely* into a part along v
and a part orthogonal to v:

    u = cv + w, with ⟨w, v⟩ = 0, where c = ⟨u,v⟩/‖v‖²
    u = (⟨u,v⟩/‖v‖²)·v  +  (u − (⟨u,v⟩/‖v‖²)·v)
        └── parallel part (proj_v(u)) ──┘   └── orthogonal part ──┘

**Why c = ⟨u,v⟩/‖v‖² (derived, not guessed):** we want the leftover w = u − cv to be
orthogonal to v:

    ⟨u − cv, v⟩ = 0  ⟹  ⟨u,v⟩ − c⟨v,v⟩ = 0  ⟹  c = ⟨u,v⟩/‖v‖²   (v ≠ 0 so ‖v‖² ≠ 0)

The scalar is *solved for* by the single requirement "the leftover has no v-component"
— and because v ≠ 0 fixes c uniquely, the decomposition is unique.

**Same piece, three names** (so notation never surprises you):
- the along-v part = proj_v(u) = cv = (⟨u,v⟩/‖v‖²)v = ⟨u, v̂⟩v̂
- the orthogonal part = w = u − proj_v(u) = the "rejection" = v_⟂

**Pythagoras applies** (the two pieces are orthogonal): ‖u‖² = ‖proj_v(u)‖² + ‖w‖².
This is the engine our triangle-inequality proof used, and it's exactly how Axler
proves Cauchy–Schwarz in one line (drops the ≥ 0 term).

**Worked example:** u = (2,1), v = (1,√3). ⟨u,v⟩ = 2·1 + 1·√3 = 3.732, ‖v‖² = 4,
c = 3.732/4 = 0.933. proj_v(u) = 0.933·(1,1.732) = (0.933, 1.616);
w = (2,1) − (0.933,1.616) = (1.067, −0.616). Check: ⟨proj,w⟩ ≈ 0.996 − 0.995 ≈ 0 ✓
(they're perpendicular); ‖proj‖² + ‖w‖² ≈ 3.48 + 1.52 ≈ 5.00 = ‖u‖² ✓ (Pythagoras).

## Topic: Why 2 independent vectors span R² (the whole argument)
- Condition: u, v not multiples of each other ⟺ det = u₁v₂ − u₂v₁ ≠ 0.
- det ≠ 0 ⟺ the system (au₁+bv₁, au₂+bv₂) = (w₁,w₂) has a UNIQUE solution for
  EVERY w — nonzero denominator means always solvable.
- Hence every w ∈ R² = au + bv → they span R² → independent + spanning = basis.
- One condition, three hats: "not parallel" ⟺ "det ≠ 0" ⟺ "every w built uniquely."
- 2-vector specific: det is the whole test. For larger sets, need the general test
  (Σcᵢvᵢ = 0 ⟹ all cᵢ = 0) — no single number does it.

## Topic: Basis & dimension (Lecture 2 §5.4)
**Basis = the minimum set of vectors that span M** (no redundancy). "Minimum" =
linearly independent = can't remove any vector and still span M. Either phrasing works:
a basis is a spanning set with zero redundancy.

**dim(M) = number of vectors in ANY basis of M = number of independent directions = m.**
It's an exact *equality*, not a bound — once dim(M) = m, every basis has exactly m
vectors, period. "Minimum" means smallest *size*, not "a specific set" — many different
bases ({(1,0),(0,1)} vs {(0.6,0.8),(0.8,0.6)}) all have the same count m.

**dim(Rⁿ) = n.** At most n independent directions (only n coordinate slots), and it's
*achievable* (the canonical basis e₁..eₙ gives n independent directions that span
everything). So every basis of Rⁿ has exactly n vectors.

**Guard — a subspace's m directions do NOT have to align with m coordinate axes.** In
Rⁿ's canonical basis one slot = one direction, but a general subspace weaves through
coordinates: the tilted plane M = {x + y + z = 0} in R³ is 2-D with basis {(1,−1,0),
(1,0,−1)} — two independent directions that cut diagonally across all three
coordinates. So dim = m independent *directions*, not "m coordinate axes." The
one-slot-one-direction picture is the clean special case (Rⁿ itself), not the general
definition.

## Topic: Span (Lecture 2 §5.1)
**Definition:** for X = {x₁,...,xₘ}, span(X) = the set of ALL linear combinations of X:

    span(X) = { a₁x₁ + ... + aₘxₘ : a₁,...,aₘ ∈ R }

One linear combination = ONE vector; the span = THE SET of all of them. Two ways to
hold it: (1) "the set of all vectors you can build from X," or (2) "how much does X
span / cover" — the extent of the space it reaches.

**Key facts:**
- span(X) is always a *subspace* (closed under + and scalar · by construction — the
  Lecture 1 closure idea resurfacing).
- "How much" is answered by **dimension**: dim(span(X)) = number of *independent*
  vectors in X. span{(1,0)}=line→1; span{(1,0),(0,1)}=plane→2; adding (2,3) to the
  latter adds nothing (already reachable) → still 2.
- Not every vector in X grows the span: if a vector is already in the span, it's
  *redundant* — which is exactly the doorway into **linear independence** (next).

## Topic: Basis + coefficients — the one-line result
**n linearly independent vectors in Rⁿ ⟹ automatically a basis** (independence + full
count leaves nothing missing). To find coefficients of any target w: set up the system
w = A·coeffs and solve — Cramer's/determinants for small n, Gaussian elimination for
bigger. det ≠ 0 ⟺ invertible ⟺ unique solution.
**Guardrails:** needs exactly n vectors in Rⁿ; fewer span only a subspace. Single
2×2 determinant shortcut only works for square (n×n) systems.

## Gram–Schmidt: subtract ALL the parallel parts, one axis at a time
**The plan:** for each new vector, properly remove the parallel part of EVERY axis
already built (u₁, u₂, ...), leaving a piece perpendicular to each, then normalize it.
Specifically: w = v − proj_u₁(v) − proj_u₂(v) − ... (subtract parallel part of each
axis already present, get something perp to every one of them), then u = w/‖w‖.

**Trap — "sum of projections" vs "projection of the sum":**
- SUM OF PROJECTIONS proj_u₁(v)+proj_u₂(v): keep axes separate, project onto each,
  then add the peels. LEGAL only because u₁ ⟂ u₂ (no interference). ✓
- PROJECTION OF THE SUM proj_(u₁+u₂)(v): merge axes into one slanted line, single
  drop onto it. ✗ WRONG.
- Why: u₁+u₂ = ONE line ⇒ "perp to the sum" = ONE constraint. But being orthogonal to
  the covered set needs a constraint PER AXIS (u₁, u₂, ...) = TWO constraints. A single
  slanted line enforces only one perpendicularity, leaving residue along all mixed axes.
  The sum erases the 2→1 dimensionality.
- The EXACT difference: proj_u₁(v)+proj_u₂(v) = proj_(u₁+u₂)(v) + proj_(u₁−u₂)(v).
  Sum-of-projections = full v (both rotated pieces); projection-of-sum = only the
  diagonal piece — it DROPS the anti-diagonal piece proj_(u₁−u₂)(v), which is the
  whole difference. Equal only when v lies on the diagonal (perp component = 0).
- Where (1,1)/(1,−1) come from: u₁+u₂ and u₁−u₂ are the SQUARE'S DIAGONALS = a second
  orthonormal frame, the axes rotated 45° (equal-length orthogonal vectors give a
  perpendicular sum & difference: (u₁+u₂)·(u₁−u₂) = ‖u₁‖²−‖u₂‖² = 0). The identity's
  RHS is just v decomposed in that rotated frame: sum-of-projections = both terms,
  projection-of-sum = only the diagonal term.
- Visual: `assets/projection-sum-vs-vector-sum.html`.

**"Same line, different lengths" (why the leftover direction is fixed):** the
leftover is EXACTLY the projection of xₖ onto the perpendicular space — (xₖ·p̂)·p̂ in
2D. Projection onto a line always lands on that line; only the scalar (xₖ·p̂) varies
with xₖ, changing the length (and sign), never the direction. Intuition: after u₁ is
"horizontal," p̂ is the only perpendicular direction left. Visual:
`assets/perp-line-leftovers.html`.
- Gram–Schmidt overall: `assets/` (worked 2D example in confusions thread).

**Gotcha — dot product is a SCALAR, always.** (1,2,1)·(1,1,0) = 1·1 + 2·1 + 1·0 =
**3**, a single number — NOT (1,2,0). Component-wise product (keeping each slot
separate) is a different operation; the dot product *sums* the matching products.
In proj_a(v) = (v·a)/(a·a)·a, the scalar (v·a) then scales the WHOLE direction
vector a. Slip's fingerprint: subtracting the wrong projection leaves a leftover
that fails the orthogonality check (dot ≠ 0).

**Worked 3D example** (v₁=(1,1,0), v₂=(1,0,1), v₃=(1,1,1)):
```
u₁ = (1/√2, 1/√2, 0)
u₂ = (1/√6, −1/√6, 2/√6)
u₃ = (−1/√3, 1/√3, 1/√3)
```
Step 3 does the double peel: proj_u₁(v₃)=(1,1,0), proj_u₂(v₃)=(1/3,−1/3,2/3),
w₃ = v₃ − both = (−1/3,1/3,1/3), normalize → u₃.
**Gotcha (trap in this example):** √(2/3) = 2/√6 is a *scalar* — it's v₃·u₂ (the
projection coefficient) AND u₂'s third coordinate, but NOT part of u₃. u₃'s third
component is 1/√3, same magnitude as the rest. Mistaking the projection scalar for a
coordinate is the classic slip. (Flipping any uᵢ → −uᵢ is still valid.)

**Worked 3D example #2** (v₁=(1,1,0), v₂=(1,0,1), v₃=(1,2,1)): same u₁, u₂; the
double peel does real work: proj_u₁(v₃)=(3/2,3/2,0), proj_u₂(v₃)=(1/6,−1/6,1/3),
w₃ = v₃ − both = (−2/3,2/3,2/3), u₃ = (−1/√3,1/√3,1/√3).
**Both subtractions, always:** v₃ − proj_u₂ ONLY gives (5/6,13/6,2/3) — wrong, still
has a u₁ component (and fails the dot-against-u₁ check). wₖ needs every projection
subtracted.

**In R³, u₃ is FORCED once u₁, u₂ are fixed:** u₃ = ±(u₁ × u₂). Any v₃ not lying in
the u₁u₂-plane yields the same u₃ up to sign — so two different v₃'s giving the same
u₃ is NOT an error.

**The one-line understanding:** for each incoming xₖ, project it onto EVERY already-
built u (i.e. compute each parallel part), subtract them ALL — the leftover is the
perpendicular part, which becomes the next u after normalizing. Goal: all u's pairwise
orthogonal and unit length = orthonormal basis of the same span.

## Topic: Orthonormal vs non-orthogonal — why orthonormalize
- **Basis ⟹ MUST be independent** (definition). Orthogonality is optional, an upgrade.
- **Superposition happens in every basis** (w = Σaᵢvᵢ always). Orthogonality is NOT about
  "fewer pieces" — it's about how *easy* the split is to find.
- **Orthonormal ⟹ coefficient = projection** = one dot product (aᵢ = w·v̂ᵢ), read off
  alone. Axes don't overlap.
- **Non-orthogonal ⟹ coefficient ≠ projection** — axes overlap, coefficients entangled,
  you must solve the system. (Proj of (3,5) onto (2,1) = 2.2, but TRUE coefficient = 1/3.)
- Visual: `assets/basis-coordinates-visual.html`.
- **What orthogonality kills is axis overlap**, not "n coefficients per vector."
  Coordinates always number n per vector; the overlap is what entangles the solve.

## Topic: Independence ⟹ unique solve ⟹ basis (the whole arc, one line)
**The chain:** independence (n vectors in Rⁿ) ⟹ det ≠ 0 ⟹ system uniquely solvable for
every target ⟹ spans all of Rⁿ ⟹ basis.

- **Independence = the coefficient map is injective** (only all-zero scalars give 0).
- **n independent vectors in Rⁿ = full count, no redundancy** → nothing can be missing
  (no room for a target to hide) → spans everything.
- **det is the computational face of the same fact**: nonzero det = legal division in
  Cramer's rule (A⁻¹ = (1/det)·adjugate) = exactly one true answer.
- **det = 0** ⟺ dependent ⟺ no unique solution (contradiction → none, or redundant →
  infinitely many).
- **Caveat:** the "automatic basis" needs the count = n. m < n independent vectors span
  only an m-dim subspace, not all of Rⁿ.

## Topic: Systems + Cramer's rule + matrices refresher
**Setting up:** w = a₁v₁+...+aₙvₙ becomes n equations (one per coordinate), n unknowns.

**Example:** a(1,2)+b(3,4)=(8,9) ⟹
```
a + 3b = 8
2a + 4b = 9
```
Solve by elimination → a = −2.5, b = 3.5 (check: (−2.5,−5)+(10.5,14) = (8,9) ✓).

**Why the formula = Cramer's rule:** A x = w, x = A⁻¹w, and A⁻¹ = (1/det)·adjugate — so
det is the denominator. a = (w₁v₂ − w₂v₁)/(u₁v₂ − u₂v₁) = det(w,v)/det(u,v).

**Matrix reading:** A maps the unit square to the parallelogram of its columns; det =
its area-scaling factor. det = 0 ⟺ flattens plane to a line ⟺ not invertible ⟺ no
unique solution. det ≠ 0 ⟺ invertible ⟺ unique solve ⟺ spans.

**Higher dims:** concept is dimension-independent, but the one-scalar det test only
works for a *square* basis (n vectors in Rⁿ). For other shapes use rank / the
homogeneous test (Σcᵢvᵢ = 0 ⟹ all zero). For big n, replace hand substitution with
Gaussian elimination (same idea, standardized, no arithmetic bookkeeping).

## Technique: the "drop the non-negative term" move
**The template** (seen in Cauchy–Schwarz, the triangle inequality, and everywhere):
write an exact identity, notice a term is ≥ 0, drop it, and get a ≥ bound.

    a = b + c,   c ≥ 0   ⟹   a ≥ b

**How it proves Cauchy–Schwarz (decomposition route):**
- u = proj_v(u) + w with w ⟂ v; Pythagoras: ‖u‖² = ‖proj_v(u)‖² + ‖w‖².
- ‖w‖² ≥ 0, so drop it: ‖u‖² ≥ ‖proj_v(u)‖² = |⟨u,v⟩|²/‖v‖².
- Rearrange + sqrt → |⟨u,v⟩| ≤ ‖u‖‖v‖. Equality iff w = 0 (u ∥ v).

**How it proves the triangle inequality:** the intermediate step 2Re⟨u,v⟩ ≤ 2‖u‖‖v‖
is C–S, which itself came from a dropped ≥ 0 term.

**The DNA of almost every inequality proof here:** either (a) drop a non-negative
term, or (b) "some square is ≥ 0" (the quadratic route expands 0 ≤ ‖u−tv‖² and uses
"discriminant ≤ 0 since a square ≥ 0"). When reading a proof, scan for which term is
being dropped / which square is ≥ 0; that's the engine.

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

**Where it will show up:** Lecture 2 §3.3 "Dot Product" (incl. the "Revisiting the
Norm" subsection, which derives the made-up norm from the made-up inner product;
verified in lecture_2.pdf). The notes confirm: "There are a few important cases where
it is useful to have a different norm and inner product, so we will revisit this
concretely when the time comes."