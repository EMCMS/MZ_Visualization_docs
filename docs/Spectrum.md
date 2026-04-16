---
layout: default
title: Spectra
nav_order: 4
parent: Raw Data Visualization
---

You can visualize the full scan spectra of MS1, MSn, either based on location (i.e. scan number or the retention time) or based on the precursor ion/window.

# MS1 level spectra 

## MS1 scan 

The function `get_scan_MS1` plots the **MS1 spectrum** for a specified scan number, displaying m/z against intensity. 

> **Warning**
> Note that the scan number is only associated with the MS1 level scans. If you are using any other XML parser than `MS_Import.jl`, make sure that the scans are separated and the files are folded properly.
{: .warning }

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS1" key). |
| `scan_n` | `Int` | Required | The scan number to extract the MS1 spectrum from. |
| `window` | `tuple{Float64, Float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. If provided, peak annotation is disabled. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate. Set to 0 to disable annotation. |
| `offset` | `Float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output

* `f`: Figure object containing the MS1 spectrum plot.

### Usage

```julia
scan_n = 630

# Default settings

get_scan_MS1(chrom_data, scan_n)

# With m/z window

window = (300, 400)

get_scan_MS1(chrom_data, scan_n; window = window)

# Disable peak annotation

n_p = 0 

get_scan_MS1(chrom_data, scan_n; n_p = n_p)

# Interactive mode

interactive = true

get_scan_MS1(chrom_data, scan_n; interactive = interactive)


```

![MS1 Spectrum](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/MS1_Spectrum_scan_630.png?ref_type=heads)

## MS1 retention time

The function `get_rt_MS1` plots the **MS1 spectrum** at the closest scan to a specified retention time (minutes). The retention time reported on the plot is the measured rt, so it may be slightly different from the selected value.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS1" key). |
| `rt_value` | `float64` | Required | The retention time (in minutes) to extract the MS1 spectrum from. |
| `window` | `tuple{Float64, Float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output 

* `f`: Figure object containing the MS1 spectrum plot at the specified retention time.

### Usage

```julia
rt_value = 5.0

# Default settings

get_rt_MS1(chrom_data, rt_value)

# With m/z window

window = (190, 198)

get_rt_MS1(chrom_data, rt_value; window = window)

# Annotate top 5 peaks, interactive

n_p = 5
interactive = true

get_rt_MS1(chrom_data, rt_value; n_p = n_p, interactive = interactive)


