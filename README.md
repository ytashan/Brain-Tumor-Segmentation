# 🧠 BraTS 2020 — Brain Tumor Segmentation, Risk Analysis & 3D Visualization

Complete A→Z pipeline for the [BraTS 2020](https://www.med.upenn.edu/cbica/brats2020/) multi-modal MRI brain tumor segmentation challenge.

## What’s included

| Stage | Content |
|-------|---------|
| 1 | Setup, configuration, robust dataset discovery |
| 2 | Exploratory data analysis (shapes, spacing, volumes, class imbalance) |
| 3 | Preprocessing + on-disk caching |
| 4 | Train/val/test split, 3D patch dataset, foreground-aware sampling & augmentation |
| 5 | **3D Residual Attention U-Net** with deep supervision |
| 6 | Combined Dice + Focal loss, region metrics, sliding-window inference + TTA |
| 7 | Full training loop (AMP, warmup, early stopping, checkpointing) |
| 8 | Held-out test-set evaluation (Dice, HD95, volume agreement) |
| 9 | Tumor size quantification + **research risk score** (heuristic, not a diagnosis) |
| 10 | Static + interactive 3D reconstruction of brain + tumor overlaid on source MRI |
| 11 | One-call inference: patient path → size, risk category, 3D report |
| 12 | Batch prediction on the unlabeled BraTS validation set (submission-ready NIfTIs) |

## Key features

- 4-modality input (FLAIR, T1, T1ce, T2) in RAS orientation
- Residual Attention 3D U-Net (~5 M parameters at base filters = 16)
- Deep supervision + region-wise Dice/Focal loss
- Sliding-window inference with configurable overlap + flip TTA
- Tumor volume (WT / TC / ET / ED / NCR), max diameter, size class
- Interpretable risk score (volume, enhancing fraction, necrotic fraction, edema, burden, multifocality)
- Interactive Plotly 3D brain + tumor visualization side-by-side with multi-planar MRI
- Ready for Kaggle or local runs (paths configurable via environment variables)

## Outputs

- Per-patient segmentation NIfTIs (labels 1 / 2 / 4)
- CSV risk ranking + size metrics
- Training curves, metric boxplots, confusion matrices
- Interactive HTML + static PNG 3D reports
- Best checkpoint (`best.pt`)

> ⚠️ The risk score is a **research heuristic** derived from the segmentation.  
> It is **not** a medical diagnosis and must not be used for clinical decision-making.
