# Novelty Verification Dossier (Phase 4)

## Verdict Limits

```
=== NOVELTY VERDICT LIMITS (these bound how you judge, never how widely you search) ===
Search exhaustively; judge calibrated. Two failures waste months equally:
passing an idea a published paper already contains, and killing a viable idea
because the territory has neighbors.
1. Proximity is information, not a verdict. Someone working nearby goes in the
   report; it is not by itself a reason to reject.
2. ABANDON has exactly one qualification: a specific published paper already
   contains this result — name that paper. No named paper, no ABANDON.
3. Crowded-but-deltaed is PROCEED: state the delta in one sentence a reviewer
   could verify. Thin or contested delta is PROCEED WITH CAUTION — say what
   would make it carry, not why it should die. CAUTION is not a safe middle:
   if you cannot name the specific thing that makes the delta thin, the
   verdict is PROCEED.
4. Concurrent or competing work is not a veto. That is a race — report it and
   let the user decide whether to run it.
5. A direct attack on a central problem is legitimate novelty when nobody has
   executed it well. "This area is hot" does not mean "this area is taken."
6. This check is an early gate, never the last one — more triage, pilots, or
   external review still stand between any idea and a paper, whatever order
   this run uses. A wrongly passed idea dies cheaply at one of them; a wrongly
   killed idea is never seen again. When torn between two verdicts, choose the
   more permissive one.
Say plainly when an idea clears the check. Do not manufacture overlap.
```

---

## Top 4 Candidates Selected for Deep Novelty Check

### Candidate 1: `idea_003` — Disentangled Morphology-vs-Echotexture Network with Intra-Patient Comparative Normalization (`MorphoTex-CTS`)

#### Core Claims
1. **Claim 1 (Orthogonal Morphology-Echotexture Disentanglement)**: Factorizing transverse carpal tunnel ultrasound into a silhouette-only geometric representation (nerve shape/CSA/flattening ratio) and an orthogonal, shape-invariant intraneural/epineurial echotexture representation prevents CSA size shortcuts from dominating feature learning.
   - *Closest Prior Work*: `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`, ✅ verified via `crossref`) and `Peng et al. (2024)` (`arXiv:2402.05554`, ✅ verified via `arxiv`).
   - *Delta*: `Shinohara et al.` feeds unmasked rectangular crops into a standard CNN (which implicitly entangles nerve size and background geometry with texture), and `Peng et al.` concatenates biometric measurements with CNN features without orthogonality constraints or stage-wise disentanglement.
2. **Claim 2 (Internal Comparative Echogenicity Normalization)**: Normalizing intraneural fascicular texture embeddings against internal reference tissues (adjacent flexor tendons / hypothenar muscle) via cosine-similarity guidance eliminates probe-gain and patient-habitus bias.
   - *Closest Prior Work*: `Sim et al. (2025)` (`10.1016/j.clinph.2025.03.038`, ✅ verified via `crossref`).
   - *Delta*: `Sim et al. (2025)` compares *thenar vs. hypothenar muscle* scans (secondary denervation atrophy in late CTS), whereas `MorphoTex-CTS` normalizes the *median nerve's own intraneural echotexture* against reference tissue and gates it against nerve silhouette morphology across severity stages.
3. **Claim 3 (Stage-Wise Diagnostic Crossover Discovery)**: Quantifying the relative diagnostic weight of echotexture vs. geometry across NCS-confirmed mild, moderate, and severe CTS tests whether intraneural edema/echotexture precedes geometric enlargement (`CSA >= 10 mm²`).
   - *Closest Prior Work*: `Faeghi et al. (2021)` (`10.1016/j.ejrad.2020.109518`, ✅ verified via `crossref`) and `Malo-Urriés et al. (2026)` (`10.20944/preprints202603.0234.v1`, ✅ verified via `crossref`).
   - *Delta*: Neither study decomposes stage-specific predictive power into orthogonal geometric vs. textural axes.

- **Preliminary Novelty Score**: `8.5 / 10`
- **Preliminary Verdict (under Novelty Verdict Limits)**: **PROCEED**
- **One-Sentence Verifiable Delta**: Unlike `Shinohara et al. (2022)` (entangled unmasked CNN) and `Sim et al. (2025)` (thenar/hypothenar muscle comparison), `MorphoTex-CTS` enforces mathematical orthogonality between median-nerve silhouette geometry and reference-normalized intraneural echotexture to resolve stage-specific sensitivity in mild vs. severe CTS.

---

### Candidate 2: `idea_001` — Cross-Modal Knowledge Distillation from Raw Nerve Conduction Waveforms to Point-of-Care B-Mode Ultrasound (`EDX2US-KD`)

