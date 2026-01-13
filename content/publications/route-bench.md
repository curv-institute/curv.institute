---
title: "ROUTE-Bench: Evaluating Selective Routing Under Composition"
date: 2026-01-12
authors: "J. W. Miller"
venue: "Research Paper Preprint"
pdf: "/papers/route-bench.pdf"
abstract: "We introduce ROUTE-Bench, a synthetic benchmark for evaluating how language models integrate evidence from multiple sources under compositional task demands. The benchmark measures routing quality across retrieval-augmented generation (RAG), structured memory access, and tool use in long-context settings. We evaluate three control strategies—baseline inference, hard-constrained prompting, and Harmonized Hyper-Connections—and find that the harmonized variant doubles evidence-grounded accuracy (0.040 vs. 0.020), albeit from a low baseline typical of compositional evidence integration tasks, while exhibiting 35% lower position sensitivity compared to baseline. Hard constraints improve evidence recall but reduce raw accuracy. Tool utilization remains a limitation across all variants."
---

We introduce **ROUTE-Bench**, a synthetic benchmark for evaluating how language models integrate evidence from multiple sources under compositional task demands. The benchmark measures routing quality across RAG, structured memory access, and tool use in long-context settings. Key finding: Harmonized Hyper-Connections double evidence-grounded accuracy while exhibiting 35% lower position sensitivity compared to baseline.

**[Read Paper PDF](/papers/route-bench.pdf)**

---

## Why ROUTE-Bench Matters in Practice

If you've built or deployed modern language systems, you've likely noticed a frustrating pattern: models often know the right information, but fail to use it reliably. They retrieve the correct document, look up the right value, or even call the correct tool—and then lose track of it later. Answers become brittle, inconsistent, or overly biased toward whatever happened most recently.

ROUTE-Bench exists to measure that failure mode directly.

## The real problem isn't retrieval—it's composition

Most current benchmarks ask whether a model can find information. ROUTE-Bench asks something harder and more realistic: can the model keep the right information influential as it's reused across multiple steps, sources, and context positions?

In real systems, models don't just answer a question once. They:

- retrieve documents,
- consult structured memory,
- call tools,
- reason over intermediate results,
- and do all of this across long contexts or multi-step loops.

Each step requires the model to route attention and influence—deciding what matters and what doesn't. The failure usually isn't that the model can't route once; it's that those routing decisions don't hold up when they're composed over time. Early evidence gets diluted, later evidence dominates due to recency, and correct tool outputs get ignored or overwritten.

ROUTE-Bench is designed specifically to expose that problem.

## Why existing benchmarks miss this

Many benchmarks isolate capabilities:

- retrieval benchmarks test retrieval,
- tool benchmarks test tool calling,
- long-context benchmarks test recall at distance.

In practice, these capabilities interact. ROUTE-Bench forces them to interact in the same example. A correct answer requires:

- retrieving the right document,
- reading the right memory entry,
- optionally using a tool,
- and integrating all of that correctly—even when the evidence appears far from the query.

Because the benchmark is synthetic and fully controlled, it can vary evidence position, difficulty, and task type while keeping everything else fixed. That makes failures interpretable instead of mysterious.

## What ROUTE-Bench reveals that matters operationally

The benchmark consistently shows three behaviors that map directly to production issues:

**Raw accuracy can look fine while grounding is poor.**
Models often answer correctly without actually using the right evidence. ROUTE-Bench's GroundedAcc metric catches this, which is critical for systems where attribution and reliability matter.

**Recency bias is a major hidden failure mode.**
Baseline models perform better when evidence is near the end of the context and worse when it appears early. That's exactly what causes agents to forget early constraints or design decisions during long sessions.

**Hard constraints trade reliability for capability.**
Forcing models to cite evidence or use tools improves recall, but often at the cost of overall accuracy and flexibility. ROUTE-Bench quantifies that trade-off instead of hand-waving about it.

## Why this matters for real systems

ROUTE-Bench is not about winning a leaderboard. It's about diagnosing why systems fail in ways that users actually experience:

- retrieval-augmented systems that hallucinate despite having the right docs,
- coding agents that ignore earlier plans or test results,
- assistants that over- or under-use tools unpredictably,
- long-context models that lose track of important early information.

By separating selection (finding the right thing) from composition (keeping it influential), ROUTE-Bench gives teams a way to tell whether a fix actually addresses the root cause—or just masks symptoms.

## The practical takeaway

If you're building systems that rely on retrieval, memory, tools, or multi-step reasoning, you don't just need models that can route once. You need models whose routing decisions remain stable when reused. ROUTE-Bench provides a concrete way to measure that stability and compare approaches honestly.

It doesn't claim to solve the problem. It makes the problem visible—and measurable.

## Code & Data

Implementation details and numerical results are available upon request from the CURV Institute.

## Related Work

This paper is a direct evaluation follow-on to [Harmonized Hyper-Connections](/publications/harmonized-hyper-connections/), which introduced a mechanism for stabilizing residual transport by regulating applied composite gain.
