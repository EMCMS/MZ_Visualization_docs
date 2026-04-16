---
layout: default
title: Raw Data Visualization
nav_order: 2
has_children: true
---

# Introduction

This section of the documentation covers the **raw data visualization** functions available in `MZ_Visualization.jl`, focusing on two complementary views of mass spectrometry data: chromatograms and spectra.

[**Chromatogram visualization**](https://emcms.github.io/MZ_Visualization_docs/docs/Chrom.html) covers functions for plotting the full chromatographic data across the time dimension. This includes 3D heatmap plots of m/z versus retention time, Total Ion Chromatograms (TIC), and Extracted Ion Chromatograms (XIC) at both MS1 and MS2 levels. The MS2 XIC functions additionally support different acquisition modes, including standard DIA, SWATH, and multi-collision experiments. Most functions support both single-dataset and multi-dataset comparisons, with options for overlaid or stacked layouts.

[**Spectrum visualization**](https://emcms.github.io/MZ_Visualization_docs/docs/Spectrum.html) covers functions for plotting mass spectra at a fixed point in time, either by scan number or retention time. Both MS1 and MS2 (DIA) levels are covered, with functions available for single spectra, multiple stacked spectra, and comparative views across multiple datasets. All spectrum functions support m/z windowing and configurable peak annotation.

Together, they provide a comprehensive toolkit for exploring raw LC-MS data, whether you are inspecting the chromatographic profile of a sample or drilling down into the spectral detail at a specific point in a run.