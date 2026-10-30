# Idea Generation Bundle (Phase 2)

You are a senior ML researcher brainstorming research ideas.

**Research direction:** Carpal tunnel syndrome diagnosis using machine learning or deep learning

## Current Literature Landscape (21 Verified Papers)

- **Ultrasound Segmentation & Biometrics:** Mask R-CNN (`Smerilli et al., 2022`, `10.1186/s13075-022-02729-6`; `Di Cosmo et al., 2021/2022`, `10.1109/EMBC46164.2021.9631057`, `10.1007/s11517-022-02662-5`) and U-Net (`Festen et al., 2021`, `10.1016/j.ultrasmedbio.2021.03.018`) achieve ~0.88–0.91 pooled Dice (`Wang et al., 2023`, `10.1016/j.artmed.2023.102496`). `Peng et al. (2024)` (`arXiv:2402.05554`, `10.1016/j.ultrasmedbio.2023.10.009`) unified segmentation, CSA measurement, and explainable diagnosis into OSA-CTSD.
- **CSA-Free Echotexture & Comparative Guidance:** `Faeghi et al. (2021)` (`10.1016/j.ejrad.2020.109518`) and `Wu et al. (2023)` (`10.3390/diagnostics13203280`) showed intraneural radiomics reaches ~88% sensitivity/specificity. `Shinohara et al. (2022)` (`10.1016/j.ultrasmedbio.2022.05.030`) trained CSA-free CNNs (96% accuracy). `Sim et al. (2025)` (`10.1016/j.clinph.2025.03.038`) introduced cosine-similarity comparative guidance between thenar and hypothenar muscle ultrasound images.
- **Dynamic / Kinematic Cine-Loop Ultrasound:** `Horng et al. (2020)` (`10.1016/j.ultrasmedbio.2020.03.017`, DeepNerve), `Wang et al. (2020)` (`10.1016/j.compmedimag.2019.101687`, MNT-DeepSL), `Festen et al. (2021)` (`10.1016/j.ultrasmedbio.2021.03.018`), and `Tanaka et al. (2023)` (`10.3390/app132413256`, YOLOv5 tracking) analyze median nerve displacement and velocity during finger/wrist motion.
- **Electrodiagnosis (EDX/NCS) & Multimodal Severity/Prognosis:** `Bakalis et al. (2024)` (`10.3390/bioengineering11020175`) applied 2D CNNs to STFT spectrograms and wavelets of raw motor/sensory nerve conduction waveforms (94–97.1% accuracy). `Tsamis et al. (2021)` (`10.3390/bioengineering8110181`), `Park et al. (2021)` (`10.1038/s41598-021-97043-7`), `Canlı et al. (2024)` (`10.1371/journal.pone.0300044`), and `Öten & Aygün (2024)` (`10.1080/10255842.2024.2417200`) trained classical/ensemble ML on EDX and clinical features. `Malo-Urriés et al. (2026)` (`10.20944/preprints202603.0234.v1`) trained a 4-class NCS-validated ultrasound CNN; `Shi et al. (2026)` (`10.1016/j.ejrad.2026.113251`) and `Manoochehri et al. (2025)` (`10.1186/s12891-025-09079-9`) predicted post-release outcomes.

## Key Gaps Identified (`research-wiki/gap_map.md`)

- **G1 (Cross-device & operator domain shift in ultrasound DL):** Models degrade across ultrasound vendors, probe frequencies, and compression levels.
- **G2 (Anatomical & demographic variance in fixed CSA cutoffs):** Fixed CSA thresholds fail in bifid median nerves, extreme habitus, or early demyelinating CTS without nerve swelling.
- **G3 (Dynamic kinematic & elastographic biomarker integration):** Few models jointly capture nerve trajectory kinematics, continuous cross-sectional deformation, and intraneural texture.
- **G4 (End-to-end multimodal fusion / distillation between imaging and raw electrodiagnosis):** Ultrasound images and raw NCS waveforms are modeled in isolation rather than via cross-modal distillation or shared representations.
- **G5 (Prospective clinical decision support & calibrated deferral):** Lack of uncertainty-calibrated triage controllers that provably bound false-negative rates when deciding who can skip invasive NCS.

## Instructions

Generate 8-12 concrete research ideas. For each idea:
1. One-sentence summary
2. Core hypothesis (what you expect to find and why)
3. Minimum viable experiment (what's the cheapest way to test this?)
4. Expected contribution type: empirical finding / new method / theoretical result / diagnostic
5. Risk level: LOW (likely works) / MEDIUM (50-50) / HIGH (speculative)
6. Estimated effort: days / weeks / months

