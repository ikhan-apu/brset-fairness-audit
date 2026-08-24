# brset-fairness-audit

Code for the paper **"Beyond AUC: Operating-Point Fairness, Mitigation Fragility,
and Cross-Camera Generalisation in Retinal Disease Screening"**, BECITHCON 2026.

This repository contains the fairness audit, mitigation, cross-camera transfer,
and adaptation notebooks used in the paper. It does **not** contain the model
training pipeline itself, which is released with the companion paper (M. I. Khan
et al., FMLDS 2026), or the raw BRSET / mBRSET data, which are available on
PhysioNet under credentialed access.

## What is in this repository

- `notebooks/01_brset_fairness_audit.ipynb` — in-domain subgroup fairness audit on BRSET, including the threshold-robustness sweep (paper Fig. 1).
- `notebooks/02_brset_mitigation.ipynb` — post-hoc mitigation experiments (per-group temperature scaling and per-group operating points) and the AMD threshold-bootstrap diagnostic (paper Table II).
- `notebooks/03_crossdomain_fairness.ipynb` — zero-shot deployment of the BRSET model on mBRSET and cross-camera subgroup fairness (paper Table III).
- `notebooks/04_adaptation_vs_fairness.ipynb` — recalibration versus lightweight fine-tuning on mBRSET (paper Table IV, Fig. 4).
- `split.csv` — the patient-level BRSET train / validation / test split used in the paper.
- `fairness_outputs/` — CSV summaries and figures produced by the notebooks (regenerated on run).

## Requirements

- Python 3.10 or later
- PyTorch 2.x, torchvision, scikit-learn, pandas, numpy, matplotlib, scipy, Pillow
- Roughly 8 GB GPU memory for inference; the fine-tuning step in notebook 04 fits on a single mid-range GPU.

Install with:

```
pip install -r requirements.txt
```

## Data

The BRSET and mBRSET datasets are available on PhysioNet under credentialed access:

- BRSET: https://physionet.org/content/brazilian-ophthalmological/1.0.0/
- mBRSET: https://physionet.org/content/mbrset/1.0/

Obtain credentialed access, download both datasets, and set the appropriate paths
in the CONFIG cell at the top of each notebook.

## Trained model weights

The class-weighted EfficientNet-B0 checkpoint used throughout the paper is
attached to the tagged release (see the Releases page). The training procedure
is described in the FMLDS 2026 companion paper. To verify integrity, check the
SHA-256 hash printed on the Releases page against the downloaded file.

## Reproducing the paper

1. Obtain BRSET and mBRSET from PhysioNet.
2. Download the model checkpoint from the release page and place it at the path
   shown in each notebook's CONFIG cell.
3. Run `01_brset_fairness_audit.ipynb` end to end. It saves `brset_val_test_preds.csv`
   under `fairness_outputs/`, which the later notebooks consume.
4. Run `02`, `03`, and `04` in order. Each notebook is self-contained after the
   predictions from notebook 01 exist.

Every table and figure in the paper is regenerated from the CSVs written by
these notebooks.

## Citation

If you use this code, please cite:

```
M. I. Khan, A. S. M. N. Islam, S. Kanaya, and M. Altaf-Ul-Amin,
"Beyond AUC: Operating-Point Fairness, Mitigation Fragility, and Cross-Camera
Generalisation in Retinal Disease Screening,"
in Proc. IEEE Int. Conf. on Biomedical Engineering, Computing and Information
Technology for Health (BECITHCON), 2026.
```

## Licence

MIT (see `LICENSE`).
