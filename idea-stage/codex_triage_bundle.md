# Idea Triage Bundle (Phase 3 → Phase 4)

Here is the full annotated candidate set (deduped across 5 analytic lenses, filtered ONLY by the Type-A objective feasibility gate).

## Summary of Phase 3 Mechanical Consolidation & Objective Feasibility Gate

- **Generated across 5 lenses (`lens_fanout_receipt.json`)**: `10` candidates (`idea_001`–`idea_010`).
- **Mechanical deduplication**: `0` exact/near duplicates (`10` unique `dedup_key`s).
- **Type-A Objective Feasibility Gate (dropped strictly on unavailable dataset/hardware prerequisites)**:
  - ❌ **Dropped `idea_008`** (*Foundation 3D-Volume Carpal Tunnel Reconstruction from Uncalibrated Freehand 2D Ultrasound Sweeps*): Requires paired 3D MRI / tracked 3D motorized ultrasound ground-truth volumes of the carpal tunnel, which are provably unavailable in public repositories.
  - ❌ **Dropped `idea_010`** (*Counterfactual Individual Treatment Effect Estimation for Conservative vs. Needle Release vs. Open Carpal Tunnel Release*): Requires longitudinal multi-arm interventional clinical trial datasets (splinting vs. US-guided needle release vs. open surgery with 6-month follow-up), which are not publicly available.
- **Surviving Feasible Candidates Entering Phase 4 Triage & Novelty Check**: **8 ideas (`idea_001`–`idea_007`, `idea_009`)**.

---

## Surviving Annotated Candidates (8 Ideas)

### 1. `idea_003` — Disentangled Morphology-vs-Echotexture Network with Intra-Patient Comparative Normalization (`MorphoTex-CTS`)
- **Lens**: `contradiction` (Addresses `G2`)
- **One-sentence summary**: Explicitly factorize carpal tunnel ultrasound into a geometry-only branch (silhouette mask shape/CSA) and a geometry-invariant intraneural texture branch normalized against internal reference tissue, fused via a severity-aware gate.
- **Hypothesis**: Enforcing mutual-information / gradient-reversal orthogonality between binary nerve silhouette geometry and masked intraneural/epineurial echotexture will reveal that texture dominates early/mild CTS (where CSA is still `<10 mm²`) while geometry dominates moderate/severe CTS, and their gated fusion will outperform both CSA-based (`Smerilli et al., 2022`) and CSA-free (`Shinohara et al., 2022`) baselines.
- **Minimum Viable Experiment (MVE)**: On transverse carpal tunnel ultrasound images (Shanghai Sixth Hospital dataset / public benchmarks), train a 2-branch network (Branch A: MLP/PointNet on segmented nerve contour; Branch B: ConvNeXt-Tiny on masked intraneural pixels with cosine-similarity normalization to surrounding tendon/muscle reference ROI and correlation penalty against CSA) and evaluate stage-wise AUROC.
- **`prior_work` annotation**: Closest works are `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`, unmasked CSA-free CNN), `Faeghi et al. (2021)` (`10.1016/j.ejrad.2020.109518`, handcrafted radiomics), and `Sim et al. (2025)` (`10.1016/j.clinph.2025.03.038`, thenar vs. hypothenar muscle comparison). None disentangle median nerve geometry from intraneural texture or quantify their stage-wise contribution across mild vs. severe CTS.
- **`so_what` annotation**: Directly resolves the central clinical debate in CTS ultrasound (CSA cutoffs vs. intrinsic echotexture) and explains *why* CSA fails in early demyelinating CTS, making both positive and negative stage-wise findings immediately publishable.
- **`effort_note` annotation**: `LOW` risk, `2–4 days` implementation on 1 GPU (`<1 GPU-hour` per 5-fold CV run).