#### Core Claims
1. **Claim 1 (Electrophysiology as Privileged Training Information — LUPI)**: Using a teacher network trained on raw motor/sensory nerve conduction time-frequency spectrograms and latencies to supervise an ultrasound-only student via relational + logit distillation transfers continuous physiological severity structure that discrete 4-class labels discard.
   - *Closest Prior Work*: `Bakalis et al. (2024)` (`10.3390/bioengineering11020175`, ✅ verified via `crossref`) and `Malo-Urriés et al. (2026)` (`10.20944/preprints202603.0234.v1`, ✅ verified via `crossref`).
   - *Delta*: `Bakalis et al.` uses NCS waveforms only for an NCS-input classifier; `Malo-Urriés et al.` collapses NCS into coarse 4-class hard labels to train an ultrasound CNN. No published paper performs cross-modal distillation from NCS waveforms/metrics into an ultrasound-only student.
2. **Claim 2 (Inference-Time Non-Invasive Deployment)**: Unlike multimodal fusion models (`Shi et al., 2026`, `10.1016/j.ejrad.2026.113251`, ✅ verified via `crossref`) that require both electrodiagnosis and ultrasound at test time, `EDX2US-KD` requires *only* B-mode ultrasound at inference time.

- **Preliminary Novelty Score**: `8.5 / 10`
- **Preliminary Verdict (under Novelty Verdict Limits)**: **PROCEED**
- **One-Sentence Verifiable Delta**: Whereas `Shi et al. (2026)` requires multimodal EDX + ultrasound inputs at test time and `Malo-Urriés et al. (2026)` trains ultrasound CNNs on hard discretized NCS grades, `EDX2US-KD` distills continuous electrophysiological representations from a privileged NCS teacher into a strictly non-invasive, ultrasound-only inference student.

---

### Candidate 3: `idea_005` — Physics-Guided Speckle-Invariant Test-Time Adaptation for Cross-Vendor Carpal Tunnel Ultrasound (`SpeckleTTA`)

#### Core Claims
1. **Claim 1 (Acoustic Speckle-Prior Test-Time Adaptation)**: Adapting normalization statistics and lightweight spatial adapters on unlabeled test ultrasound scans using a Rayleigh/Nakagami acoustic backscatter prior coupled with nerve-boundary contour entropy minimization mitigates cross-scanner and probe-compression domain shift.
   - *Closest Prior Work*: `Wang et al. (2023)` (`10.1016/j.artmed.2023.102496`, ✅ verified via `crossref`) and `Peng et al. (2024)` (`arXiv:2402.05554`, ✅ verified via `arxiv`).
   - *Delta*: No published CTS median nerve segmentation or diagnostic paper applies test-time adaptation or physics-guided acoustic speckle priors for cross-scanner robustness.

- **Preliminary Novelty Score**: `8.0 / 10`
- **Preliminary Verdict (under Novelty Verdict Limits)**: **PROCEED**
- **One-Sentence Verifiable Delta**: `SpeckleTTA` is the first test-time adaptation framework for carpal tunnel ultrasound that couples Nakagami acoustic speckle distribution priors with boundary-entropy minimization to adapt median nerve segmentation and diagnosis on unseen scanners without target labels.

---

### Candidate 4: `idea_009` — Shortcut Auditing & Frequency-Band Attribution in Ultrasound and NCS Deep Learning Classifiers (`CTS-ShortcutAudit`) + `idea_006` (`ConformalCTS-Gate`)

#### Core Claims
1. **Claim 1 (Counterfactual Nerve-Erased Shortcut Audit)**: Quantifying diagnostic performance when the median nerve ROI is completely masked out (background-only ultrasound) exposes spurious acquisition/depth shortcuts in standard CNNs (`Shinohara et al., 2022`, `10.1016/j.ultrasmedbio.2022.05.030`, ✅ verified via `crossref`).
2. **Claim 2 (Anatomically Constrained Attention + Conformal Deferral)**: Constraining Grad-CAM/attention energy inside the segmented carpal tunnel compartment and calibrating split conformal prediction sets guarantees a bounded false-negative rate (`<=2%`) for non-invasive triage (`Canlı et al., 2024`, `10.1371/journal.pone.0300044`, ✅ verified via `crossref`).

- **Preliminary Novelty Score**: `8.0 / 10`
- **Preliminary Verdict (under Novelty Verdict Limits)**: **PROCEED**
- **One-Sentence Verifiable Delta**: Provides the first quantitative counterfactual shortcut audit (nerve-erased vs. nerve-only vs. full-frame) and distribution-free conformal risk-controlled deferral gate for CTS ultrasound and electrodiagnostic AI.

