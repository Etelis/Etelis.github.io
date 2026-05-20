---
title: "FlashAttention, From the GPU Up — An Interactive Deck"
date: 2026-05-20
author: "Etelis"

lastmod: 2026-05-20
featuredImagePreview: ""
featuredImage: ""

draft: false
subtitle: ""
description: "An interactive, slide-by-slide walkthrough of FlashAttention — tiling, online softmax, and recomputation — plus the FA2/3/4 lineage and where it sits in the vLLM stack."
tags: ["FlashAttention", "GPU", "Attention", "Transformers", "vLLM"]
categories: ["Machine Learning"]

---

## Why I built this

FlashAttention is one of those papers where the *idea* is simple — compute exact attention without ever
materializing the giant N×N score matrix — but the *why* only clicks once you understand the GPU memory
hierarchy underneath it. So instead of writing another summary, I built an interactive deck you can click
through: worked examples with real numbers, an animated forward-pass kernel, sliders for the softmax
overflow problem, and a step-by-step backward pass.

It walks the whole arc:

- **Setup** — why long sequences are hard, the approximate-attention landscape, and a GPU-101 primer
  (SMs, SIMT, the HBM ↔ SRAM memory hierarchy).
- **The core idea** — vanilla attention's memory cost (per head, per layer), safe/online softmax, block
  tiling, and the animated FlashAttention forward pass.
- **Backward & results** — recomputation, the kernel speed/memory microbenchmarks, and the BERT / GPT-2
  training wins.
- **The lineage** — FA2 → FA3 (Hopper) → FA4 (Blackwell), and where FlashAttention actually lives in the
  modern **vLLM** inference stack.

## Open the slides

The deck is fully interactive and keyboard-driven. Use **← / →** to navigate, **o** for an overview grid,
and **f** for fullscreen.

<div style="text-align:center; margin: 1.5em 0">
  <a href="/decks/flashattention.html" target="_blank" rel="noopener"
     style="display:inline-block; padding: 14px 28px; border-radius: 10px; background:#d97757; color:#fff;
            font-weight:700; text-decoration:none; font-size:1.05rem; box-shadow:0 6px 18px rgba(217,119,87,.35)">
    ▶ &nbsp;Open the interactive deck
  </a>
</div>

> Best viewed full-screen on a laptop. Built as a single self-contained page — original visualizations,
> describing the publicly published FlashAttention work (Dao et al., 2022) and its successors.