```

![MS1 Spectrum at RT](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/MS1_Spectrum_rt_5.0.png?ref_type=heads)

## Multiple MS1 scans 

The function `get_multi_scanMS1` generates **stacked MS1 spectrum panels** for multiple specified scan numbers.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS1" key). |
| `scans_n` | `vector{Int}` | Required | A list of scan numbers to extract the MS1 spectra from. |
| `window` | `tuple{Float64, Float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate per panel. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output

* `f`: Figure object containing the MS1 spectrum plots for all specified scans.

### Usage

```julia
scans_n = [500, 200, 300]

# Default settings

get_multi_scanMS1(chrom_data, scans_n)

# With m/z window and no annotation

window = (205, 210)
n_p = 0

get_multi_scanMS1(chrom_data, scans_n; window = window, n_p = n_p)


```

![Multi MS1 Spectra](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/Multi_MS1_Spectra.png?ref_type=heads)


## Multiple MS1 rts 

The function `get_multi_rtMS1` generates **stacked MS1 spectrum panels** at multiple specified retention times.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS1" key). |
| `rt_values` | `vector{Float64}` | Required | A list of retention times (in minutes) to extract the MS1 spectra from. |
| `window` | `tuple{Float64, Float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate per panel. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output 

* `f`: Figure object containing the MS1 spectrum plots for all specified retention times.

### Usage

```julia
rt_values = [5.0, 10.0]

# Default settings

get_multi_rtMS1(chrom_data, rt_values)

# With m/z window

window = (205, 210)

get_multi_rtMS1(chrom_data, rt_values; window = window)


```

![Multi MS1 Spectra by RT](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/Multi_MS1_Spectra_rt.png?ref_type=heads)


## One scan number with multiple MS1 files

The function `get_oneScan_multiMS1` generates **comparative MS1 spectra** from multiple datasets at a single scan number.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data_list` | `vector{Dict}` | Required | A list of chromatographic datasets. |
| `scan_n` | `Int` | Required | The scan number to extract the MS1 spectra from. |
| `labels` | `vector{string}` | Required | Labels corresponding to each dataset. |
| `window` | `tuple{float64, float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate per panel. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output

* `f`: Figure object containing stacked MS1 spectrum plots, one per dataset.

### Usage

```julia
chrom_data_list = [chrom_1PPB, chrom_100PPB]
labels = ["1 PPB", "100 PPB"]
scan_n = 300

# Default settings

get_oneScan_multiMS1(chrom_data_list, scan_n, labels)

# With m/z window

window = (150, 200)

get_oneScan_multiMS1(chrom_data_list, scan_n, labels; window = window)


```

![OneScan MultiMS1](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/OneScan_MultiMS1_Spectra.png?ref_type=heads)

## One rt with multiple MS1 files

The function `get_oneRt_multiMS1` generates **comparative MS1 spectra** from multiple datasets at a single retention time.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data_list` | `vector{Dict}` | Required | A list of chromatographic datasets. |
| `rt_value` | `float64` | Required | The retention time (in minutes) to extract the MS1 spectra from. |
| `labels` | `vector{string}` | Required | Labels corresponding to each dataset. |
| `window` | `tuple{float64, float64}` | nothing - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate per panel. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### output 

* `f`: Figure object containing stacked MS1 spectrum plots, one per dataset.

### Usage

```julia
chrom_data_list = [chrom_1PPB, chrom_100PPB]
labels = ["1 PPB", "100 PPB"]
rt_value = 4.95

# Default settings

get_oneRt_multiMS1(chrom_data_list, rt_value, labels)

# With m/z window

window = (195, 197)

get_oneRt_multiMS1(chrom_data_list, rt_value, labels; window = window)


```

![OneRt MultiMS1](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/OneRt_MultiMS1_Spectra.png?ref_type=heads)

# MS2 level spectra 

## DIA MS2 spectrum at a scan

> **Warning**
> When mentioned DIA (i.e. data independent acquisition), it is referring to having continuos alternating MS1 and MS2 scans. For SWATH and multi-collision experiments, there are specific functions to be used.
{: .warning }

The function `get_scan_MS2` plots the **MS2 spectrum** for a specified scan number.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS2" key). |
| `scan_n` | `Int` | Required | The scan number to extract the MS2 spectrum from. |
| `window` | `tuple{float64, float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output 

* `f`: Figure object containing the MS2 spectrum plot.

### Usage

```julia
scan_n = 500

# Default settings

get_scan_MS2(chrom_data, scan_n)

# With m/z window, interactive

window = (100, 500)
interactive = true

get_scan_MS2(chrom_data, scan_n; window = window, interactive = interactive)


```

![MS2 Spectrum](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/MS2_Spectrum_scan_500.png?ref_type=heads)


## DIA MS2 spectrum at a rt 

The function `get_rt_MS2` plots the **MS2 spectrum** at the closest scan to a specified retention time.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS2" key). |
| `rt_value` | `float64` | Required | The retention time (in minutes) to extract the MS2 spectrum from. |
| `window` | `tuple{float64, float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output

* `f`: Figure object containing the MS2 spectrum plot at the specified retention time.

### Usage

```julia
rt_value = 11.0

# Default settings

get_rt_MS2(chrom_data, rt_value)

# With m/z window

window = (100, 500)


get_rt_MS2(chrom_data, rt_value; window = window)


```

![MS2 Spectrum at RT](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/MS2_Spectrum_rt_11.0.png?ref_type=heads)

## DIA multiple MS2 spectra at scan numbers

The function `get_multi_scanMS2` generates **stacked MS2 spectrum panels** for multiple specified scan numbers.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS2" key). |
| `scans_n` | `vector{Int}` | Required | A list of scan numbers to extract the MS2 spectra from. |
| `window` | `tuple{float64, float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate per panel. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output

* `f`: Figure object containing the MS2 spectrum plots for all specified scans.

### Usage

```julia
scans_n = [150, 300, 500]

# Default settings

get_multi_scanMS2(chrom_data, scans_n)

# With m/z window

window = (100, 200)

get_multi_scanMS2(chrom_data, scans_n; window = )

```

![Multi MS2 Spectra](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/Multi_MS2_Spectra.png?ref_type=heads)

## DIA multiple MS2 spectra at rts

The function `get_multi_rtMS2` generates **stacked MS2 spectrum panels** at multiple specified retention times.

### Inputs

| Argument | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `chrom_data` | `Dict` | Required | A dictionary containing the full chromatographic data ("MS2" key). |
| `rt_values` | `vector{float64}` | Required | A list of retention times (in minutes) to extract the MS2 spectra from. |
| `window` | `tuple{float64, float64}` | `nothing` - Optional | m/z range (min_mz, max_mz) to zoom the plot. |
| `n_p` | `Int` | 3 - Optional | The number of top peaks to annotate per panel. Set to 0 to disable. |
| `offset` | `float64` | 0.1 - Optional | Spacing parameter for the sig_select peak labeling utility. |
| `interactive` | `Bool` | `false` - Optional | Enables an interactive GLMakie window. |

### Output 

* `f`: Figure object containing the MS2 spectrum plots for all specified retention times.

### Usage

```julia
rt_values = [4.8, 10.0, 15.0]

# Default settings

get_multi_rtMS2(chrom_data, rt_values)

# With m/z window

window = (100, 200)

get_multi_rtMS2(chrom_data, rt_values; window = window)


```

![Multi MS2 Spectra by RT](https://gitlab.com/EMCMS_UVA/MZ_Visualization.jl/-/raw/main/figures/Multi_MS2_Spectra_rt.png?ref_type=heads)

