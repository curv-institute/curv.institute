---
title: "Testing the Platonic Representation Hypothesis via Representation-Controlled Tokenization"
date: 2026-01-16
authors: "J. W. Miller"
venue: "Technical Preprint"
pdf: "/papers/universal-tokenizer-prh.pdf"
abstract: "Modern tokenizers are treated as neutral preprocessing steps, yet they implicitly encode assumptions about representation, stability, and learnability. The Platonic Representation Hypothesis (PRH) posits that stable abstract representations exist independently of semantics and learning objectives, and that such representations can be measured and regulated. We test this hypothesis empirically by constructing a representation-controlled stack consisting of a Universal Lossless Tokenizer (ULT), a relational regularization mechanism (Harmonized Hyper-Connections, HHC), and a reversible Language Interface Layer (LIL). Across heterogeneous byte streams, ULT achieves lossless universal tokenization with measurable stability diagnostics. Introducing HHC yields a controlled trade-off: a modest compression penalty in exchange for substantially improved stability and reduced representational curvature under regime shifts. A strictly normalized downstream language-model proxy experiment produces a negative result, confirming that stability-optimized representations are not necessarily easier to learn under next-token objectives. Finally, LIL demonstrates that interface stability can be achieved independently of representation and learning, via deterministic, reversible structure normalization. Together, these results are consistent with PRH's core prediction that representational stability is an intrinsic property, separable from compression efficiency and learnability."
---

We present empirical tests of the Platonic Representation Hypothesis by constructing a representation-controlled tokenization stack. The core finding: stability, efficiency, and learnability are distinct axes requiring explicit trade-offs. Representations optimized for global stability are not necessarily aligned with local next-token predictability—a negative result that confirms rather than contradicts PRH.

**[Read Paper PDF](/papers/universal-tokenizer-prh.pdf)**

---

## Why Tokenization Reveals Representation

This work treats the Platonic Representation Hypothesis not as philosophy but as an engineering hypothesis. Tokenization provides an ideal test bed: it is foundational to modern AI systems, yet under-examined as a site where representational assumptions are implicitly encoded.

PRH posits that representation precedes semantics and learning—stable structural forms exist regardless of whether they are easy to compress or predict. From this follow testable predictions: (1) stability can be measured independently of learning; (2) enforcing relational constraints should increase stability at some cost; (3) representations optimized for stability may be harder to learn; and (4) interface structure can be stabilized without semantic inference.

## The Representation-Controlled Stack

We construct three components that isolate different aspects of representation:

**Universal Lossless Tokenizer (ULT).** Operates directly on bytes with streaming operation and guarantees exact reconstruction. Tokenization proceeds via equilibrium projection and bounded segmentation, with residual coding ensuring losslessness. Diagnostics are computed during tokenization to assess representational curvature and stability.

**Harmonized Hyper-Connections (HHC).** Introduces bounded relational coupling between neighboring representations during equilibrium projection, along with relative curvature diagnostics. A closed-loop stability controller regulates trade-offs between efficiency and stability.

**Language Interface Layer (LIL).** A reversible, deterministic transformation applied above ULT that normalizes prompt structure, enforces explicit role boundaries, and applies reversible macro compaction to common interface patterns.

## Key Results

### ULT achieves universal lossless tokenization
- 100% bit-exact reconstruction across mixed text, code, JSON, Unicode, and arbitrary binary streams
- End-to-end compression reaches approximately 3.35 bits per byte on heterogeneous streams
- Curvature distributions remain well-behaved across scale

### HHC demonstrates the stability–efficiency trade-off
- 10.5% increase in bits per byte in exchange for 36% improvement in stability margin
- 9% reduction in mean curvature under regime-shift stress streams
- HHC is fully active and non-degenerate with minimal controller interventions required

### Negative downstream result confirms PRH
- HHC-stabilized tokens yield substantially higher loss (~50% increase) in language-model proxy experiments
- Under strict byte-normalized controls, baseline tokens achieve 1.15 ± 0.03 loss vs HHC's 1.76 ± 0.08
- This confirms that representations optimized for global stability and relational coherence are not aligned with local next-token predictability

### LIL achieves interface stability orthogonally
- 100% lossless round-trip reconstruction when composed with ULT
- Modest structural overhead (~5% BPB) that diminishes with prompt length
- Demonstrates that interface stability can be achieved independently of representation and learning

## Interpretation

The experiments support PRH's core claims:

1. Stable representations exist and are measurable independently of semantics and learning
2. Enforcing relational constraints increases stability while trading off compression efficiency and learnability
3. Interface stability can be achieved orthogonally via reversible structure normalization
4. Negative downstream results are not failures but confirmations of objective misalignment

By treating representation as a controllable substrate rather than an incidental preprocessing step, this work provides empirical evidence that stability, efficiency, and learnability are distinct axes. Future systems must choose deliberately which properties to optimize rather than conflating them implicitly.

## Historical Context

The motivation for a structure-bearing representation dates back to John Wilkins' 17th-century proposal for a philosophical language. Wilkins correctly identified that linguistic symbols should encode structural relations rather than rely on interpretation alone. However, his approach assumed that such structure could be fixed a priori through taxonomy. The present results suggest the opposite: stable representational structure must be dynamically realized, measured, and regulated, and inevitably trades off against efficiency and learnability.

## Code & Data

All assets required to reproduce the results are included in the accompanying repository. This includes source code, deterministic data generation scripts, evaluation datasets with manifests, generated figures and tables, and scripts to reproduce all experiments from recorded manifests. No external datasets, pretrained models, or proprietary resources are required.

**Repository:** [github.com/curv-institute/universal_tokenizer](https://github.com/curv-institute/universal_tokenizer)
