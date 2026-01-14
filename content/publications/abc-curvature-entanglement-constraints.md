---
title: "Constraints on Curvature-Mediated Long-Range Entanglement in a Minimal Three-Node Quantum Chain"
date: 2026-01-13
authors: "J. W. Miller"
venue: "Technical Preprint — Under submission to Physical Review A"
pdf: "/papers/abc-curvature-entanglement-constraints.pdf"
abstract: "We test whether hub-localized noise can induce curvature-mediated long-range entanglement in a minimal three-node chain (A–B–C) with nearest-neighbor couplings only. Using ideal simulation (Qiskit Aer) and IBM superconducting quantum hardware, we reconstruct pairwise two-qubit states (AB, BC, AC) via tomography and quantify entanglement by negativity. Across physically meaningful noise regimes—delay-based decoherence (time-under-T₁/T₂) and dephasing-dominant Pauli-Z—we observe no robust emergence of A–C entanglement. A small A–C negativity appears only under Pauli-Z at higher noise settings and remains far below nearest-neighbor entanglement. These results constrain strong 'curvature-channel' claims in the minimal A–B–C geometry."
---

We present a systematic experimental test of whether curvature- or geometry-mediated mechanisms can induce long-range entanglement in open quantum systems beyond direct Hamiltonian couplings. Using the minimal nontrivial topology—a three-node linear chain with nearest-neighbor interactions only—we find no evidence for robust long-range entanglement under hub-localized noise on real IBM superconducting quantum hardware.

**[Read Paper PDF](/papers/abc-curvature-entanglement-constraints.pdf)**

---

## Summary

This work presents a systematic experimental test of whether curvature- or geometry-mediated mechanisms can induce long-range entanglement in open quantum systems beyond direct Hamiltonian couplings.

Using the minimal nontrivial topology—a three-node linear chain (A–B–C) with nearest-neighbor interactions only—we probe multiple physically meaningful noise regimes on real IBM superconducting quantum hardware. Across ideal simulation, noisy simulation, and hardware execution, we find no evidence for robust long-range A–C entanglement under hub-localized noise. A small, bounded A–C signal appears only under dephasing-dominant noise and remains far below nearest-neighbor entanglement.

These results place quantitative constraints on strong "curvature-channel" claims in minimal geometries and clarify that any geometry-mediated entanglement effects, if present, are not operative at the smallest nontrivial scale.

## What was tested

- A three-qubit linear chain (A–B–C) with XX-like couplings on A–B and B–C only
- No direct A–C coupling
- Pairwise entanglement measured via full Pauli-basis tomography and negativity
- Multiple hub-noise regimes applied to the intermediate node B:
  - Idle gate injection (unitary control)
  - Delay-based decoherence (time-under-T₁/T₂)
  - Dephasing-dominant Pauli-Z noise
- Experiments were carried out using Qiskit Aer and IBM Quantum hardware via Qiskit Runtime

## Key results

- Nearest-neighbor entanglement (A–B and B–C) behaves as expected under all noise regimes
- Physical decoherence introduced via delay produces controlled monotonic degradation without inducing long-range entanglement
- Dephasing-dominant noise produces a small, bounded A–C correlation near the tomography noise floor
- No regime exhibits A–C dominance or a robust long-range entanglement channel

## Interpretation

This study falsifies the strong form of curvature-mediated long-range entanglement in minimal three-node chains. The results indicate that geometry- or curvature-based entanglement mechanisms, if they exist, require additional structural ingredients—such as redundant paths, feedback, or network-level topology—to manifest at measurable strength.

Rather than supporting shortcut or topology-bypassing entanglement, the data reinforce that geometric effects in open quantum systems are emergent and collective, not pointwise.

## Why this matters

Negative results of this kind are essential for bounding speculative extensions of open-system dynamics and for preventing misinterpretation of noise-assisted effects in near-term quantum hardware. This work provides a clean experimental baseline that clarifies where geometry does not matter, thereby sharpening the conditions under which it might.

## Reproducibility

All experiments were executed using publicly available tools and required less than ten minutes of total QPU runtime on IBM Quantum's standard free-access allocation. Circuit definitions, raw measurement counts, and analysis scripts are publicly available.

## Code & Data

Implementation details and numerical results are available upon request from the CURV Institute.
