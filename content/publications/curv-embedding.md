---
title: "Stability-Driven Chunking and Representational Reranking for Dynamic Vector Databases"
date: 2026-01-17
authors: "J. W. Miller"
venue: "Technical Preprint"
pdf: "/papers/curv-embedding.pdf"
abstract: "Vector databases are increasingly used in dynamic settings where documents are incrementally ingested, edited, and queried over time. In such regimes, heuristic chunking and similarity-based retrieval can lead to unstable embeddings, excessive re-indexing, and inconsistent retrieval behavior. In this work, we present a staged empirical study of stability-driven chunking and representational reranking for vector databases. We show that chunking based on representational stability produces fewer, more coherent chunks and supports streaming ingestion with bounded deviation from offline segmentation. We report a negative result demonstrating that stability-driven chunking is more sensitive to localized edits under naive, count-based mutation metrics. We then show that this apparent failure is a measurement artifact: when mutation cost is measured in bytes rather than chunk counts, a hybrid chunking policy that combines stability-driven base chunks with localized overlapping micro-chunks achieves the lowest effective update cost. Finally, we demonstrate that representational reranking improves retrieval robustness in the tails, increasing worst-case reformulation stability without affecting mutation cost or determinism. Together, these results disentangle representational coherence, mutation tolerance, and retrieval robustness, and highlight the importance of cost-aligned metrics in evaluating dynamic vector retrieval systems."
---

We present empirical methods for stability-aware chunking and retrieval in dynamic vector databases. The core finding: representational coherence, mutation tolerance, and retrieval robustness are distinct axes requiring explicit trade-offs—and metric choice fundamentally determines which strategies appear optimal.

**[Read Paper PDF](/papers/curv-embedding.pdf)**

---

## Why Stability Matters for Vector Databases

Most vector database systems rely on heuristic chunking strategies—fixed-size segments with overlap—combined with approximate nearest-neighbor search. While effective in static benchmarks, these choices implicitly assume stable embeddings and infrequent updates.

In practice, many vector databases operate under continuous ingestion and localized edits. Under such conditions, naive chunking can induce excessive re-embedding, index churn, and retrieval instability. These effects are often invisible to benchmark-style evaluations, which emphasize static accuracy rather than temporal behavior.

This work investigates chunking and retrieval strategies through the lens of stability, asking how these choices affect structural coherence, mutation tolerance, and robustness over time.

## Key Results

### Stability-driven chunking produces coherent segments
Chunking based on representational strain signals produces 35% fewer chunks with larger mean size compared to fixed-size heuristics. Boundaries are placed at points of elevated representational strain rather than arbitrary length thresholds, preserving coherent regions as single units.

### Streaming parity with offline segmentation
Under bounded lookahead, streaming execution closely approximates offline stability-driven segmentation. Boundary overlap exceeds 97% within a ±256-byte tolerance, confirming compatibility with live ingestion pipelines.

### Negative result under count-based metrics
When evaluated under localized edits, stability-driven chunking exhibits higher apparent mutation sensitivity than fixed-size overlapping chunking when measured using count-based metrics. This reflects the larger granularity of stability-driven chunks, where any edit invalidates the entire chunk.

### Metric correction reverses the ranking
Count-based mutation metrics implicitly treat all chunks as equal cost, mischaracterizing hybrid policies that intentionally vary granularity. When mutation cost is measured in bytes rather than chunk counts, the ranking reverses. Hybrid chunking reduces effective mutation cost by 54% relative to the baseline.

### Representational reranking improves tail robustness
Representational reranking yields modest improvements in mean reformulation overlap (+2.3%) and substantially improves worst-case behavior, increasing P10 overlap by 14.3%. A random reranking control collapses performance, confirming that gains arise from representational signals.

## Three Competing Axes

Across all experiments, three competing axes emerge:

1. **Representational coherence** — optimized by stability-driven chunking
2. **Mutation tolerance** — optimized by fixed-size overlapping chunking
3. **Retrieval robustness** — improved by representational reranking

No single mechanism optimizes all three simultaneously. Hybrid policies do not eliminate trade-offs but localize them, making system behavior predictable and bounded under updates.

## Practical Implications

These results suggest that dynamic vector databases should:

- **Decouple segmentation, mutation handling, and retrieval ranking** as independent design choices
- **Evaluate systems using cost-aligned metrics** (bytes, not chunk counts) rather than static benchmarks
- **Consider hybrid chunking** that combines stability-driven base chunks with localized micro-chunks in edit regions
- **Apply representational reranking** for improved worst-case retrieval behavior without affecting mutation cost

## Code & Data

All code, data generation scripts, and experiment manifests are available. Each run produces configuration snapshots, raw metric measurements, aggregated statistics, and full chunk audit logs.

**Repository:** [github.com/curv-institute/curv-embedding](https://github.com/curv-institute/curv-embedding)
