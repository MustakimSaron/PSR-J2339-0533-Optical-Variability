# High-Cadence TESS Optical Photometry of PSR J2339-0533

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

This repository contains the data reduction pipeline, statistical testing code, publication figures, and LaTeX manuscript for the paper:

> **"High-Cadence TESS Optical Photometry of the Redback Pulsar PSR J2339–0533: Constraints on Shock-Driven Micro-Variability"**  
> *Md Mustakim Bin Alam* (Novosibirsk State University)

---

## Abstract

Utilizing continuous space-based photometry from the Transiting Exoplanet Survey Satellite (TESS), we present a high-cadence optical variability and micro-flaring analysis of the redback millisecond pulsar binary **PSR J2339–0533**. Processing 29,511 photometric cadences, Lomb-Scargle periodogram analysis yields an orbital period of $P_{\mathrm{orb}} = 0.193099\text{ d}$ ($278.06\text{ min}$), driven by strong day-side thermal companion heating. 

We explicitly evaluate the single-cadence noise floor, finding that the optical scatter ($\sigma_{\mathrm{res}} = 0.6566$) is entirely dominated by the TESS instrumental Poisson noise floor ($\sigma_{\mathrm{phot}} = 0.7191$; $S/N \approx 1.49$). Detrending the heating curve using a 3rd-order Savitzky-Golay filter yields isolated residuals. A Kolmogorov-Smirnov test on candidate $>3\sigma$ micro-flaring events yields $D = 0.0700$ and $p = 0.738$, confirming that residual variability is uniformly distributed across orbital phase with no physical phase-locking to the intrabinary shock (IBS) geometry. Sensitivity testing across $2\%$, $4\%$, and $8\%$ filter window widths confirms that the $p$-value ($p \in [0.641, 0.812]$) and Power Spectral Density slope ($\alpha \approx 0.000$) are invariant to detrending choices. Masking night-side minimum light artifacts isolates a true off-minimum fractional RMS scatter of $\sigma_{\mathrm{frac}} = 56.81\%$, placing a strict single-cadence upper limit on non-thermal optical shock variability of $<34.48\%$ relative to peak companion flux.

---

## Key Astrophysical Summary

| Parameter / Metric | Measured Value / Result |
| :--- | :--- |
| **Target Name** | **PSR J2339–0533** (TIC 30870711) |
| **Cadences Processed ($N$)** | $29,511$ cadences |
| **Orbital Period ($P_{\mathrm{orb}}$)** | $0.193099\text{ d}$ ($278.06\text{ min} / 4.63\text{ h}$) |
| **Instrumental Noise Floor ($\sigma_{\mathrm{phot}}$)** | $0.7191$ ($71.91\%$) |
| **Normalized Residual Noise ($\sigma_{\mathrm{res}}$)** | $0.6566$ ($65.66\%$) |
| **Noise-Floor Ratio ($\sigma_{\mathrm{res}}/\sigma_{\mathrm{phot}}$)** | $0.91\times$ (**Instrumental Noise Dominated**) |
| **K-S Test Phase Distribution** | $p = 0.738$ (**Uniform / No Shock Phase-Locking**) |
| **PSD Turbulence Index ($\alpha$)** | $\alpha = -0.001$ ($P(f) \propto f^0$, White Noise) |
| **Masked Off-Minimum RMS ($\sigma_{\mathrm{frac}}$)** | $56.81\%$ |
| **Optical Non-Thermal Shock Bound** | **$< 34.48\%$ of Peak Companion Flux** |

---

## Repository Structure

* `psr_j2339_pipeline_v2.py`: Fully reproducible Python script for TESS data retrieval, normalization, Savitzky-Golay detrending, S-G sensitivity analysis, K-S test, PSD modeling, and figure generation.
* `main.tex`: Complete LaTeX manuscript source code formatted for the *Journal of High Energy Astrophysics* (`elsarticle` preprint template).
* `Figure1_J2339_LightCurve_Residuals.png`: 300 DPI publication Figure 1 (Light Curve, Residuals, and K-S Histogram).
* `Figure2_J2339_FractionalVariability.png`: 300 DPI publication Figure 2 (Masked Fractional Residuals and Phase-Binned RMS Scatter).

---

## Quickstart & Reproducibility

### 1. Clone the Repository
```bash
git clone [https://github.com/your-username/PSR-J2339-0533-Optical-Variability.git](https://github.com/your-username/PSR-J2339-0533-Optical-Variability.git)
cd PSR-J2339-0533-Optical-Variability
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the Analysis Pipeline
```bash
python psr_j2339_pipeline_v2.py
```

---


  note      = {In review}
}
```
