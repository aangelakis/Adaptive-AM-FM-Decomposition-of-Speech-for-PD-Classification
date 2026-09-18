# Adaptive-AM-FM-Decomposition-of-Speech-for-PD-Classification
Source code for paper titled "Adaptive AM-FM Decomposition of Speech for Parkinson’s Disease Classification"

This repository implements a Machine Learning pipeline for the classification of **Parkinson's Disease (PD)**. It utilized high-resolution features derived from an Adaptive AM-FM (Amplitude Modulation - Frequency Modulation) decomposition of speech called **eaQHM**, to distinguish between Healthy Controls (HC) and PD patients.

**Abstract**:
Parkinson’s disease (PD) detection from sustained-vowel
speech is undermined by data leakage and inconsistent evalu-
ation. We introduce 18 novel, interpretable AM-FM features
from the extended adaptive Quasi-Harmonic Model (eaQHM),
a high-resolution decomposition new to PD detection, yield-
ing descriptors similar to jitter, shimmer, flux, centroid, and
Teager operator. These new features are evaluated under a re-
peated, speaker-independent, stratified nested cross-validation
with speaker-level metrics using conventional ML models.
On the clean PC-GITA corpus, a corrected resampled test
finds no significant difference between them and a richer 88-d
eGeMAPS baseline or a fine-tuned WavLM foundation model.
However, on the noisier NeuroVoz corpus, the picture changes,
as eGeMAPS and WavLM outperform AM-FM features. Com-
pact, interpretable features compete against far larger represen-
tations on clean phonation under strict, leakage-free evaluation,
with clear limits under acoustic degradation.

If you use this repository, pleace cite the accompanying paper (BibTeX to be added once available):

@article{TODO, title = {Adaptive AM-FM Decomposition of Speech for PD Classification}, author = {TODO}, journal = {TODO}, year = {TODO} }

