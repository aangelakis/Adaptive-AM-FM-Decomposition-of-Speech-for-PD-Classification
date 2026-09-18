# Adaptive-AM-FM-Decomposition-of-Speech-for-PD-Classification

Source code for the paper *"Adaptive AM-FM Decomposition of Speech for Parkinson's Disease Classification"*.

This repository implements a machine-learning pipeline for the classification of **Parkinson's disease (PD)** from sustained vowels. It uses high-resolution features derived from an adaptive AM-FM (amplitude modulation – frequency modulation) decomposition of speech, the **extended adaptive Quasi-Harmonic Model (eaQHM)**, to distinguish PD patients from healthy controls (HC).

## Abstract

Parkinson's disease (PD) detection from sustained-vowel speech is undermined by data leakage and inconsistent evaluation. We introduce 18 novel, interpretable AM-FM features from the extended adaptive Quasi-Harmonic Model (eaQHM), a high-resolution decomposition new to PD detection, yielding descriptors similar to jitter, shimmer, flux, centroid, and Teager operator. These new features are evaluated under a repeated, speaker-independent, stratified nested cross-validation with speaker-level metrics using conventional ML models. On the clean PC-GITA corpus, a corrected resampled test finds no significant difference between them and a richer 88-d eGeMAPS baseline or a fine-tuned WavLM foundation model. However, on the noisier NeuroVoz corpus, the picture changes, as eGeMAPS and WavLM outperform AM-FM features. Compact, interpretable features compete against far larger representations on clean phonation under strict, leakage-free evaluation, with clear limits under acoustic degradation.

## Repository structure

```
.
├── features/            # Pre-extracted feature files (eaQHM .mat, eGeMAPS .csv)
├── folds/               # Predefined cross-validation folds shared by all models
├── gender_metadata/     # Speaker gender, used for stratification
├── SVM/                 # RBF-kernel SVM notebooks
├── XGBoost/             # XGBoost notebooks
├── WavLM/               # WavLM foundation-model baseline notebooks
└── README.md
```

### `features/`

| File | Content |
|---|---|
| `pc_gita_vowels_16k_5ms_chopped_650.mat` | eaQHM AM-FM features, PC-GITA vowels |
| `neurovoz_16k_5ms_chopped_650.mat` | eaQHM AM-FM features, NeuroVoz vowels |
| `pc_gita_vowels_egemapsv02_16k_5ms.csv` | eGeMAPSv02 functionals (openSMILE), PC-GITA vowels |
| `neurovoz_vowels_egemapsv02_16k_5ms.csv` | eGeMAPSv02 functionals (openSMILE), NeuroVoz vowels |

The eaQHM features were extracted in MATLAB, and the eGeMAPS features with openSMILE, before running the notebooks. The notebooks start from these files.

### `folds/`

| File | Content |
|---|---|
| `master_cv_folds_vowels.csv` | PC-GITA folds |
| `master_cv_folds_neurovoz_vowels.csv` | NeuroVoz folds |

Each file assigns every speaker to one outer fold per repeat (`Repeat_1_Fold` … `Repeat_5_Fold`). The folds are speaker-independent and stratified by label and gender. **Every model on a given corpus uses the same fold file**, so all feature sets and classifiers are compared on identical splits.

### `gender_metadata/`

| File | Content |
|---|---|
| `genders.csv` | Speaker gender, PC-GITA |
| `metadata_hc.csv`, `metadata_pd.csv` | Speaker metadata (including sex), NeuroVoz |

### Notebooks

| Folder | Notebook | Features | Corpus |
|---|---|---|---|
| `SVM/` | `SVM_PC-GITA.ipynb` | eaQHM | PC-GITA |
| `SVM/` | `SVM_NeuroVoz.ipynb` | eaQHM | NeuroVoz |
| `SVM/` | `SVM_eGeMAPS_PC-GITA.ipynb` | eGeMAPS | PC-GITA |
| `SVM/` | `SVM_eGeMAPS_NeuroVoz.ipynb` | eGeMAPS | NeuroVoz |
| `XGBoost/` | `XGBoost_PC-GITA.ipynb` | eaQHM | PC-GITA |
| `XGBoost/` | `XGBoost_NeuroVoz.ipynb` | eaQHM | NeuroVoz |
| `XGBoost/` | `XGBoost_eGeMAPS_PC-GITA.ipynb` | eGeMAPS | PC-GITA |
| `XGBoost/` | `XGBoost_eGeMAPS_NeuroVoz.ipynb` | eGeMAPS | NeuroVoz |
| `WavLM/` | `SSL4PR_PC-GITA.ipynb` | Raw audio (WavLM-Base) | PC-GITA |
| `WavLM/` | `SSL4PR_NeuroVoz.ipynb` | Raw audio (WavLM-Base) | NeuroVoz |

## Features

The 18 eaQHM-based features are:

- **AM features:** Amplitude Variation of harmonics $H_1$–$H_5$ and the Normalised first difference of $A_1$ (`ampl_var_H1` … `ampl_var_H5`, `A1_norm_diff`)
- **FM features:** Frequency Variation of harmonics $H_1$–$H_5$ and the Normalised first difference of $f_0$ (`freq_var_H1` … `freq_var_H5`, `f0_norm_diff`)
- **Spectral and Teager-energy features:** Five-harmonic Spectral Centroid (mean, std), Quasi-Harmonic-Amplitude Flux (mean, max) and Teager-inspired Parametric Energy (mean, std)

## Evaluation protocol

All models use the same protocol:

- **Repeated nested cross-validation:** 5 repeats × 10 outer folds, with a 5-fold inner loop for hyper-parameter tuning, scored by ROC AUC.
- **Speaker independence:** no speaker appears in both the training and the test data, in either the outer or the inner loop. Each notebook asserts this for every fold.
- **Stratification** by label and gender.
- **Metrics** at the sample (recording) level and at the speaker level, where a speaker's PD probability is the mean over their recordings.

Hyper-parameters are tuned by grid search for the SVM ($C$, $\gamma$) and XGBoost (number of trees, learning rate, maximum depth, row and column subsampling), and with Optuna for WavLM (learning rate, weight decay, dropout, pooling).

The WavLM baseline follows the SSL4PR approach of La Quatra et al. (Interspeech 2024): [K-STMLab/SSL4PR](https://github.com/K-STMLab/SSL4PR).

## Data availability

The audio recordings of **PC-GITA** and **NeuroVoz** are not distributed with this repository and must be obtained from their respective authors under their terms of use.

## Requirements

- Python 3 with `numpy`, `pandas`, `scipy`, `scikit-learn`, `matplotlib`, `seaborn`
- `xgboost` for the XGBoost notebooks
- `torch`, `torchaudio`, `transformers`, `optuna` and `tqdm` for the WavLM notebooks (a CUDA GPU is strongly recommended)

## Citation

If you use this repository, please cite the accompanying paper (BibTeX to be added once available):

```bibtex
@article{TODO,
  title   = {Adaptive AM-FM Decomposition of Speech for Parkinson's Disease Classification},
  author  = {TODO},
  journal = {TODO},
  year    = {TODO}
}
```
