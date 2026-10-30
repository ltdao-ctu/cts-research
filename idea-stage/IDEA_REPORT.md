# Idea Discovery Report: Carpal Tunnel Syndrome Diagnosis Using Machine Learning & Deep Learning

**Direction**: `carpal tunnel syndrome diagnosis using machine learning or deep learning`
**Date**: 2026-10-30
**Run ID**: `cts_ml_dl_20261030`
**Reviewer Route**: `manual` (`— reviewer: manual` — `REVIEW_UNAVAILABLE` pending manual external reviewer input; see [`idea-stage/codex_triage_bundle.md`](./codex_triage_bundle.md) and [`idea-stage/NOVELTY_DOSSIER.md`](./NOVELTY_DOSSIER.md))
**Ideas Evaluated**: `10` generated across 5 analytic lenses → `8` survived Type-A objective feasibility gate → `4` top-tier ideas deep-verified for novelty

---

## Executive Summary

Using the 21 verified papers and 5 structural field gaps (`G1`–`G5`) compiled in `research-wiki/`, we executed a 5-lens generation fan-out producing **10 concrete method ideas** (`idea_001`–`idea_010`), mechanically deduplicated them (`10` unique hypotheses), and applied the Type-A objective feasibility gate (`8` feasible on public/standard clinical datasets; `2` archived due to unavailable 3D volumetric MRI/US or multi-arm longitudinal trial data). Deep novelty verification against 2020–2026 literature confirmed strong, verifiable differentiation (`PROCEED`, novelty `8.0–8.5/10`) for the top four directions:
1. **`MorphoTex-CTS` (`idea_003`)**: Orthogonal disentanglement of median nerve silhouette geometry (CSA/flattening) vs. reference-normalized intraneural echotexture across CTS severity stages.
2. **`EDX2US-KD` (`idea_001`)**: Cross-modal knowledge distillation from privileged raw nerve conduction (NCS) time-frequency teachers into a non-invasive, ultrasound-only student.
3. **`SpeckleTTA` (`idea_005`)**: Physics-guided Nakagami/Rayleigh speckle-invariant test-time adaptation for cross-scanner carpal tunnel ultrasound segmentation and grading.
4. **`CTS-ShortcutAudit` & `ConformalCTS-Gate` (`idea_009` + `idea_006`)**: Counterfactual nerve-erased shortcut auditing combined with split conformal risk-controlled deferral (`<=2%` false-negative bound).

---

## Literature Landscape {#literature-landscape}

1. **Automated Median Nerve Segmentation & Biometrics**: Mask R-CNN (`Smerilli et al., 2022`, `10.1186/s13075-022-02729-6`; `Di Cosmo et al., 2021/2022`, `10.1109/EMBC46164.2021.9631057`, `10.1007/s11517-022-02662-5`) and U-Net (`Festen et al., 2021`, `10.1016/j.ultrasmedbio.2021.03.018`) reach pooled Dice scores of `0.88–0.91` (`Wang et al., 2023`, `10.1016/j.artmed.2023.102496`). `Peng et al. (2024)` (`arXiv:2402.05554`, `10.1016/j.ultrasmedbio.2023.10.009`) unified real-time segmentation, biometric CSA calculation, and explainable diagnosis into OSA-CTSD.
2. **Morphological Cutoffs vs. Intrinsic Echotexture**: While traditional ultrasound relies on fixed CSA cutoffs (`9–12 mm²`), `Faeghi et al. (2021)` (`10.1016/j.ejrad.2020.109518`) and `Wu et al. (2023)` (`10.3390/diagnostics13203280`) showed intraneural radiomics reaches `~88%` sensitivity/specificity. `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`) achieved `96%` accuracy with CSA-free CNNs, and `Sim et al. (2025)` (`10.1016/j.clinph.2025.03.038`) introduced cosine-similarity comparative guidance between thenar and hypothenar muscle ultrasound scans.
3. **Dynamic Kinematic Ultrasound & Raw Waveform Electrodiagnosis**: Dynamic cine-loop studies (`Horng et al., 2020`, `10.1016/j.ultrasmedbio.2020.03.017`; `Wang et al., 2020`, `10.1016/j.compmedimag.2019.101687`; `Festen et al., 2021`; `Tanaka et al., 2023`, `10.3390/app132413256`) track nerve displacement and velocity during finger flexion. On the electrodiagnostic side, `Bakalis et al. (2024)` (`10.3390/bioengineering11020175`) trained 2D CNNs on STFT spectrograms and wavelets of raw motor/sensory nerve conduction signals (`94–97.1%` accuracy), while `Malo-Urriés et al. (2026)` (`10.20944/preprints202603.0234.v1`) and `Shi et al. (2026)` (`10.1016/j.ejrad.2026.113251`) targeted 4-class NCS-anchored severity grading and multicenter post-release outcome prediction.