### 2. `idea_001` — Cross-Modal Knowledge Distillation from Raw Nerve Conduction Waveforms to Point-of-Care B-Mode Ultrasound (`EDX2US-KD`)
- **Lens**: `method-transfer` (Addresses `G4`, `G2`)
- **One-sentence summary**: Distill electrophysiological functional representations from a privileged teacher trained on raw motor/sensory NCS spectrograms (`Bakalis et al., 2024`) into an ultrasound-only student network (`Malo-Urriés et al., 2026`) so non-invasive B-mode ultrasound alone predicts functional 4-level CTS severity.
- **Hypothesis**: Training a B-mode ultrasound student with contrastive relational + logit knowledge distillation from a privileged NCS-waveform/electrophysiological teacher during training (Privileged Information / LUPI paradigm) will improve ultrasound-only 4-grade severity macro-F1 by `>=5%` over training on discrete NCS severity labels alone, especially at the mild-vs-moderate boundary.
- **Minimum Viable Experiment (MVE)**: Using paired US + EMG/NCS patient records (Shanghai Sixth Hospital dataset, `n=55`, 5-fold subject-wise CV), train Teacher on EDX features/waveforms, Student on B-mode US alone, and compare standard CE vs. `EDX2US-KD` (feature + relational similarity distillation).
- **`prior_work` annotation**: `Malo-Urriés et al. (2026)` (`10.20944/preprints202603.0234.v1`) uses NCS only as hard 4-class target labels for US CNNs; `Shi et al. (2026)` (`10.1016/j.ejrad.2026.113251`) requires both US and EDX at inference time. No prior CTS work uses EDX as privileged training-time teacher representations distilled into an inference-time ultrasound-only student.
- **`so_what` annotation**: Enables painless, non-invasive point-of-care ultrasound to inherit fine-grained physiological severity staging without requiring invasive electrodiagnosis at test time.
- **`effort_note` annotation**: `LOW` risk, `3–5 days` implementation on 1 GPU (`<2 GPU-hours`).

### 3. `idea_005` — Physics-Guided Speckle-Invariant Test-Time Adaptation for Cross-Vendor Carpal Tunnel Ultrasound (`SpeckleTTA`)
- **Lens**: `untested-assumption` (Addresses `G1`)
- **One-sentence summary**: Adapt median nerve segmentation and CTS classification networks at test time on unseen ultrasound machines/Settings using acoustic Rayleigh/Nakagami speckle consistency and boundary-entropy minimization.
- **Hypothesis**: Updating normalization statistics and lightweight spatial adapters at test time via a self-supervised physics loss (enforcing local Nakagami-m speckle statistics in background fascia + sharp low-entropy nerve boundary transitions) will recover `>=60%` of the Dice and AUROC drop under cross-probe frequency, gain, TGC attenuation, and operator compression shifts.
- **Minimum Viable Experiment (MVE)**: Construct a controlled acoustic corruption benchmark (varying speckle scale, depth-dependent attenuation, dynamic range compression, and axial elastic compression) on public nerve segmentation + CTS datasets; compare frozen U-Net/ConvNeXt, Tent, SAR, and `SpeckleTTA`.
- **`prior_work` annotation**: `Wang et al. (2023)` (`10.1016/j.artmed.2023.102496`) highlights cross-machine generalization as a primary bottleneck in median nerve segmentation, yet all 20 reviewed CTS DL papers evaluate frozen weights without test-time adaptation.
- **`so_what` annotation**: Solves the #1 clinical deployment barrier for point-of-care wrist ultrasound AI across heterogeneous hospital scanners with zero target-domain labels.
- **`effort_note` annotation**: `LOW` risk, `3–4 days` implementation on 1 GPU (`<2 GPU-hours`).

