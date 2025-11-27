---
title: Home
layout: home
nav_order: 2
has_children: false
---

# MZ_Visualization.jl

A powerful, high-performance Julia package for visualizing high-resolution Mass Spectrometry (MS) data. Built on CairoMakie, MZ_Visualization provides fast, flexible, and publication-quality plots for all your MS data analysis needs. Currently, for reading *XML* files the package is dependent on the package [*MS_Import.jl*](https://gitlab.com/EMCMS_UVA/MS_Import.jl), which only imports files in *mzXML* format. If you would like to use other file formats, just make sure that the imported file has the same format and keys. 

# Features

The *MZ_Visualization.jl* is meant to provide you with a suite of visulaization tools for raw data, pre-processed data (e.g. feature lists), and annotations. At the moment the modules related to pre-processed data and annotation are under development. 

# Installation 

For installation, please follow the below instructions: 

```julia 

using Pkg
Pkg.add(url="https://gitlab.com/EMCMS_UVA/MS_Import.jl")
Pkg.add(url="https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl")
println("MZ_Visualization.jl installed successfully.")

``` 

or 

```julia

] 

add "https://gitlab.com/EMCMS_UVA/MS_Import.jl"
add "https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl"

``` 

# Demonstration

We have created a simple Google Colab with some example plots and explanation that should help you to get started. For details explanation of each function, please take a look at this documentation. 

To use the colab, you can get the demo files using this Zenodo link: [https://zenodo.org/records/17544458](https://zenodo.org/records/17544458)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1kmM4H97BIs-Fe6SStt0JOufiA_EbCcfv?usp=sharing)