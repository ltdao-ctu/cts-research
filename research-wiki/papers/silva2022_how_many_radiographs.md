---
type: paper
node_id: paper:silva2022_how_many_radiographs
title: "How many radiographs are needed to re-train a deep learning system for object detection?"
authors: ["Raniere Silva", "Khizar Hayat", "Christopher M Riggs", "Michael Doube"]
year: 2022
venue: "arXiv (eess.IV, cs.CV)"
external_ids:
  arxiv: "2210.08734"
  doi: null
  s2: null
tags: ["wrist-xray", "object-detection", "sample-efficiency", "deep-learning"]
added: 2026-10-30T09:05:09Z
---

# How many radiographs are needed to re-train a deep learning system for object detection?

## One-line thesis
Empirical sample-efficiency study quantifying how many labeled wrist radiographs are required to fine-tune and re-train deep learning object detection models across clinical sites.

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

> Background: Object detection in radiograph computer vision has largely benefited from progress in deep convolutional neural networks and can, for example, annotate a radiograph with a box around a knee joint or intervertebral disc. Is deep learning capable of detect small (less than 1% of the image) in radiographs? And how many radiographs do we need use when re-training a deep learning model?   Methods: We annotated 396 radiographs of left and right carpi dorsal 75 medial to palmarolateral oblique (DMPLO) projection with the location of radius, proximal row of carpal bones, distal row of carpal bones, accessory carpal bone, first carpal bone (if present), and metacarpus (metacarpal II, III, and IV). The radiographs and respective annotations were splited into sets that were used to leave-one-out cross-validation of models created using transfer learn from YOLOv5s.   Results: Models trained using 96 radiographs or more achieved precision, recall and mAP above 0.95, including for the first carpal bone, when trained for 32 epochs. The best model needed the double of epochs to learn to detect the first carpal bone compared with the other bones.   Conclusions: Free and open source state of the art object detection models based on deep learning can be re-trained for radiograph computer vision applications with 100 radiographs and achieved precision, recall and mAP above 0.95.