### 4. `idea_009` — Shortcut Auditing & Frequency-Band Attribution in Ultrasound and NCS Deep Learning Classifiers (`CTS-ShortcutAudit`)
- **Lens**: `diagnostic` (Addresses `G1`, `G2`)
- **One-sentence summary**: Audit the extent to which high-accuracy CTS ultrasound CNNs (`96%` in `Shinohara et al., 2022`) rely on non-anatomical background/acquisition shortcuts vs. true median nerve pathology, and introduce an anatomically masked attention regularizer.
- **Hypothesis**: Training standard CNNs/ViTs on background-only images (with the median nerve completely zeroed out) will still achieve unexpectedly high accuracy (`>70%`) on single-center CTS datasets due to probe depth, gain, and retinaculum depth shortcuts, whereas enforcing an anatomical ROI-attention loss eliminates shortcut reliance and improves out-of-distribution generalization.
- **Minimum Viable Experiment (MVE)**: Evaluate 4 input ablations across ResNet-50, ConvNeXt, and ViT: (1) Full US frame, (2) Nerve-only crop, (3) Nerve-erased background-only frame, (4) High/low spatial-frequency filtered frames; then benchmark standard training vs. Right-for-the-Right-Reasons anatomical attention regularization.
- **`prior_work` annotation**: `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`) and `Peng et al. (2024)` (`arXiv:2402.05554`) use qualitative Grad-CAM heatmaps on selected examples, but no quantitative counterfactual masking or frequency-shortcut audit exists in CTS ultrasound AI.
- **`so_what` annotation**: High-impact diagnostic contribution: whether existing CNNs pass or fail the nerve-erased test, the empirical finding directly reshapes evaluation standards in neuromuscular ultrasound AI.
- **`effort_note` annotation**: `LOW` risk, `2–3 days` implementation on 1 GPU (`<1 GPU-hour`).

### 5. `idea_004` — Spatiotemporal Kinematic-Deformation Transformer on Dynamic Cine-Loop Ultrasound (`GlideFormer-CTS`)
- **Lens**: `contradiction` (Addresses `G3`)
- **One-sentence summary**: Jointly model median nerve centroid excursion kinematics and continuous cross-sectional boundary strain/circularity deformation across dynamic finger/wrist flexion cine loops.
- **Hypothesis**: Coupling trajectory kinematics (radial-ulnar/dorsal-palmar velocity and acceleration) with frame-to-frame nerve contour Fourier-descriptor deformation tokens in a temporal Transformer will significantly beat centroid-only tracking (`Tanaka et al., 2023`) and static CSA (`Smerilli et al., 2022`) in detecting early tethering in mild CTS.
- **Minimum Viable Experiment (MVE)**: Extract per-frame median nerve masks across cine-loop sequences using U-Net (`Festen et al., 2021`), compute kinematic + shape-strain token sequences, and compare a 2-layer temporal Transformer against static CSA and centroid displacement velocity alone.
- **`prior_work` annotation**: `Horng et al. (2020)` (`10.1016/j.ultrasmedbio.2020.03.017`) and `Festen et al. (2021)` (`10.1016/j.ultrasmedbio.2021.03.018`) focus on dynamic segmentation accuracy (Dice), while `Tanaka et al. (2023)` (`10.3390/app132413256`) tracks only bounding-box centroid displacement/velocity via YOLOv5 without continuous contour strain/deformation tokens.
- **`so_what` annotation**: Captures biomechanical nerve compression and subsynovial tethering during motion, addressing cases where static wrist ultrasound appears normal.
- **`effort_note` annotation**: `MEDIUM` risk, `1–2 weeks` implementation (`~2 GPU-hours`).

### 6. `idea_006` — Conformal Risk-Controlled Deferral for Two-Stage Non-Invasive-to-EDX Clinical Triage (`ConformalCTS-Gate`)
- **Lens**: `untested-assumption` (Addresses `G5`)
- **One-sentence summary**: Formulate CTS diagnosis as a two-stage conformal risk-controlled deferral pipeline that guarantees a user-specified false-negative ceiling (`alpha <= 2%`) using non-invasive screening (anthropometrics + symptoms + US) and defers only ambiguous cases to invasive NCS.
- **Hypothesis**: Calibrating split conformal prediction sets and Learn-then-Test risk control over a multimodal non-invasive ensemble will safely spare `>=45%` of patients from painful electrodiagnostic testing while mathematically bounding missed moderate/severe CTS below `2%`.
- **Minimum Viable Experiment (MVE)**: On tabular clinical/anthropometric (`Canlı et al., 2024`; `Park et al., 2021`) and ultrasound cohorts, compare naive softmax thresholding vs. temperature scaling vs. Conformal Risk Control across 100 random calibration/test splits.
- **`prior_work` annotation**: `Canlı et al. (2024)` (`10.1371/journal.pone.0300044`) and `Park et al. (2021)` (`10.1038/s41598-021-97043-7`) report point-estimate accuracy/AUROC without distribution-free false-negative guarantees or selective deferral to EDX.
- **`so_what` annotation**: Directly actionable clinical decision-support contribution: clinicians care about guaranteed sensitivity/false-negative bounds when deciding whether to skip NCS.
- **`effort_note` annotation**: `LOW` risk, `2–3 days` implementation on CPU/1 GPU (`<0.5 GPU-hours`).

