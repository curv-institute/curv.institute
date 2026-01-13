---
title: "Harmonized Hyper-Connections: Stabilizing Residual Transport Through Feedback on Geometry"
date: 2026-01-07
authors: "J. W. Miller"
venue: "CURV Institute Technical Report"
pdf: "/papers/harmonized-hyper-connections.pdf"
abstract: "Hyper-Connections (HC) expand the residual stream and introduce learnable residual mixing, increasing expressivity but often compromising training stability due to unbounded signal amplification across depth. Manifold-Constrained Hyper-Connections (mHC) address this instability by projecting residual transport onto a doubly stochastic manifold, restoring identity-like propagation and bounding composite gain. However, hard manifold projection can overconstrain residual transport and degrade performance on routing-heavy tasks. We propose a minimal alternative: Harmonized Hyper-Connections, which enforce stability through feedback acting on the geometry of residual transport by directly regulating the applied composite gain. We evaluate unconstrained HC, mHC, and Harmonized Hyper-Connections on a key–value retrieval task across multiple random seeds and extended training horizons. Unconstrained HC exhibits large gain variance across seeds and monotonic gain drift over time, while mHC enforces perfect stability at the cost of routing capability. In contrast, Harmonized Hyper-Connections maintain bounded applied gain with low variance while recovering task performance comparable to unconstrained HC. These results demonstrate that global feedback control can stabilize residual transport without hard manifold projection, provided control is applied to effective transport geometry rather than raw parameters."
---

## Overview

Residual connections owe their effectiveness to the identity mapping property, which enables stable forward and backward signal propagation through depth. Hyper-Connections (HC) generalize this paradigm by widening the residual stream and introducing learnable residual mixing matrices, increasing architectural expressivity without increasing FLOPs.

However, when extended across many layers, unconstrained residual transport compromises identity propagation—signals can be amplified or attenuated multiplicatively through depth, leading to instability, gradient explosion, or late-stage training failure.

## Method

Harmonized Hyper-Connections enforce stability through feedback acting on the geometry of residual transport, rather than through hard per-layer constraints:

$$H^{\mathrm{raw}}_{\ell} = I + \epsilon \Theta_{\ell}, \qquad H^{\mathrm{res}}_{\ell}(s) = I + s\,(H^{\mathrm{raw}}_{\ell} - I)$$

At each training step, the controller computes the composite gain of the *applied* transport and updates the transport scale $s$ using feedback to maintain a target gain budget.

**Key insight:** Control is applied to the transport actually used by the network rather than to raw parameter magnitudes. This decouples parameter drift from functional transport.

## Results

Three distinct regimes of residual transport:

| Variant | Stability | Routing Capability |
|---------|-----------|-------------------|
| Unconstrained HC | Seed-dependent, time-coupled instability | High (when stable) |
| mHC | Perfect stability | Collapsed |
| **Harmonized HC** | **Strong, repeatable stability** | **Preserved** |

- Unconstrained HC: Composite gain varies 12–33× across seeds
- mHC: Gain tightly bounded near unity, but accuracy collapses to chance
- Harmonized HC: Applied gain bounded with low variance, accuracy comparable to mean HC performance

## Code & Data

All code, logs, and plots are available at: [github.com/curv-institute/harmonized-hyper-connections](https://github.com/curv-institute/harmonized-hyper-connections)

## Acknowledgment

This work builds directly on the analysis introduced in *Manifold-Constrained Hyper-Connections* by Zhenda Xie and colleagues at DeepSeek-AI, who identified composite residual gain as the governing instability mechanism.
