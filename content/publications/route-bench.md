---
title: "ROUTE-Bench: Evaluating Selective Routing Under Composition"
date: 2026-01-12
authors: "J. W. Miller"
venue: "CURV Institute Technical Report"
abstract: "We introduce ROUTE-Bench, a synthetic benchmark for evaluating how language models integrate evidence from multiple sources under compositional task demands. The benchmark measures routing quality across retrieval-augmented generation (RAG), structured memory access, and tool use in long-context settings. We evaluate three control strategies—baseline inference, hard-constrained prompting, and Harmonized Hyper-Connections—and find that the harmonized variant doubles evidence-grounded accuracy (0.040 vs. 0.020), albeit from a low baseline typical of compositional evidence integration tasks, while exhibiting 35% lower position sensitivity compared to baseline. Hard constraints improve evidence recall but reduce raw accuracy. Tool utilization remains a limitation across all variants."
---

## Overview

ROUTE-Bench is a fully synthetic and deterministically verifiable evaluation suite for studying selective routing under composition. Unlike existing benchmarks that isolate individual capabilities, ROUTE-Bench requires models to simultaneously:

- Retrieve relevant evidence from large document collections
- Query structured memory
- Invoke tools when computation is required
- Integrate evidence across variable context positions

## Key Findings

| Metric | Baseline | Hard-Constrained | Harmonized |
|--------|----------|------------------|------------|
| AnswerAcc | **0.255** | 0.150 | 0.225 |
| GroundedAcc | 0.020 | 0.025 | **0.040** |
| ToolTraceAcc | 0.410 | **0.435** | 0.420 |
| EvidenceRecall | 0.333 | **0.403** | 0.365 |

**Harmonized Hyper-Connections** improve evidence-grounded accuracy by 2× relative to baseline and reduce position sensitivity by 35%, indicating more stable performance across context positions.

## Code & Data

All code, data, and results are available at: [github.com/curv-institute/route-bench](https://github.com/curv-institute/route-bench)

## Related Work

This paper is a direct evaluation follow-on to [Harmonized Hyper-Connections](/publications/harmonized-hyper-connections/), which introduced a mechanism for stabilizing residual transport by regulating applied composite gain.
