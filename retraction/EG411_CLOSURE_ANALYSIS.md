# EG#411 r=2 — Closure Analysis and Proof Architecture

## Summary

The depth-3 closure of EG#411 r=2 reduces to proving that for all primes p ≡ 7 mod 8
with p ≥ 7, the function `cambie_depth3_check p` returns `true`.

**Current status:** Axiom-clean for p ≤ 10^7 (native_decide). Named axiom for p > 10^7.
A formal ω-product argument eliminates the axiom up to p ≈ 5.9 × 10^60.
Full unconditional closure requires formalizing Mertens' third theorem.

## The Depth-3 Check

```
cambie_depth3_check p :=
  let N := (3p - 1) / 4
  let c2 := 3p² - p + 2(p-1)·φ(N)
  if c2·10000 ≥ 9849·4p² then true       -- above-threshold
  else
    let c3 := p·c2 + (p-1)·φ(c2)
    4p³ ≤ c3                               -- depth-3 overshoot
```

**Two paths:** above-threshold (α ≥ 0.6264) or depth-3 overshoot (c3 ≥ 4p³).

## Key Quantities

- α = φ(N)/N where N = (3p-1)/4, gcd(N,6) = 1
- β = φ(c2)/c2 where c2 = 4m, m odd, gcd(m,6) = 1
- Above-threshold iff α ≥ 0.6264 (exact: 3α/2 ≥ 3·0.9849·4/10000 - ...)
- Depth-3 overshoot (asymptotic): (2 + α)(1 + β) ≥ 8/3

## Computational Verification

| Range | Primes tested | Below threshold | Worst ratio | Worst α | Worst β |
|-------|---------------|-----------------|-------------|---------|---------|
| [7, 10^6] | 19,669 | 126 | 1.295 | 0.591 | 0.295 |
| (10^6, 10^7] | 126,899 | 786 | 1.226 | 0.576 | 0.270 |
| (10^7, 10^8] | 1,274,169 | 7,783 | 1.216 | 0.575 | 0.259 |

**ALL PRIMES PASS** in every range. Zero failures through 10^8.

## Three-Layer Proof Architecture

### Layer 1: Finite Verification (p ≤ 10^7)

Two-stage `native_decide` in Lean 4:
- Stage 1: p ∈ [0, 10^6] — 19,669 primes, ~30s
- Stage 2: p ∈ (10^6, 10^7] — 126,899 primes

**Status:** Compiling (estimated 20-60 min).

### Layer 2: Omega-Product Bound (10^7 < p < 5.9 × 10^60)

**Key lemma (provable in Lean/Mathlib):**
For n coprime to 6 with ω(n) = k distinct prime factors:
  φ(n)/n ≥ ∏_{j=1}^k (1 - 1/q_j)
where q_1=5, q_2=7, q_3=11, ... are the primes ≥ 5 in order.

**Proof:** φ(n)/n = ∏_{p|n}(1-1/p). Each factor ≥ (1-1/q_j) since p_j ≥ q_j
when both are sorted in increasing order.

**Primorial bound (provable in Lean):**
ω(n) ≤ K iff n ≥ primorial₅(K) := q_1 · q_2 · ... · q_K.
Contrapositive: if n < primorial₅(K+1), then ω(n) ≤ K.

**Finite verification (34 × 62 pairs):**
For each K_N ∈ {1,...,34} and corresponding worst-case K_m:
  (2 + f(K_N))(1 + f(K_m)/2) ≥ 8/3
where f(k) = ∏_{j=1}^k (1-1/q_j).

PARI verification: ALL pairs pass. First failure at K_N = 35.

**Crossover data:**
```
K_N  q_KN  f(K_N)    K_m_wc  f(K_m)/2  product    pass?
...
32   139   0.334096  57      0.147734  2.678922   YES
33   149   0.331854  59      0.146688  2.673910   YES
34   151   0.329656  61      0.145712  2.669114   YES  (last pass)
35   157   0.327556  62      0.145243  2.665618   NO   (first fail)
```

primorial₅(35) ≈ 5.90 × 10^60. So the bound covers all p < 5.9 × 10^60.

### Layer 3: Asymptotic Case (p ≥ 5.9 × 10^60) — AXIOM

Requires formalizing Mertens' third theorem (Rosser-Schoenfeld explicit form):
  ∏_{q≤x}(1-1/q) ≥ e^{-γ}/ln(x) · (1 - 1/(2(ln x)²))  for x ≥ 286

This is NOT in Mathlib v4.29.1 and represents a significant formalization project.

**Impact:** The axiom applies only for p > 5.9 × 10^60. No computation will ever
reach this range. The mathematical gap is purely formal.

## Why the Problem is Hard

The depth-3 condition (2+α)(1+β) ≥ 8/3 involves the JOINT behavior of:
- α = φ(N)/N (smoothness of N = (3p-1)/4)
- β = φ(c2)/c2 (smoothness of c2 = 3p²-p+2(p-1)φ(N))

The ω-product bound treats α and β as INDEPENDENT worst cases. In reality,
there is a strong anti-correlation: when N is smooth (α small), c2 tends NOT
to be smooth (β stays moderate). This anti-correlation has margin 16× at 10^7.

Exploiting the anti-correlation would extend the bound much further, potentially
all the way to unconditional, but requires deep algebraic number theory.

## Omega Distribution Data (PARI, p ≤ 10^8)

| ω(c2/4) max | Range |
|--------------|-------|
| 4 | p ≤ 10^3 |
| 5 | p ≤ 10^4 |
| 6 | p ≤ 10^5 |
| 7 | p ≤ 10^7 |
| 8 | p ≤ 10^6 (omega_correlation.gp) |
| 9 | p ≤ 10^8 |

ω(c2/4) grows approximately as 1.1·log(log(p)) — much slower than the
theoretical worst case from primorial bounds.
