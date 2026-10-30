# Research Wiki Query Pack

_Auto-generated. Do not edit._

## Open Gaps
# Gap Map

- **G1 (Cross-device & operator domain shift in ultrasound DL):** Most ultrasound segmentation and diagnostic CNNs are trained on single-center, single-probe cohorts and degrade across ultrasound vendors, probe frequencies, and operator compression levels.
- **G2 (Anatomical & demographic variance in fixed CSA cutoffs):** Reliance on absolute median nerve cross-sectional area (CSA) thresholds (e.g., 9–12 mm²) fails in patients with bifid median nerves, extreme body habitus, or early demyelinating CTS without nerve swelling.
- **G3 (Dynamic kinematic & elastographic biomarker integration):** Few deep learning frameworks jointly model dynamic median nerve mobility/deformation (cine loops) together with tissue stiffness (shear wave elastography) and B-mode echotexture.
- **G4 (End-to-end multimodal fusion of imaging and raw electrodiagnosis):** Existing studies mostly treat ultrasound images and raw nerve conduction study (NCS) waveforms in isolation rather than learning unified cross-modal representations for severity staging and prognosis.
- **G5 (Prospective multicenter clinical validation & longitudinal outcome prediction):** Most ML/DL studies are retrospective diagnos
## Key Papers (33 total)
- [paper:bakalis2024_carpal_tunnel_syndrome] Carpal Tunnel Syndrome Automated Diagnosis: A Motor vs. Sensory Nerve Conduction-Based Approach: 2D CNNs on STFT spectrograms and wavelet decomposition of raw motor and sensory nerve conduction signals achieve 94-97.1% automated CTS grading accura
- [paper:bello2026_privacypreserving_collaborative_medical] Privacy-Preserving Collaborative Medical Image Segmentation Using Latent Transform Networks: Privacy-preserving collaborative medical image segmentation via Latent Transform Networks evaluated across multi-institutional ultrasound nerve segmen
- [paper:canli2024_carpal_tunnel_syndrome] Carpal Tunnel Syndrome Prediction with Machine Learning Algorithms Using Anthropometric and Strength-Based Measurement: Random Forest and XGBoost models predict CTS non-invasively from hand anthropometric dimensions and grip/pinch strength.
- [paper:chen2020_attentionguided_discriminative_region] Attention-Guided Discriminative Region Localization and Label Distribution Learning for Bone Age Assessment: Attention-guided discriminative region localization and label distribution learning for automated hand and wrist radiograph assessment.
- [paper:cosmo2021_learningbased_median_nerve] Learning-Based Median Nerve Segmentation From Ultrasound Images For Carpal Tunnel Syndrome Evaluation: Mask R-CNN instance segmentation of the median nerve in transverse wrist ultrasound scans supports objective CTS evaluation.
- [paper:cosmo2022_deep_learning_approach] A deep learning approach to median nerve evaluation in ultrasound images of carpal tunnel inlet: Deep semantic segmentation network delineates median nerve boundaries at the carpal tunnel inlet for automated CSA quantification.
- [paper:darol2023_artificial_intelligence_based] Artificial Intelligen
## Recent Relationships (53 total)
  idea:idea_004 --addresses_gap--> gap:G3
  idea:idea_007 --inspired_by--> paper:smerilli2022_development_convolutional_neural
  idea:idea_007 --inspired_by--> paper:cosmo2022_deep_learning_approach
  idea:idea_007 --addresses_gap--> gap:G1
  idea:idea_002 --inspired_by--> paper:sim2025_diagnosis_carpal_tunnel
  idea:idea_002 --inspired_by--> paper:peng2024_onestop_automated_diagnostic
  idea:idea_002 --addresses_gap--> gap:G2
  idea:idea_008 --inspired_by--> paper:peng2024_onestop_automated_diagnostic
  idea:idea_008 --addresses_gap--> gap:G2
  idea:idea_008 --addresses_gap--> gap:G3
  idea:idea_010 --inspired_by--> paper:shi2026_explainable_ultrasoundbased_multimodal
  idea:idea_010 --inspired_by--> paper:manoochehri2025_machine_learning_applications
  idea:idea_010 --addresses_gap--> gap:G5
  darol2023_artificial_intelligence_based --addresses_gap--> G2
  yener2024_application_machine
