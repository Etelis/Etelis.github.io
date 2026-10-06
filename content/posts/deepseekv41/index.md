---
title: "DeepSeek-V4.1-Flash — An Interactive Architecture Explorer"
date: 2026-10-06
author: "Etelis"

lastmod: 2026-10-06
featuredImagePreview: ""
featuredImage: ""

draft: false
subtitle: ""
description: "A clickable 3D model of DeepSeek-V4.1-Flash in which every part opens its own animated walkthrough: CED, CSA2, the lightning and hierarchical sparse indexers, Engram, single-pass mHC, and the 890-byte-per-token KV cache."
tags: ["DeepSeek", "DeepSeek-V4.1", "Attention", "KV Cache", "LLM", "Visualization"]
categories: ["Machine Learning"]

---

## Why I built this

DeepSeek-V4.1-Flash packs a lot of new ideas into one 40-layer model, and most of them only make sense once
you see where they sit and what flows through them. So for a talk I built the whole model as one 3D object
you can orbit and click. Every part opens a short walkthrough that plays like a video with captions, using
real numbers and small worked examples, checked against the paper, the released config and the reference code.

The walkthroughs:

- **Causal encoder-decoder (CED)**: from the 2017 Transformer to YOCO, then how CED builds the decoder's keys
  and values from the encoder's output, and why V4.1-Flash keeps only layer 20's projection.
- **The attention family → CSA2**: MHA, GQA, MQA, CSA and HCA as one lineage, then CSA2 and how 40 layers share
  4 caches through its Full, Reindex and Reuse modes.
- **The lightning indexer**: where the index key, index query and head weights come from, the 32 index heads,
  and top-k.
- **The hierarchical sparse indexer**: layer 20 scores every position and keeps 2,048 blocks of 8 as a
  candidate pool; the Reindex layers score only that pool.
- **Engram**: n-gram memory, from why every 2-, 3- and 4-gram can't get its own row to hashing them into fixed
  tables, and where its ≈197B parameters go.
- **Single-pass mHC**: from one residual lane to four hyper-connection lanes with a worked numerical example,
  then why the mixing must stay balanced and how a single pass halves the memory traffic.
- **The KV cache**: where the 890 bytes per token go, and how the cache for a million tokens got 437× smaller
  than DeepSeek-V1's.

Built with three.js.

## Open the explorer

Drag to orbit, then click any part to open its walkthrough. Inside a walkthrough, use **← / →** (or Play) to
step through it and **Esc** to return to the model.

<div style="text-align:center; margin: 1.5em 0">
  <a href="/decks/deepseekv41/" target="_blank" rel="noopener"
     style="display:inline-block; padding: 14px 28px; border-radius: 10px; background:#4353d6; color:#fff;
            font-weight:700; text-decoration:none; font-size:1.05rem; box-shadow:0 6px 18px rgba(67,83,214,.35)">
    ▶ &nbsp;Open the interactive explorer
  </a>
</div>

> Best viewed full-screen on a laptop. Original visualizations; the architecture details describe DeepSeek's
> published work, and toy values in the examples are marked as illustrative.
