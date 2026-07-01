---
title: "Mixture of Experts — From a Dense FFN to Sparse Routing"
date: 2026-07-01
author: "Etelis"

lastmod: 2026-07-01
featuredImagePreview: ""
featuredImage: ""

draft: false
subtitle: ""
description: "An interactive, click-through walkthrough of Mixture-of-Experts LLMs — from a dense FFN through routing and fine-grained experts to DeepSeek V3, then out to expert parallelism, the NVFP4 / fused-MoE GPU kernels, and EPLB load balancing."
tags: ["Mixture of Experts", "MoE", "DeepSeek", "LLM", "vLLM", "Visualization"]
categories: ["Machine Learning"]

---

## Why I built this

Mixture of Experts is easy to state — swap the dense FFN for many smaller "expert" FFNs and route each
token to just a few of them — but the *consequences* only click once you follow the idea all the way down:
how routing actually works, why each expert ends up *narrow*, how a 671B-parameter model gets split across
GPUs, and what it takes to serve it fast. So instead of another summary, I built an interactive deck you can
scrub through, zooming from a single dense layer out to a full rack of GPUs.

It's one continuous arc — 55 beats across 16 chapters:

- **From dense to sparse** — the full model and one decoder layer, where the parameters actually live, and
  splitting the dense FFN into experts.
- **Routing** — what the router routes (token vs. sequence), the router and its top-k gating, fine-grained
  expert segmentation, and a zoom inside one small SwiGLU expert.
- **A real model** — DeepSeek V3's full per-token flow, and why 671B parameters (37B active) don't fit on a
  single GPU.
- **Serving it fast** — model parallelism (DP / TP / PP / EP), expert parallelism, the NVFP4 and fused-MoE
  GPU kernels, wide expert parallelism across an NVL72 rack, and EPLB load balancing.

Built with React + Framer Motion + d3.

## Open the interactive deck

Click anywhere — or use **← / →** — to step through the beats. Jump to any chapter from the rail at the top.

<div style="text-align:center; margin: 1.5em 0">
  <a href="/decks/moe/" target="_blank" rel="noopener"
     style="display:inline-block; padding: 14px 28px; border-radius: 10px; background:#0f766e; color:#fff;
            font-weight:700; text-decoration:none; font-size:1.05rem; box-shadow:0 6px 18px rgba(15,118,110,.35)">
    ▶ &nbsp;Open the interactive deck
  </a>
</div>

> Best viewed full-screen on a laptop. Original visualizations; the DeepSeek V3, kernel, and EPLB details
> describe publicly published work.
