# universal-tree-embedding

SMT-based computation of minimum-edge substrates for universal
arc-disjoint binary tree embedding, with dilation analysis across
six regular directed graph families.

---

## Overview

Given *n*, the **universal binary tree embedding problem** asks for
the sparsest directed graph G_S such that every *n*-vertex binary
tree admits an arc-disjoint embedding into G_S with bounded
dilation (maximum hops per tree edge).

This repository contains the solver code and raw results for two
complementary approaches studied in the thesis
*Design of On-Chip Interconnects* (M.Tech, IIT Dharwad, 2026).

| Chapter | Setting | Method |
|---|---|---|
| Strict (m=1, χ=1) | Each tree edge → single arc; G_S has exactly *n* vertices | SMT optimisation over Z3 |
| Relaxed (m≥1, χ≥1) | Each tree edge → directed path of length ≤ m in a regular substrate | Feasibility solver over six families |

---

## Results at a Glance

### Strict Embedding (Chapter 3)

| n | \|K_n\| edges | Minimum edges | Reduction |
|---|---|---|---|
| 3 | 6 | 3 | 50.0% |
| 4 | 12 | 4 | 66.7% |
| 5 | 20 | 7 | 65.0% |
| 6 | 30 | 9 | 70.0% |
| 7 | 42 | 11 | 73.8% |
| 8 | 56 | 13 | 76.8% |

Minimal substrates are asymmetric, non-regular, and follow no
closed-form pattern. Solver runtime for n=8: ~10–11 days on a
single machine.

### Relaxed Embedding — Minimum Dilation by Family (Chapter 4)

No family requires m > 2 across n = 3–21.
The crossed cube CQ_d achieves m = 1 for the widest range at
every tested dimension d ∈ {2, 3, 4}, strictly dominating the
hypercube Q_d while matching it in vertex count, degree, and edge
count.

| Family | m = 1 cases (n=3–20) | m = 2 cases | Notes |
|---|---|---|---|
| Crossed Cube | 16 | 2 | Best; sole unit-dilation substrate |
| Hypercube | 11 | 7 | Parity obstruction at n > (3/4)·2^d |
| Torus | 7 | 11 | Non-monotone dilation profile |
| Mesh | 2 | 16 | Fewest edges at every n |
| De Bruijn | 0 | 18 | k=2 optimal throughout |
| Kautz | 0 | 18 | Finer granularity than de Bruijn |
