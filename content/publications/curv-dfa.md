---
title: "Curv-DFA: A Curvature-Controlled Architecture for Density Functional Approximations in DFT"
date: 2026-01-02
authors: "J. W. Miller"
venue: "Research Paper Preprint"
pdf: "/papers/curv-dfa.pdf"
abstract: "Density Functional Theory (DFT) exhibits persistent failure modes—such as self-interaction error, overbinding, and density instability—that are commonly addressed through increasingly complex, entangled density functional approximations (DFAs). In this work, we introduce Curv-DFA, a curvature-controlled architecture for DFAs developed at the CURV Institute as part of its Representational Science program. Curv-DFA treats electronic density as a representation whose failures arise from distinct forms of curvature in representation space. Through controlled numerical experiments, we demonstrate that density-geometry regularization based on Fisher information does not correct self-interaction error and instead requires a separate energy-level control channel. We implement two orthogonal, diagnostic-gated correction layers: a harmonized Fisher curvature channel that regulates density geometry and bonding behavior, and a self-coupling control (SCC) channel that selectively regulates Hartree self-interaction in one-electron-dominated regions. Using sign-correct tests with positive controls and composability analysis, we show that these channels act independently and compose stably. Curv-DFA does not propose a universal functional; it provides a modular, experimentally validated control architecture for diagnosing and regulating representational failure within density functional approximations."
---

We introduce **Curv-DFA**, a curvature-controlled architecture for density functional approximations within DFT. Rather than proposing a new universal functional, Curv-DFA provides a modular framework that diagnoses distinct representational failure modes and applies orthogonal, diagnostic-gated control channels targeted to each mode. Key finding: self-interaction error and density geometry distortion are distinct failures requiring separate control mechanisms that compose stably.

**[Read Paper PDF](/papers/curv-dfa.pdf)**

---

## Why Curv-DFA Matters

Density Functional Theory is the workhorse of computational chemistry and materials science, but its approximate functionals exhibit persistent failures that resist simple fixes. Self-interaction error causes electrons to spuriously repel themselves. Overbinding distorts molecular geometries. Density instabilities appear in stretched bonds and transition states.

The standard response has been to build increasingly complex functionals that attempt to fix everything at once. The result is entangled corrections where it's unclear which mechanism addresses which failure—and where improvements in one regime often cause regressions elsewhere.

Curv-DFA takes a different approach: treat these as distinct representational failures that require orthogonal control.

## Two failure modes, two control channels

Through controlled numerical experiments, we establish that:

**Density geometry distortion** (how sharply the density curves and forms bonds) is addressed by Fisher-information-based regularization. This channel affects bonding behavior but does *not* correct self-interaction error.

**Self-interaction error** (spurious electron self-repulsion in the Hartree term) requires a separate Self-Coupling Control (SCC) channel that operates on energy rather than geometry. Critically, this channel must be gated to activate only in genuinely one-electron-dominated regions—naive application catastrophically overcorrects in normal molecules.

Sign-correct tests on H₂⁺ confirm that these are genuinely distinct failures: geometry control shifts energies in the *opposite* direction from self-interaction correction.

## Composability matters

When both control channels are applied simultaneously, deviations from additivity remain below 2% across all test systems. This orthogonality is not incidental—it's the design goal. Modular, composable corrections are easier to validate, easier to interpret, and easier to extend than monolithic functionals where everything affects everything.

## Scope

Curv-DFA does not claim to be a universal functional or to achieve benchmark dominance. It demonstrates that representational failures in DFT can be diagnosed and controlled through modular architecture rather than functional complexity. The current implementation uses a frozen-gate approximation; full variational consistency is future work.

## Code & Data

Implementation details and numerical results are available upon request from the CURV Institute.