---

## Ranked Ideas {#ranked-ideas}

### 🏆 Idea 1 (`idea_003`): Disentangled Morphology-vs-Echotexture Network with Intra-Patient Comparative Normalization (`MorphoTex-CTS`) — **RECOMMENDED #1**
- **Method (what we actually do)**:
  1. Segment the median nerve and an adjacent internal reference region (flexor tendon / hypothenar muscle) on transverse B-mode carpal tunnel ultrasound images.
  2. Feed the binary nerve silhouette mask into a lightweight geometric encoder (extracting CSA, perimeter, circularity, and flattening ratio) and feed the masked intraneural/epineurial pixels into a texture encoder normalized via cosine similarity against the internal reference tissue.
  3. Enforce mathematical orthogonality (gradient reversal + distance correlation penalty) between the texture embedding and nerve CSA so the texture branch cannot cheat via nerve size.
  4. Combine both branches through a learned severity-stage gate that outputs CTS diagnosis, 4-level severity grade, and the exact percentage attribution to morphology vs. echotexture.
- **Hypothesis**: Orthogonalizing median nerve silhouette geometry and reference-normalized intraneural echotexture will reveal a clinical crossover — intraneural texture dominates early/mild CTS (`CSA < 10 mm²`) whereas geometry dominates moderate/severe CTS — and their gated fusion will outperform both CSA-cutoff (`Smerilli et al., 2022`) and unmasked CNN (`Shinohara et al., 2022`) baselines by `>=3–5%` macro-F1.
- **Minimum Viable Experiment (MVE)**: 5-fold patient-level cross-validation on transverse carpal tunnel ultrasound images (Shanghai Sixth People's Hospital dataset + public nerve benchmarks), comparing (a) CSA-only logistic/MLP, (b) unmasked ResNet-50/ConvNeXt (`Shinohara et al., 2022`), (c) masked texture-only CNN, and (d) `MorphoTex-CTS` with orthogonality loss.
- **Expected Outcome**: Clear quantitative stage-wise crossover curve (texture AUROC > geometry AUROC in mild CTS; gated fusion highest overall). Even a null result (geometry or texture dominating across all stages) settles a major clinical debate.
- **Novelty**: `8.5 / 10` (`PROCEED`) — Closest work: `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`) and `Sim et al. (2025)` (`10.1016/j.clinph.2025.03.038`).
- **Feasibility**: `2–4 days`, `<1 GPU-hour` on 1 GPU, works on standard static B-mode wrist ultrasound datasets.
- **Risk**: `LOW`
- **Contribution Type**: New method + diagnostic empirical finding (addresses Gap `G2`).
- **Pilot Result**: `SKIPPED: ready for pilot deployment (<1 GPU-hour)`.
- **Reviewer's Likely Objection**: "Does masking the median nerve discard perineurial/retinaculum context outside the nerve boundary?" — *Mitigation*: Include an ablation with a dilated (`+15%` radius) epineurial ring branch while still zeroing out nerve area scale.

---

### 🥈 Idea 2 (`idea_001`): Cross-Modal Knowledge Distillation from Raw Nerve Conduction Waveforms to Point-of-Care B-Mode Ultrasound (`EDX2US-KD`) — **RECOMMENDED #2**
- **Method (what we actually do)**:
  1. Train a privileged teacher network on paired electrophysiological data (motor/sensory STFT spectrograms, distal latencies, amplitudes, and conduction velocities following `Bakalis et al., 2024` and `Park et al., 2021`).
  2. Train a B-mode ultrasound-only student network (`ConvNeXt-Tiny` / `Swin-T`) on the corresponding wrist ultrasound images.
  3. Supervise the ultrasound student jointly with ground-truth severity labels, temperature-scaled teacher logits, and a contrastive relational similarity loss (Relational Knowledge Distillation) that preserves pairwise inter-patient physiological distances in the ultrasound embedding space.
  4. At test time, discard the EDX teacher completely and predict 4-level functional CTS severity using only non-invasive B-mode ultrasound.
