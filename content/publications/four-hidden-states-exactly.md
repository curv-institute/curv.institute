---
title: "Four hidden states, exactly: a replayable result on observed time-asymmetry"
date: 2026-08-26
authors: "J. W. Miller"
venue: "Replayable result (preprint in preparation)"
abstract: "A strictly positive stationary Markov chain seen through a deterministic binary view can show observed time-asymmetry only if it has at least four hidden states, and four suffice. Both halves are exact: a short proof for the impossibility with three or fewer states, and an explicit rational four-state family whose length-four word probabilities differ from their reversals by exactly −2s³. A minimal harness reproduces every stated number with rational arithmetic."
---

**Setting.** A hidden chain with transition matrix `P` and stationary law `π` is observed through a map `g` sending each hidden state to `0` or `1`. For an observed word `w`, write `D(w) = Pr(w) − Pr(reverse of w)`. The observed process is time-reversible exactly when every `D(w)` is zero.

**Theorem 1 (three states cannot).** If the chain has at most three hidden states and `g` is onto `{0,1}`, then `D(w) = 0` for every word `w` of every length, whatever the hidden chain does. Reason: some observed symbol is emitted by a single hidden state; a run-factorization identity `L_m = π₀ T_m` then pairs every word with its reversal at equal probability.

**Theorem 2 (four states can, and length four sees it).** Take four hidden states, uniform law, view `(0,0,1,1)`, and

    A = [[ 0,-2, 0, 2],
         [ 2, 0,-1,-1],
         [ 0, 1, 0,-1],
         [-2, 1, 1, 0]],     P(s) = J/4 + s·A,   |s| < 1/16.

Every entry of `P(s)` exceeds 1/8 and the uniform law is stationary. Then

    D(0010) = −2 s³,

so the observed process is reversible if and only if `s = 0`, and by stationary marginalization the asymmetry appears at every word length ≥ 4.

**Exact witnesses.** At `s = 5/96`: `D(0010) = −125/442368`, with 8 nonzero coordinates among length-4 words. At `s = −7/128`: `D(0010) = 343/1048576`, with 20 nonzero coordinates among length-5 words. Values are exact rationals, not approximations.

**What is not claimed.** Nothing about non-stationary chains, stochastic (non-deterministic) views, alphabets larger than two, or how many hidden states are needed for other asymmetry patterns. Related prior work exists on reversibility of three-state hidden Markov models; the confrontation with it is part of the paper.

**Replay it.** The harness (`check.py`, two independent exact engines, stated witnesses) prints `PASS` only if every number above reproduces in both implementations; anything else prints `UNRESOLVED`. Download: *(link once released)*.
