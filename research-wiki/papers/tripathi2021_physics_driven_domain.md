---
type: paper
node_id: paper:tripathi2021_physics_driven_domain
title: "Physics Driven Domain Specific Transporter Framework with Attention Mechanism for Ultrasound Imaging"
authors: ["Arpan Tripathi", "Abhilash Rakkunedeth", "Mahesh Raveendranatha Panicker", "Jack Zhang", "Naveenjyote Boora", "Jessica Knight", "Jacob Jaremko", "Yale Tung Chen", "Kiran Vishnu Narayan", "Kesavadas C"]
year: 2021
venue: "arXiv (eess.IV, cs.CV)"
external_ids:
  arxiv: "2109.06346"
  doi: null
  s2: null
tags: ["ultrasound", "physics-informed", "attention", "deep-learning"]
added: 2026-10-30T09:05:09Z
---

# Physics Driven Domain Specific Transporter Framework with Attention Mechanism for Ultrasound Imaging

## One-line thesis
Physics-driven domain-specific transporter network with attention mechanism incorporating acoustic wave propagation priors for robust ultrasound nerve and tissue image representation.

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

> Most applications of deep learning techniques in medical imaging are supervised and require a large number of labeled data which is expensive and requires many hours of careful annotation by experts. In this paper, we propose an unsupervised, physics driven domain specific transporter framework with an attention mechanism to identify relevant key points with applications in ultrasound imaging. The proposed framework identifies key points that provide a concise geometric representation highlighting regions with high structural variation in ultrasound videos. We incorporate physics driven domain specific information as a feature probability map and use the radon transform to highlight features in specific orientations. The proposed framework has been trained on130 Lung ultrasound (LUS) videos and 113 Wrist ultrasound (WUS) videos and validated on 100 Lung ultrasound (LUS) videos and 58 Wrist ultrasound (WUS) videos acquired from multiple centers across the globe. Images from both datasets were independently assessed by experts to identify clinically relevant features such as A-lines, B-lines and pleura from LUS and radial metaphysis, radial epiphysis and carpal bones from WUS videos. The key points detected from both datasets showed high sensitivity (LUS = 99\% , WUS = 74\%) in detecting the image landmarks identified by experts. Also, on employing for classification of the given lung image into normal and abnormal classes, the proposed approach, even with no prior training, achieved an average accuracy of 97\% and an average F1-score of 95\% respectively on the task of co-classification with 3 fold cross-validation. With the purely unsupervised nature of the proposed approach, we expect the key point detection approach to increase the applicability of ultrasound in various examination performed in emergency and point of care.