- **Hypothesis**: Distilling continuous physiological representations from a privileged NCS teacher during training (Learning Using Privileged Information) will boost ultrasound-only 4-class severity grading macro-F1 by `>=5%` over standard hard-label supervision (`Malo-Urriés et al., 2026`), particularly at the clinically ambiguous mild-vs-moderate boundary.
- **Minimum Viable Experiment (MVE)**: 5-fold subject-wise CV on the public Shanghai Sixth Hospital paired US + EMG/NCS dataset (`n=55` patients) comparing hard-label ultrasound CNN vs. logit KD vs. relational + feature KD (`EDX2US-KD`).
- **Expected Outcome**: Improved mild/moderate F1 and better calibration against continuous distal motor/sensory latency values using ultrasound alone at inference.
- **Novelty**: `8.5 / 10` (`PROCEED`) — Closest work: `Malo-Urriés et al. (2026)` (`10.20944/preprints202603.0234.v1`) and `Shi et al. (2026)` (`10.1016/j.ejrad.2026.113251`).
- **Feasibility**: `3–5 days`, `<2 GPU-hours` on 1 GPU, public paired dataset available on Zenodo.
- **Risk**: `LOW`
- **Contribution Type**: New method (addresses Gaps `G4`, `G2`).
- **Pilot Result**: `SKIPPED: ready for pilot deployment (<2 GPU-hours)`.
- **Reviewer's Likely Objection**: "Paired US+EDX datasets are often small (`n=50–200`), risking teacher overfitting." — *Mitigation*: Regularize the teacher with physiological monotonicity constraints and evaluate relational distance distillation (which transfers geometry rather than high-dimensional parameters).

---

### 🥉 Idea 3 (`idea_005`): Physics-Guided Speckle-Invariant Test-Time Adaptation for Cross-Vendor Carpal Tunnel Ultrasound (`SpeckleTTA`) — **RECOMMENDED #3 (Backup)**
- **Method (what we actually do)**:
  1. Attach lightweight affine normalization parameters and a shallow spatial adapter to a pre-trained median nerve segmentation + CTS diagnostic network (`OSA-CTSD` style).
  2. When deployed on an unseen target ultrasound scanner or probe setting, estimate local acoustic speckle statistics (Nakagami-$m$ shape and scale parameters) in non-nerve background tissue and compute boundary contour entropy along the predicted median nerve perimeter.
  3. Run 1–3 gradient steps per test patient/video to minimize the divergence between canonical acoustic backscatter statistics and minimize boundary contour entropy, without requiring any target labels.
- **Hypothesis**: Physics-guided speckle and boundary-entropy test-time adaptation will recover `>=60%` of the segmentation Dice and diagnostic AUROC lost under cross-vendor frequency, gain, TGC attenuation, and operator probe-pressure shifts.
- **Minimum Viable Experiment (MVE)**: Evaluate source-trained U-Net / Mask R-CNN + classifier across physics-based ultrasound shift benchmarks (acoustic frequency/speckle scaling, depth attenuation, axial compression deformation) against Frozen, Tent, SAR, and `SpeckleTTA`.
- **Novelty**: `8.0 / 10` (`PROCEED`) — Closest work: `Wang et al. (2023)` (`10.1016/j.artmed.2023.102496`) and `Peng et al. (2024)` (`arXiv:2402.05554`).
- **Feasibility**: `3–4 days`, `<2 GPU-hours` on 1 GPU.
- **Risk**: `LOW`
- **Contribution Type**: New method (addresses Gap `G1`).

---

