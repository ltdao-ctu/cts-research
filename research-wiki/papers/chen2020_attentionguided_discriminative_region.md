---
type: paper
node_id: paper:chen2020_attentionguided_discriminative_region
title: "Attention-Guided Discriminative Region Localization and Label Distribution Learning for Bone Age Assessment"
authors: ["Chao Chen", "Zhihong Chen", "Xinyu Jin", "Lanjuan Li", "William Speier", "Corey W. Arnold"]
year: 2020
venue: "arXiv (cs.CV)"
external_ids:
  arxiv: "2006.00202"
  doi: null
  s2: null
tags: ["wrist-xray", "attention", "label-distribution-learning", "deep-learning"]
added: 2026-10-30T09:05:09Z
---

# Attention-Guided Discriminative Region Localization and Label Distribution Learning for Bone Age Assessment

## One-line thesis
Attention-guided discriminative region localization and label distribution learning for automated hand and wrist radiograph assessment.

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

> Bone age assessment (BAA) is clinically important as it can be used to diagnose endocrine and metabolic disorders during child development. Existing deep learning based methods for classifying bone age use the global image as input, or exploit local information by annotating extra bounding boxes or key points. However, training with the global image underutilizes discriminative local information, while providing extra annotations is expensive and subjective. In this paper, we propose an attention-guided approach to automatically localize the discriminative regions for BAA without any extra annotations. Specifically, we first train a classification model to learn the attention maps of the discriminative regions, finding the hand region, the most discriminative region (the carpal bones), and the next most discriminative region (the metacarpal bones). Guided by those attention maps, we then crop the informative local regions from the original image and aggregate different regions for BAA. Instead of taking BAA as a general regression task, which is suboptimal due to the label ambiguity problem in the age label space, we propose using joint age distribution learning and expectation regression, which makes use of the ordinal relationship among hand images with different individual ages and leads to more robust age estimation. Extensive experiments are conducted on the RSNA pediatric bone age data set. Using no training annotations, our method achieves competitive results compared with existing state-of-the-art semi-automatic deep learning-based methods that require manual annotation. Code is available at https: //github.com/chenchao666/Bone-Age-Assessment.

