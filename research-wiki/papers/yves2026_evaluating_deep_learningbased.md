---
type: paper
node_id: paper:yves2026_evaluating_deep_learningbased
title: "Evaluating Deep Learning-Based Nerve Segmentation in Brachial Plexus Ultrasound Under Realistic Data Constraints"
authors: ["Dylan Yves", "Khush Agarwal", "Jonathan Hoyin Chan", "Patcharapit Promoppatum", "Aroonkamon Pattanasiricharoen"]
year: 2026
venue: "arXiv (cs.CV, cs.AI)"
external_ids:
  arxiv: "2602.00763"
  doi: null
  s2: null
tags: ["ultrasound", "nerve-segmentation", "deep-learning", "data-efficiency"]
added: 2026-10-30T09:05:09Z
---

# Evaluating Deep Learning-Based Nerve Segmentation in Brachial Plexus Ultrasound Under Realistic Data Constraints

## One-line thesis
Systematic evaluation of deep learning peripheral nerve segmentation architectures (U-Net, nnU-Net, Swin-UNet) on ultrasound images under realistic clinical low-data and cross-subject constraints.

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

> Accurate nerve localization is critical for the success of ultrasound-guided regional anesthesia, yet manual identification remains challenging due to low image contrast, speckle noise, and inter-patient anatomical variability. This study evaluates deep learning-based nerve segmentation in ultrasound images of the brachial plexus using a U-Net architecture, with a focus on how dataset composition and annotation strategy influence segmentation performance. We find that training on combined data from multiple ultrasound machines (SIEMENS ACUSON NX3 Elite and Philips EPIQ5) provides regularization benefits for lower-performing acquisition sources, though it does not surpass single-source training when matched to the target domain. Extending the task from binary nerve segmentation to multi-class supervision (artery, vein, nerve, muscle) results in decreased nerve-specific Dice scores, with performance drops ranging from 9% to 61% depending on dataset, likely due to class imbalance and boundary ambiguity. Additionally, we observe a moderate positive correlation between nerve size and segmentation accuracy (Pearson r=0.587, p<0.001), indicating that smaller nerves remain a primary challenge. These findings provide methodological guidance for developing robust ultrasound nerve segmentation systems under realistic clinical data constraints.