### Idea 4 (`idea_009` + `idea_006`): Counterfactual Shortcut Auditing & Conformal Risk-Controlled Deferral (`CTS-ShortcutAudit` + `ConformalCTS-Gate`) — **RECOMMENDED #4 (Diagnostic / Clinical Safety)**
- **Method (what we actually do)**:
  1. Train and evaluate standard ultrasound CNNs across four counterfactual inputs: (a) Full image, (b) Median-nerve crop only, (c) Nerve-erased background-only image, and (d) Frequency-band filtered images to quantify background shortcut leakage.
  2. Add an anatomical ROI-attention penalty ("Right-for-the-Right-Reasons") that penalizes Grad-CAM energy outside the carpal tunnel compartment.
  3. Wrap the shortcut-cleaned classifier in a Split Conformal Risk Controller that outputs singleton diagnoses for high-confidence cases and defers ambiguous multi-label prediction sets to invasive nerve conduction studies (NCS) under a strict false-negative bound (`alpha <= 2%`).
- **Hypothesis**: Unconstrained CNNs achieve `>70%` accuracy even on nerve-erased background images due to acquisition shortcuts; removing these shortcuts and applying conformal risk control safely eliminates `>=45%` of invasive NCS referrals while bounding missed moderate/severe CTS below `2%`.
- **Minimum Viable Experiment (MVE)**: Run the 4-way counterfactual masking audit on ResNet-50/ConvNeXt/ViT and evaluate split conformal deferral curves at `alpha in {0.01, 0.02, 0.05}`.
- **Novelty**: `8.0 / 10` (`PROCEED`) — Closest work: `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`) and `Canlı et al. (2024)` (`10.1371/journal.pone.0300044`).
- **Feasibility**: `2–3 days`, `<1 GPU-hour` on 1 GPU.
- **Risk**: `LOW`
- **Contribution Type**: Diagnostic + clinical decision-support method (addresses Gaps `G1`, `G5`).

---

### Additional Feasible Candidates Retained in Pool (`idea_004`, `idea_007`, `idea_002`)
- **Idea 5 (`idea_004` — `GlideFormer-CTS`)**: Spatiotemporal Kinematic-Deformation Transformer combining centroid excursion velocity (`Tanaka et al., 2023`, `10.3390/app132413256`) with continuous Fourier contour strain tokens across dynamic finger-flexion cine loops (`Festen et al., 2021`, `10.1016/j.ultrasmedbio.2021.03.018`). (`MEDIUM` risk, `1–2 weeks`, addresses `G3`).
- **Idea 6 (`idea_007` — `NerveMAE`)**: Cross-anatomy self-supervised Masked Autoencoder pre-trained on 5,635 brachial plexus ultrasound images for 10-shot/20-shot median nerve segmentation and CTS grading. (`LOW` risk, `3–5 days`, addresses `G1`).
- **Idea 7 (`idea_002` — `CarpalGraph-Net`)**: Relational Graph Attention Network (`GATv2`) modeling the spatial topology and relative echogenicity of the median nerve, nine flexor tendons, and flexor retinaculum. (`MEDIUM` risk, `1–2 weeks`, addresses `G2`).

---

## Novelty Verification {#novelty-verification}

All closest prior works cited below passed deterministic pre-search verification via `verify_papers.py` ([`verified_papers.json`](../.aris/verify-papers/verified_papers.json) and [`novelty_verified.json`](../.aris/verify-papers/novelty_verified.json), `verdict: PASS`, `hallucination_rate: 0.0`). Full claim-by-claim analysis and verbatim verdict limits are recorded in [`idea-stage/NOVELTY_DOSSIER.md`](./NOVELTY_DOSSIER.md).

