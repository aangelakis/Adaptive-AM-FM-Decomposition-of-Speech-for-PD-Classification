# Adaptive-AM-FM-Decomposition-of-Speech-for-PD-Classification
Source code for paper titled "Adaptive AM-FM Decomposition of Speech for Parkinson’s Disease Classification"

This repository implements a Machine Learning pipeline for the classification of **Parkinson's Disease (PD)**. It utilized high-resolution features derived from an Adaptive AM-FM (Amplitude Modulation - Frequency Modulation) decomposition of speech called **eaQHM**, to distinguish between Healthy Controls (HC) and PD patients.

**Abstract**:
We propose a set of novel AM-FM features for detecting Parkinson's disease (PD) from speech signals. This set is obtained from the extended adaptive Quasi-Harmonic Model (eaQHM), which is able to locally adapt its parameters in order to decompose speech into high-resolution, time varying, sinusoidal signals. We apply this method on two PD speech datasets, the PC-GITA and the NeuroVoz. For each speech signal, the analyzed AM and FM components are summarized over time yielding a fixed-length feature vector successively fed into machine learning models. We employ a repeated, 10-by-5, stratified, speaker-independent nested cross-validation to display the robustness of our method and to ensure leakage-free classification. We also report a standard suite of classification metrics on a speaker basis evaluation. Finally, cross-dataset evaluations are presented providing valuable insights into the challenges of cross-corpus PD detection.

If you use this repository, pleace cite the accompanying paper (BibTeX to be added once available):

@article{TODO, title = {Adaptive AM-FM Decomposition of Speech for PD Classification}, author = {TODO}, journal = {TODO}, year = {TODO} }