### 7. `idea_007` — Cross-Anatomy Peripheral Nerve Self-Supervised Pre-Training for Few-Shot Median Nerve Segmentation (`NerveMAE`)
- **Lens**: `scaling-regime` (Addresses `G1`)
- **One-sentence summary**: Pre-train a speckle-tube Masked Autoencoder on large public peripheral nerve ultrasound datasets (e.g., 5,635 brachial plexus images) to achieve high-accuracy median nerve segmentation and CTS diagnosis in low-label regimes (`<=20` labeled wrists).
- **Hypothesis**: Domain-specific self-supervised pre-training on heterogeneous peripheral nerve ultrasound images with speckle-scale masking will improve 10-shot and 20-shot median nerve Dice by `>=4%` over ImageNet-pretrained encoders.
- **Minimum Viable Experiment (MVE)**: Pre-train ConvNeXt-V2 / ViT-Small MAE on the public Kaggle Brachial Plexus Ultrasound Nerve dataset (`5,635` images), fine-tune on `{5, 10, 20, 50}` labeled carpal tunnel frames, and compare Dice/HD95 against ImageNet-init and scratch training.
- **`prior_work` annotation**: `Smerilli et al. (2022)` (`10.1186/s13075-022-02729-6`), `Di Cosmo et al. (2022)` (`10.1007/s11517-022-02662-5`), and `Peng et al. (2024)` (`arXiv:2402.05554`) rely exclusively on ImageNet pre-training.
- **`so_what` annotation**: Enables small rheumatology/orthopedic clinics to adapt median nerve segmentation models to their own ultrasound scanner with only 10–20 annotated scans.
- **`effort_note` annotation**: `LOW` risk, `3–5 days` implementation (`~3 GPU-hours`).

### 8. `idea_002` — Anatomical-Graph Neural Network over Carpal Tunnel Structure Topology (`CarpalGraph-Net`)
- **Lens**: `method-transfer` (Addresses `G2`)
- **One-sentence summary**: Represent the carpal tunnel inlet as an anatomical graph connecting the median nerve, nine flexor tendons, and flexor retinaculum to capture compartmental crowding and relative echogenicity.
- **Hypothesis**: Relational message passing (`GATv2`) over multi-structure anatomical nodes (size, relative distance, bowing angle, and tendon-to-nerve echogenicity ratio) will outperform isolated median-nerve CNNs in atypical/bifid anatomy and mild CTS.
- **Minimum Viable Experiment (MVE)**: Segment/detect median nerve + surrounding flexor tendons on transverse ultrasound images, build a spatial graph with relative geometric and echotextural edge features, and compare `CarpalGraph-Net` against isolated nerve CNNs.
- **`prior_work` annotation**: `Sim et al. (2025)` (`10.1016/j.clinph.2025.03.038`) compares only two muscle ROIs (thenar vs. hypothenar), while `Peng et al. (2024)` (`arXiv:2402.05554`) crops only the median nerve. None model the multi-tendon carpal tunnel compartment as a graph.
- **`so_what` annotation**: Reflects the true biomechanical etiology of CTS (compartmental crowding and retinacular bowing compressing the median nerve against flexor tendons).
- **`effort_note` annotation**: `MEDIUM` risk, `1–2 weeks` implementation (`~2 GPU-hours`; requires multi-structure pseudo-labels or SAM-assisted tendon masks).

---

## Triage Instructions for Reviewer

For each candidate above, make the strongest case both ways:
- What is the best case FOR it — what would make this the paper people cite?
- What's the strongest objection a reviewer would raise?
- What's the most likely failure mode?
- Is the `prior_work` note a real novelty problem, or differentiable?
- Rank by expected information and upside within the pilot budget — which results would matter most, whichever way they come out?
- Which 2–3 would you actually work on, and why?

