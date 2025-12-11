This repository contains the complete codebase used in the study:
“A physics-aware hybrid framework for transferable prediction of membrane fouling dynamics.”
It integrates reduced-order mechanistic modeling, time-series ML, and curated multi-study datasets to predict flux decline in membrane systems operated with diverse oils, membranes, and operating conditions.

Membrane fouling remains the primary limitation in oil–water separation. Existing ML or empirical models can describe individual experiments but do not transfer across membranes, laboratories, or feed chemistries.

This repository provides a reproducible implementation of the first hybrid physics–ML pipeline capable of predicting fouling behavior across studies. It combines:

1. Reduced-Order Model (ROM)

A finite-element–inspired transport model approximating advection–diffusion–Darcy coupling and parameterizing fouling via a stretched-exponential (KWW) decay:

J(t)=J∞+(J0−J∞)exp⁡[−(t/τ)β]


Scripts include:

KWW fitting for each flux–time curve

Physics-aware normalization

Curve reconstruction and curve-level error quantification

2. Metadata → Parameter Mapping (Machine Learning)

A two-stage regression pipeline predicting KWW parameters (J₀, J∞, τ, β) from curve-level metadata using:

GroupKFold (grouped by article/lab)

HistGradientBoostingRegressor

Preprocessing pipelines for mixed numeric/categorical metadata

Model evaluation (MAE, RMSE, R², grouped cross-validation)

3. Curve → Metadata (MiniRocket + Shape Embeddings)

A stacked architecture combining:

MiniRocket multivariate time-series embeddings

Shape descriptors (AUC, segment slopes, curvature, final flux)

Logistic regression with grouped CV

Multi-target prediction (oil type, membrane material, droplet size, P_bar, porosity, pore size, etc.)

Time-window importance for interpretability

4. Cross-study reproducibility tools

Publication-level holdout validation

Minimal metadata standard generation

Automated feature importance characterization

Data cleaning, ID normalization, curve consolidation