| Candidate Idea | Closest Verified Prior Work | Overlap | Verifiable Delta | Score & Recommendation |
|---|---|---|---|---|
| **Idea 1 (`MorphoTex-CTS`, `idea_003`)** | `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`); `Sim et al. (2025)` (`10.1016/j.clinph.2025.03.038`); `Faeghi et al. (2021)` (`10.1016/j.ejrad.2020.109518`) | Uses ultrasound texture/CNN features for CTS diagnosis without manual CSA cutoffs | Enforces mathematical orthogonality between median-nerve silhouette geometry and reference-normalized intraneural echotexture to quantify stage-wise crossover across mild vs. severe CTS | **8.5 / 10 — PROCEED** |
| **Idea 2 (`EDX2US-KD`, `idea_001`)** | `Malo-Urriés et al. (2026)` (`10.20944/preprints202603.0234.v1`); `Bakalis et al. (2024)` (`10.3390/bioengineering11020175`); `Shi et al. (2026)` (`10.1016/j.ejrad.2026.113251`) | Links B-mode ultrasound with NCS severity grades or fuses US + EDX at test time | Uses raw NCS spectrograms/metrics as *privileged training-time teacher representations* (LUPI) distilled via relational KD into a strictly non-invasive *ultrasound-only inference student* | **8.5 / 10 — PROCEED** |
| **Idea 3 (`SpeckleTTA`, `idea_005`)** | `Peng et al. (2024)` (`arXiv:2402.05554`); `Wang et al. (2023)` (`10.1016/j.artmed.2023.102496`) | Automated median nerve segmentation and CTS classification on B-mode ultrasound | First test-time adaptation framework for carpal tunnel ultrasound combining Rayleigh/Nakagami acoustic speckle priors with nerve-boundary entropy minimization | **8.0 / 10 — PROCEED** |
| **Idea 4 (`CTS-ShortcutAudit` + `ConformalCTS-Gate`, `idea_009` + `idea_006`)** | `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`); `Canlı et al. (2024)` (`10.1371/journal.pone.0300044`) | Grad-CAM visualization on CTS CNNs and non-invasive CTS screening | First counterfactual nerve-erased shortcut audit in CTS ultrasound paired with split conformal prediction sets that guarantee a bounded false-negative rate (`<=2%`) for EDX deferral | **8.0 / 10 — PROCEED** |

---

## External Critical Review {#external-critical-review}

- **Reviewer Route Status**: `REVIEW_UNAVAILABLE` (invoked with `— reviewer: manual`; `mcp__manual_review__review` MCP server is not registered in the current environment, so no external cross-family `Reviewer-Model:` receipt has been recorded yet).
- **Ready-to-Paste Bundles for Manual Cross-Model Review**:
  - Brainstorm bundle: [`idea-stage/codex_brainstorm_bundle.md`](./codex_brainstorm_bundle.md)
  - Triage / Devil's-Advocate bundle: [`idea-stage/codex_triage_bundle.md`](./codex_triage_bundle.md)
  - Novelty Dossier: [`idea-stage/NOVELTY_DOSSIER.md`](./NOVELTY_DOSSIER.md)
- **How to Complete Manual Review**: Paste [`idea-stage/codex_triage_bundle.md`](./codex_triage_bundle.md) or [`idea-stage/NOVELTY_DOSSIER.md`](./NOVELTY_DOSSIER.md) into an external reviewer model (e.g., OpenAI GPT/o-series or Anthropic Claude, beginning the reply with `Reviewer-Model: <exact-model-id>`) and return the response here, or select one of the top ideas directly to proceed to `/research-refine-pipeline` and experiment implementation.

---

## Eliminated Ideas {#eliminated-ideas}

| ID | Idea | Phase Eliminated | Objective Reason (Type-A Gate) |
|---|---|---|---|
| `idea_008` | *Foundation 3D-Volume Carpal Tunnel Reconstruction from Uncalibrated Freehand 2D Ultrasound Sweeps* | Phase 3 (Objective Feasibility Gate) | Requires paired 3D volumetric MRI or tracked 3D motorized ultrasound ground-truth volumes of the carpal tunnel, which are provably unavailable in public repositories. |
| `idea_010` | *Counterfactual Individual Treatment Effect (ITE) Estimation for Conservative vs. Needle Release vs. Open Carpal Tunnel Release* | Phase 3 (Objective Feasibility Gate) | Requires longitudinal multi-arm interventional clinical trial datasets (splinting vs. US-guided needle release vs. open surgery with 6-month follow-up), which are not publicly available. |

---

## Next Steps

- [ ] Select **Idea 1 (`MorphoTex-CTS`)** or **Idea 2 (`EDX2US-KD`)** (or provide your manual reviewer response starting with `Reviewer-Model: <exact-model-id>`) to run Phase 4.5 (`/research-refine-pipeline`) and generate `refine-logs/FINAL_PROPOSAL.md` + `refine-logs/EXPERIMENT_PLAN.md`.
- [ ] Run `/run-experiment` to execute the 5-fold cross-validation pilot on the public paired ultrasound/EMG dataset.

