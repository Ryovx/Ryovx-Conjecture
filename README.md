<div align="center">
   
# The Ryovx Conjecture

**A Novel Discrete Dynamical System Combining Digit Reversal with Parity-Dependent Arithmetic Operations**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Status: Conjecture](https://img.shields.io/badge/Status-Conjecture-orange.svg)]()
[![Preprint](https://img.shields.io/badge/Preprint-Zenodo-blue.svg)](https://zenodo.org/)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.XXXXXXX-blue.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
[![Language: LaTeX](https://img.shields.io/badge/Paper-LaTeX-green.svg)]()
[![Language: C](https://img.shields.io/badge/Code-C-blue.svg)]()
[![Language: Lean 4](https://img.shields.io/badge/Formalization-Lean%204-purple.svg)]()
[![Python](https://img.shields.io/badge/Analysis-Python-yellow.svg)]()

[![AMS 11A63](https://img.shields.io/badge/AMS-11A63-red.svg)](https://mathscinet.ams.org/msc/msc2020.html)
[![AMS 37P99](https://img.shields.io/badge/AMS-37P99-red.svg)](https://mathscinet.ams.org/msc/msc2020.html)
[![AMS 37B20](https://img.shields.io/badge/AMS-37B20-red.svg)](https://mathscinet.ams.org/msc/msc2020.html)
[![AMS 11B75](https://img.shields.io/badge/AMS-11B75-red.svg)](https://mathscinet.ams.org/msc/msc2020.html)
[![AMS 68Q99](https://img.shields.io/badge/AMS-68Q99-red.svg)](https://mathscinet.ams.org/msc/msc2020.html)

[![PRs: Closed](https://img.shields.io/badge/PRs-Closed%20by%20Invitation-red.svg)]()
[![Contributions: Welcome via Issues](https://img.shields.io/badge/Contributions-Issues%20Only-yellow.svg)]()

</div>

---

## ⚠️ Important Notice

> **This repository contains a mathematical CONJECTURE, not a proven theorem.**
>
> The Ryovx Conjecture has been:
> - ✅ **Formulated** rigorously
> - ✅ **Verified computationally** on 1,290+ numbers across 8 families
> - ✅ **Structured** with a conditional proof framework
> - ❌ **NOT YET PROVEN** in full generality
>
> Any use of this work in further research, publications, or derivative systems
> must explicitly acknowledge that the conjecture remains open. See
> [Status](#current-status) below.

---

## 📖 Table of Contents

- [What is the Ryovx Conjecture?](#what-is-the-ryovx-conjecture)
- [The Map T](#the-map-t)
- [Statement of the Conjecture](#statement-of-the-conjecture)
- [Examples](#examples)
- [Computational Verification](#computational-verification)
- [Theoretical Framework](#theoretical-framework)
- [Current Status](#current-status)
- [Repository Structure](#repository-structure)
- [What Has Been Done](#what-has-been-done)
- [What Remains to Be Done](#what-remains-to-be-done)
- [Applications and Derivative Works](#applications-and-derivative-works)
- [References](#references)
- [Citation](#citation)
- [License](#license)
- [Contact](#contact)
- [Contributing](#contributing)

---

## 🧭 What is the Ryovx Conjecture?

The **Ryovx Conjecture** is a novel discrete dynamical system defined on the
natural numbers. It combines two well-known mathematical operations:

1. **Digit reversal in base 10** — reversing the decimal digits of a number.
2. **Parity-dependent arithmetic** — performing different operations based on
   whether a number is odd or even.

The conjecture states that **for all parameters `a < b`, every trajectory
converges** — either entering a cycle or reaching zero — and **never diverges
to infinity**.

The system is named after the author's research project, *Ryovx*.

---

## 🔁 The Map T

### Digit Reversal Function

For a natural number `x` with `L` decimal digits, written as:

```
x = a₀ · 10^(L-1) + a₁ · 10^(L-2) + ... + a_{L-1} · 10^0
```

the **digit reversal function** `R: ℕ → ℕ` is defined by:

```
R(x) = a_{L-1} · 10^(L-1) + a_{L-2} · 10^(L-2) + ... + a₀ · 10^0
```

with the convention `R(0) = 0`.

**Examples:**

| x | R(x) |
|---|---|
| 10 | 1 |
| 543 | 345 |
| 1200 | 21 |
| 12345 | 54321 |
| 1 | 1 |

### The Ryovx Map

For `a, b ∈ ℕ` with `a < b`, the **Ryovx map** `T: ℕ₀ → ℕ₀` is defined by:

```
T(x) = { R(a · x)           if x is odd
       { R(⌊x / b⌋)         if x is even
```

where `⌊·⌋` denotes the floor function (Euclidean division).

**Equivalently**, using the parity indicator:

```
T(x) = R( a·x·[x odd] + ⌊x/b⌋·[x even] )
```

---

## 🎯 Statement of the Conjecture

> **Conjecture (Ryovx).**
>
> For all `a, b ∈ ℕ` with `a < b`, and for all `x ∈ ℕ₀`, the trajectory
> `{T^(k)(x)}_{k=0}^∞` either:
>
> 1. **enters a cycle** after finitely many steps, or
> 2. **reaches 0** after finitely many steps.
>
> In particular, **the trajectory never diverges to infinity**.

**Formally:**

```
∀ a, b ∈ ℕ, a < b, ∀ x ∈ ℕ₀:
    (∃ m, p ∈ ℕ : T^(m+p)(x) = T^(m)(x))
    ∨
    (∃ m ∈ ℕ : T^(m)(x) = 0)
```

---

## 📐 Examples

### Example 1: Starting from `x = 9`, parameters `(a, b) = (2, 3)`

```
T(9)   = R(2·9)   = R(18)   = 81
T(81)  = R(2·81)  = R(162)  = 261
T(261) = R(2·261) = R(522)  = 225
T(225) = R(2·225) = R(450)  = 54
T(54)  = R(⌊54/3⌋) = R(18)   = 81   ← cycle
```

**Trajectory enters the cycle** `(81, 261, 225, 54)`.

### Example 2: Starting from `x = 37`, parameters `(a, b) = (2, 3)`

```
37 → 47 → 49 → 89 → 871 → 2471 → 2494 → 138 → 64 → 12 → 4 → 1 → 2 → 0
```

**Trajectory reaches zero.**

### Example 3: Starting from `x = 16`, parameters `(a, b) = (2, 3)`

```
16 → 5 → 1 → 2 → 0
```

**Trajectory reaches zero in 4 steps.**

### Example 4: The Nested Cycle Family

The system exhibits a remarkable **nested cycle structure**:

```
C₁ = (81, 261, 225, 54)
C₂ = (891, 2871, 2475, 594)
C₃ = (8991, 28971, 24975, 5994)
C₄ = (81081, 261261, 225225, 54054)
C₅ = (810081, 2610261, 2250225, 540054)
...
```

Each cycle is derived from the previous one by inserting additional digits
at the leading position.

---

## 🖥️ Computational Verification

### Scope of Verification

We have verified the conjecture computationally for:

| Parameter | Range | Numbers Tested | Divergences |
|---|---|---|---|
| `(a, b) = (2, 3)` | `[0, 10⁶]` | 1,000,001 | **0** |
| `(a, b) = (2, 3)` | Families + large numbers | 1,290 | **0** |
| `(a, b) = (2, 3)` | Up to 1,417 digits | ~50 | **0** |

### Families Tested

The computational verification includes the following number families:

1. **Mersenne numbers**: `2^n − 1` for `n ∈ [1, 200]`
2. **Repdigits of 9**: `9, 99, 999, ...` (up to 100 digits)
3. **Repdigits of 1**: `1, 11, 111, ...` (up to 100 digits)
4. **Numbers with many 9s**: hand-picked critical cases
5. **Powers of 2**: `2^n`, `2^n ± 1`
6. **Fibonacci numbers**: `F_n` for `n ∈ [1, 300]`
7. **Palindromes**: small + constructed large palindromes
8. **Random samples**: extended range testing

### Key Findings

- **Zero divergences** observed in all tested ranges.
- **64 cycle records** identified for `(2, 3)` (up to rotation, fewer distinct cycles).
- **Nested cycle structure** confirmed across all scales.
- **Ratio stability**: ~56% of trajectories reach zero; ~44% enter cycles.

---

## 🧮 Theoretical Framework

### Geometric Growth Factor

The critical threshold governing convergence is:

```
λ = √(a / b)
```

- If `λ < 1` (i.e., `a < b`): convergence is expected.
- If `λ = 1` (i.e., `a = b`): partial divergence is expected.
- If `λ > 1` (i.e., `a > b`): frequent divergence is expected.

### Structure of the Proof

The proof framework, presented in the accompanying preprint, decomposes into:

| Component | Description | Status |
|---|---|---|
| **0. Definitions** | R, T, iterations | ✅ Complete |
| **1. Reduction** | Reduction to odd-run boundedness | ⚠️ Partial |
| **2. S₁ analysis** | `ρ₁ = 7/9` | ✅ Proven |
| **3. S₂ analysis** | `ρ₂ ≤ 4/5` | ✅ Proven |
| **4. Markov ergodicity** | Van der Corput-based | ⚠️ Conditional |
| **5. Exponential decay** | `ρ_L → 0` | ⚠️ Conditional |
| **6. Minimal counterexample** | Final argument | ✅ Structurally complete |

### The Van der Corput Ingredient

The conjecture's proof relies on the **Van der Corput low-discrepancy
property** of digit reversal, which states (informally) that reversing the
digits of a number produces a distribution that is closer to uniform than
random. This property is **known to hold** for digit-reversal sequences in
base 2 (Spiegelhofer, 2017), but its **extension to base 10 for the Ryovx
map remains to be formally established**.

---

## 📊 Current Status

### What This Repository Contains

- ✅ **A rigorous formulation** of the Ryovx Conjecture.
- ✅ **Extensive computational evidence** supporting the conjecture.
- ✅ **A conditional proof framework** with clearly identified gaps.
- ✅ **Reference implementation** in C (with GMP support).
- ✅ **LaTeX source** of the preprint.
- 🚧 **Partial Lean 4 formalization** (in progress).
- ⚠️ **The conjecture remains UNPROVEN.**

### Honest Classification

| Category | Status |
|---|---|
| **Conjecture** | ✅ Formulated |
| **Computational Evidence** | ✅ Extensive |
| **Theoretical Framework** | ⚠️ Conditional |
| **Rigorous Proof** | ❌ Not yet |
| **Lean 4 Formalization** | 🚧 In progress |
| **Peer-Reviewed Publication** | ❌ Not yet |

---

## 📁 Repository Structure

```
ryovx-conjecture/
├── README.md                  ← This file
├── LICENSE.md                 ← CC BY 4.0 International
├── CONTACT.md                 ← Contact information
├── CITATION.cff               ← Citation metadata
├── paper/
│   ├── ryovx-conjecture.tex   ← LaTeX source
│   ├── ryovx-conjecture.pdf   ← Compiled preprint
│   └── references.bib         ← Bibliography
├── code/
│   ├── c/
│   │   ├── rct.c              ← C implementation (uint64)
│   │   ├── rct_gmp.c          ← C implementation (GMP)
│   │   └── Makefile
│   ├── python/
│   │   ├── analysis.py        ← Statistical analysis
│   │   └── plotting.py        ← Visualization
│   └── lean/
│       └── Ryovx.lean         ← Lean 4 formalization
├── data/
│   ├── results_10e6.txt       ← Full program output (10⁶)
│   ├── cycles.txt             ← Catalog of cycles
│   └── families.txt           ← Family-based results
├── docs/
│   ├── conjecture.md          ← Detailed statement
│   ├── proof-sketch.md        ← Proof framework
│   └── faq.md                 ← Frequently asked questions
└── .github/
    └── workflows/
        └── build.yml          ← CI/CD for LaTeX + Lean
```

---

## ✅ What Has Been Done

### Mathematical Contributions

1. **Formulation** of a new discrete dynamical system.
2. **Definition** of the geometric growth factor `λ = √(a/b)`.
3. **Identification** of the subcritical threshold `a < b`.
4. **Discovery** of the nested cycle structure.
5. **Derivation** of `ρ₁ = 7/9` and `ρ₂ ≤ 4/5`.
6. **Framework** for a conditional proof via Van der Corput.

### Computational Contributions

1. **C implementation** (with `uint64_t` and GMP versions).
2. **OpenMP parallelization** for large-scale verification.
3. **Hash-set based** cycle detection.
4. **1,290+ numbers verified** across 8 families.
5. **Zero divergences** observed in all tested ranges.

### Documentation Contributions

1. **LaTeX preprint** with full mathematical exposition.
2. **Kernel documentation** in `docs/`.
3. **Example gallery** illustrating key behaviors.
4. **Reference bibliography** of related work.

---

## 🚧 What Remains to Be Done

### Mathematical Open Problems

1. **Rigorous proof** of the conjecture for `a < b`.
2. **Formal proof** of the Van der Corput ingredient in base 10.
3. **Characterization** of all cycles as a function of `(a, b)`.
4. **Extension** to arbitrary bases `B ≥ 2`.
5. **Connection** to ergodic theory and invariant measures.
6. **Study** of the `a = b` and `a > b` regimes.

### Computational Work

1. **Extended verification** to `10⁸` and beyond.
2. **Systematic family exploration**.
3. **Statistical analysis** of cycle distributions.
4. **Visualization** of trajectory structures.

### Formalization Work

1. **Complete Lean 4 formalization** of the framework.
2. **Formal proof** of the basic properties of `R`.
3. **Formal proof** of `ρ₁ = 7/9` and `ρ₂ ≤ 4/5`.
4. **Formal statement** of the Van der Corput axiom.
5. **Formal derivation** of the conjecture from the axiom.

---

## 🔗 Applications and Derivative Works

### Current Scope

**This repository currently contains ONLY the conjecture and its
preliminary framework.** No derivative applications are yet included.

### Planned Derivative Works

The following are **planned** but **not yet available**:

- **Extended bases**: systems defined in bases other than 10.
- **Generalized operations**: systems with more general parity-dependent rules.
- **Applied systems**: cryptographic and information-theoretic applications.
- **Pedagogical tools**: interactive visualizations for teaching dynamical systems.

### How to Build on This Work

If you wish to build on the Ryovx Conjecture:

1. **Cite this repository** in your work (see [Citation](#citation)).
2. **Acknowledge** that the conjecture remains open.
3. **Contact the author** (see [Contact](#contact)) for coordination.
4. **Share your results** via issues for inclusion in future updates.

---

## 📚 References

### Primary Reference

- **Muhammad, A. M.** (2026). *The Ryovx Conjecture: A Novel Discrete
  Dynamical System Combining Digit Reversal with Parity-Dependent
  Arithmetic Operations.* Preprint.

### Related Work

- **Lagarias, J. C.** (1985). *The 3x + 1 Problem and Its Generalizations.*
  American Mathematical Monthly, 92(1), 3–23.

- **Lagarias, J. C.** (ed.) (2010). *The Ultimate Challenge: The 3x + 1
  Problem.* American Mathematical Society.

- **Guy, R. K.** (1989). *Conway's RATS and Other Reversals.* American
  Mathematical Monthly, 96(5), 425–428.

- **Thiel, J.** (2014). *On RATS Sequences in General Bases.* Integers, 14,
  Paper A50.

- **Almirantis, Y., & Li, W.** (2024). *Rich Dynamical Behaviors from a
  Digital Reversal Operation.* arXiv:2408.02527.

- **Kaprekar, D. R.** (1949). *Another Solitaire Game.* Scripta Mathematica,
  15, 244–245.

- **Van der Corput, J. G.** (1935). *Verteilungsfunktionen I–II.*
  Proc. Kon. Ned. Akad. v. Wetensch., 38, 813–821, 1058–1066.

- **Spiegelhofer, L.** (2017). *The discrepancy of the digit reversal
  sequence.* Journal of Number Theory.

- **Hardy, G. H., & Wright, E. M.** (2008). *An Introduction to the
  Theory of Numbers.* Oxford University Press, 6th ed.

### AMS Subject Classification

- **11A63** — Radix representation; digital problems
- **37P99** — Arithmetic dynamics; none of the above, but in this section
- **37B20** — Dynamical systems and ergodic theory; local and nonlocal
- **11B75** — Sequences and sets; other combinatorial number theory
- **68Q99** — Theory of computing; none of the above, but in this section

---

## 📝 Citation

If you use this work, please cite:

```bibtex
@misc{muhammad2026ryovx,
  author       = {Muhammad, AbdulRahman M.},
  title        = {The Ryovx Conjecture: A Novel Discrete Dynamical System
                  Combining Digit Reversal with Parity-Dependent
                  Arithmetic Operations},
  year         = {2026},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.XXXXXXX},
  url          = {https://github.com/USERNAME/ryovx-conjecture}
}
```

**Zenodo DOI**: [10.5281/zenodo.XXXXXXX](https://doi.org/10.5281/zenodo.XXXXXXX)
*(placeholder — will be updated upon publication)*

**Zenodo Record**: [zenodo.org/record/XXXXXXX](https://zenodo.org/record/XXXXXXX)
*(placeholder — will be updated upon publication)*

---

## 📄 License

This work is licensed under the
[Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

**You are free to:**

- ✅ **Share** — copy and redistribute the material in any medium or format.
- ✅ **Adapt** — remix, transform, and build upon the material for any purpose.

**Under the following terms:**

- 📝 **Attribution** — You must give appropriate credit, provide a link to
  the license, and indicate if changes were made.

See [LICENSE.md](LICENSE.md) for the full license text.

---

## 📬 Contact

For questions, collaborations, or media inquiries, please see
[CONTACT.md](CONTACT.md).

**Primary Contact:**
AbdulRahman M. Muhammad
Independent Researcher
Email: `bedob3401@gmail.com`

---

## 🤝 Contributing

### Current Policy

> **Pull Requests are currently CLOSED by invitation only.**

This repository is in its **foundational phase**. We are focused on:

1. **Establishing** the mathematical framework rigorously.
2. **Completing** the Lean 4 formalization.
3. **Preparing** the preprint for peer review.

### How to Contribute

**While PRs are closed, we welcome:**

- 🐛 **Bug reports** via GitHub Issues.
- 💡 **Mathematical suggestions** via GitHub Discussions.
- 📚 **Reference recommendations** via Issues.
- 🔬 **Independent verification** reports via Issues.

### Future Contributions

Once the foundational phase is complete, we may open PRs for:

- Extended computational verification.
- Additional family testing.
- Lean 4 formalization contributions.
- Derivative systems (with proper attribution).

### Acknowledgment Policy

All contributors will be acknowledged in:

- The repository's `CONTRIBUTORS.md` file.
- Subsequent versions of the preprint.
- Future papers derived from this work.

---

## 🔮 Roadmap

### Phase 1: Foundational (Current)

- [x] Formulate the conjecture
- [x] Computational verification (up to 10⁶)
- [x] Draft the preprint
- [x] Publish on GitHub
- [ ] Publish on Zenodo
- [ ] Publish on arXiv

### Phase 2: Theoretical (3–12 months)

- [ ] Complete the Van der Corput analysis
- [ ] Formalize basic properties in Lean 4
- [ ] Extend verification to 10⁸
- [ ] Submit to a peer-reviewed journal

### Phase 3: Extensions (12+ months)

- [ ] Generalization to arbitrary bases
- [ ] Characterization of all cycles
- [ ] Connection to ergodic theory
- [ ] Applications to cryptography

### Phase 4: Long-Term (Ongoing)

- [ ] Full rigorous proof (if achievable)
- [ ] Interaction with the Collatz community
- [ ] Development of derivative systems

---

## 📈 Project Statistics

![GitHub repo size](https://img.shields.io/github/repo-size/Ryovx/ryovx-conjecture)
![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/Ryovx/ryovx-conjecture)
![GitHub last commit](https://img.shields.io/github/last-commit/Ryovx/ryovx-conjecture)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/Ryovx/ryovx-conjecture)
![GitHub issues](https://img.shields.io/github/issues/Ryovx/ryovx-conjecture)
![GitHub stars](https://img.shields.io/github/stars/Ryovx/ryovx-conjecture)

---

## 🙏 Acknowledgments

- The open-source community for the tools used in this research.
- **Ryovx Researches** for institutional support.
- The developers of **C**, **GMP**, **OpenMP**, **Lean 4**, and **LaTeX**.
- The mathematical community for inspiration from Collatz, RATS, and related
  dynamical systems.

---

<div align="center">

**The Ryovx Conjecture — A novel object of mathematical inquiry.**

*Status: Conjecture. Not yet proven. Open for collaboration.*

**© 2026 AbdulRahman M. Muhammad — CC BY 4.0 International**

</div>
