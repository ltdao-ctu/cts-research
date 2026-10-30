---
type: paper
node_id: paper:bello2026_privacypreserving_collaborative_medical
title: "Privacy-Preserving Collaborative Medical Image Segmentation Using Latent Transform Networks"
authors: ["Saheed Ademola Bello", "Muhammad Shahid Jabbar", "Muhammad Sohail Ibrahim", "Shujaat Khan"]
year: 2026
venue: "arXiv (q-bio.QM, cs.CR)"
external_ids:
  arxiv: "2603.05541"
  doi: null
  s2: null
tags: ["ultrasound", "nerve-segmentation", "privacy-preserving", "federated-learning"]
added: 2026-10-30T09:05:09Z
---

# Privacy-Preserving Collaborative Medical Image Segmentation Using Latent Transform Networks

## One-line thesis
Privacy-preserving collaborative medical image segmentation via Latent Transform Networks evaluated across multi-institutional ultrasound nerve segmentation and medical imaging datasets.

## Problem / Gap
_TODO._

## Method
_TODO._

## Key Results
_TODO._

## Assumptions
_TODO._

## Limitations / Failure Modes
_TODO._

## Reusable Ingredients
_TODO._

## Open Questions
_TODO._

## Claims
_TODO._

## Connections
_Edges are recorded in `graph/edges.jsonl`; summarize here for human readers._

## Relevance to This Project
_TODO._

## Abstract (original)

> Collaborative training across multiple institutions is becoming essential for building reliable medical image segmentation models. However, privacy regulations, data silos, and uneven data availability prevent hospitals from sharing raw scans or annotations, limiting the ability to train generalizable models. Latent-space collaboration frameworks such as privacy-segmentation framework (SF) offer a promising alternative, but such methods still face challenges in segmentation accuracy and vulnerability to latent inversion and membership-inference attacks. This work introduces a privacy-preserving collaborative medical image segmentation framework (PPCMI-SF) designed for heterogeneous medical datasets. The approach combines skip-connected autoencoders for images and masks with a keyed latent transform that applies client-specific orthogonal mixing and permutation to protect latent features before they are shared. A unified mapping network on the server-side performs multi-scale latent-to-latent translation, enabling segmentation inference without exposing raw data. Experiments on four datasets: PSFH ultrasound, ultrasound nerve segmentation, FUMPE CTA, and cardiac MRI show that the proposed PPCMI-SF consistently achieves high Dice scores and improved boundary accuracy, as reflected by lower 95th percentile Hausdorff distance (HD95) and average symmetric surface distance (ASD) compared to the current state-of-the-art and performs competitively with privacy-agnostic baselines. Privacy tests confirm strong resistance to inversion and membership attacks, and the overall system achieves real-time inference with low communication overhead. These results demonstrate that accurate and efficient medical image segmentation can be achieved without compromising data privacy in multi-institution settings.

