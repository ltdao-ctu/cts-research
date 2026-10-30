# Gap Map

- **G1 (Cross-device & operator domain shift in ultrasound DL):** Most ultrasound segmentation and diagnostic CNNs are trained on single-center, single-probe cohorts and degrade across ultrasound vendors, probe frequencies, and operator compression levels.
- **G2 (Anatomical & demographic variance in fixed CSA cutoffs):** Reliance on absolute median nerve cross-sectional area (CSA) thresholds (e.g., 9–12 mm²) fails in patients with bifid median nerves, extreme body habitus, or early demyelinating CTS without nerve swelling.
- **G3 (Dynamic kinematic & elastographic biomarker integration):** Few deep learning frameworks jointly model dynamic median nerve mobility/deformation (cine loops) together with tissue stiffness (shear wave elastography) and B-mode echotexture.
- **G4 (End-to-end multimodal fusion of imaging and raw electrodiagnosis):** Existing studies mostly treat ultrasound images and raw nerve conduction study (NCS) waveforms in isolation rather than learning unified cross-modal representations for severity staging and prognosis.
- **G5 (Prospective multicenter clinical validation & longitudinal outcome prediction):** Most ML/DL studies are retrospective diagnostic classifiers rather than prospective clinical decision-support tools predicting post-treatment (conservative vs. surgical release) recovery trajectories.
