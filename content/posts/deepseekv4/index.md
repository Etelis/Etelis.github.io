---
title: "How LLMs Work — A Visual Tour Toward DeepSeek v4"
date: 2026-05-06
author: "Etelis"

lastmod: 2026-05-06
featuredImagePreview: ""
featuredImage: ""

draft: false
subtitle: ""
description: "An interactive, browser-based walkthrough of decoder-only transformers — from Llama 3 8B fundamentals down to a single attention head, then back out to DeepSeek v4's compressed-sparse-attention design."
tags: ["DeepSeek", "Transformers", "Attention", "LLM", "Visualization"]
categories: ["Machine Learning"]

---

## A guided zoom through a modern LLM

I wanted something that makes the architecture of a modern LLM *tangible* — not a wall of equations, but
an interactive tour you can scrub through. It zooms from the full model down to a single attention head's
matrix math, then back out to DeepSeek v4's full design, so each abstraction layer is grounded in the one
beneath it.

The tour walks seven scenes:

1. **Llama 3 8B architecture** — the full decoder stack: tokenizer → embedding → 32 decoder layers → final RMSNorm → LM head.
2. **Decoder layer** — what one layer contains: pre-norm, attention, residual, FFN (SwiGLU), residual.
3. **Multi-head attention** — the 32 query / 8 KV heads of grouped-query attention, laid out in parallel.
4. **Attention computation** — step-by-step Q · Kᵀ → scale → mask → softmax → · V on a small, real example.
5. **Attention variants** — MHA → GQA → MQA → MLA, each shown as a delta from the previous.
6. **DeepSeek v4 — CSA** — Compressed Sparse Attention: the Lightning Indexer, top-K selection, the m=4 / m=128 split.
7. **DeepSeek v4 — full architecture** — 61 layers interleaving HCA, CSA, and a full-attention layer, each with a 256-expert MoE FFN (8 active per token).

Built with React + React Flow + d3.

## Open the visual tour

<div style="text-align:center; margin: 1.5em 0">
  <a href="/decks/deepseekv4/" target="_blank" rel="noopener"
     style="display:inline-block; padding: 14px 28px; border-radius: 10px; background:#4f6bed; color:#fff;
            font-weight:700; text-decoration:none; font-size:1.05rem; box-shadow:0 6px 18px rgba(79,107,237,.35)">
    ▶ &nbsp;Open the interactive tour
  </a>
</div>

> Best viewed full-screen on a laptop.
