# High-Cadence TESS Optical Photometry of the Redback Pulsar PSR J2339−0533: Constraints on Shock-Driven Micro-Variability (v6.0)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Aeh1HtnIXkXn_vgjKsEwlxpbzstp0jN6)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://www.python.org/downloads/)
[![TESS SPOC](https://img.shields.io/badge/NASA%20MAST-TESS%20SPOC%20120s-brightgreen)](https://mast.stsci.edu/)

**Author:** Md Mustakim Bin Alam  
**Affiliation:** Department of Physics, Novosibirsk State University, Novosibirsk, 630090, Russia  
**Contact:** [m.alam1@g.nsu.ru](mailto:m.alam1@g.nsu.ru)  
**Journal:** *Physics of the Dark Universe* 
**Click on the "Open in Colab" will directly open the pipeline in Google Colab.**

---

## Overview

This repository contains the official end-to-end Python analysis pipeline (`v6.0`), Target Pixel File (TPF) difference-imaging routines, heteroscedastic Monte Carlo simulations, full-pipeline pre-detrending flare injection–recovery modules, correlated red-noise diagnostics, and publication figures for the study:

> **High-Cadence TESS Optical Photometry of the Redback Pulsar PSR J2339−0533: Constraints on Shock-Driven Micro-Variability**

Using 120-s cadence space-based photometry from the Transiting Exoplanet Survey Satellite (TESS) Science Processing Operations Center (SPOC) pipeline across **Sector 70** (2023 September 20 – October 16) and **Sector 92** (2025 May 7 – June 3), we analyze $N = 29,511$ strictly unflagged ($\texttt{QUALITY} = 0$) photometric cadences ($T_{\mathrm{exp}} = 40.99\ \mathrm{d}$ net exposure) of the redback millisecond pulsar binary **PSR J2339−0533** (**TIC 2052434280**; $\mathrm{RA} = 23^{\mathrm{h}}39^{\mathrm{m}}38.74^{\mathrm{s}}$, $\mathrm{Dec} = -05^\circ 33^\prime 05.3^{\prime\prime}$; $T_{\mathrm{mag}} = 18.61$, mean Gaia $G \approx 18.97$).

---

## Key Scientific & Methodological Highlights (v6.0)

1. **Target Verification, Crowding Audit & Pixel-Level Difference Imaging:**
   - Queries the NASA MAST archive for **PSR J2339−0533 (TIC 2052434280)** using official SPOC 120-s `PDCSAP_FLUX` and `SAP_FLUX` light curves and Target Pixel Files (no QLP product exists at $T_{\mathrm{mag}} = 18.61$).
   - Audits aperture crowding ($\texttt{CROWDSAP} = 0.3032$ in Sector 70 and $0.1286$ in Sector 92; $\texttt{FLFRCSAP} = 0.4759$ and $0.6593$) and sky/scattered-light background ($\mathrm{med}[\texttt{SAP_BKG}] = 306.9$ and $1792.6\ \mathrm{e^- s^{-1}}$ vs. de-blended target medians of $9.38$ and $9.84\ \mathrm{e^- s^{-1}}$).
   - Constructs orbital maximum ($\phi_{\mathrm{orb}} \in [0.60, 0.90]$) minus minimum ($\phi_{\mathrm{orb}} \in [0.10, 0.40]$) pixel-level difference images, localizing the orbital modulation to within $\Delta = 3.82^{\prime\prime} \pm 2.63^{\prime\prime}$ (Sector 70, aperture $\mathrm{S/N} = 101.0$) and $\Delta = 1.39^{\prime\prime} \pm 2.15^{\prime\prime}$ (Sector 92, aperture $\mathrm{S/N} = 64.1$) of the Gaia DR3 pulsar position.
   - Cross-calibrates TPF difference fluxes ($\Delta F_{\mathrm{diff,ap}} = 5.88 \pm 0.06$ and $7.47 \pm 0.12\ \mathrm{e^- s^{-1}}$; PSF-corrected $12.35$ and $11.33\ \mathrm{e^- s^{-1}}$) against 1D `SAP` ($5.85$ and $7.23\ \mathrm{e^- s^{-1}}$) and `PDCSAP` ($12.22$ and $11.02\ \mathrm{e^- s^{-1}}$) amplitudes within $1\%\text{--}3.3\%$, demonstrating consistent additive-invariant peak-to-peak modulation ($\Delta F_{\mathrm{pp,PDC}} = 15.59$ and $13.91\ \mathrm{e^- s^{-1}}$).

2. **Orbital Ephemeris Alignment & Periodically Wrapped Detrending:**
   - Recovers $P_{\mathrm{orb}} = 0.19309835 \pm 0.00000017\ \mathrm{d}$ ($278.0616 \pm 0.0002\ \mathrm{min}$) via 200-trial bootstrap Lomb–Scargle analysis ($\Delta P = +0.0385 \pm 0.0147\ \mathrm{s}$ relative to the Pletsch & Clark 2015 reference ephemeris $P_{\mathrm{orb,ephem}} = 0.19309790(1)\ \mathrm{d}$).
   - References all orbital phases to the ascending node epoch $T_{\mathrm{asc}} = \mathrm{MJD}\ 55791.9182100(4)$ ($\mathrm{BTJD}_0 = -1207.5817900$), placing inferior conjunction (night-side minimum) at $\phi_{\mathrm{orb}} = 0.25$ and superior conjunction (day-side maximum) at $\phi_{\mathrm{orb}} = 0.75$.
   - Eliminates phase-boundary discontinuities at $\phi_{\mathrm{orb}} = 0/1$ using 25% ($\approx 7,377$-cadence) periodic boundary padding prior to applying a 3rd-order Savitzky–Golay filter (4% phase window, $1,181$ cadences), cross-validated against a 4-harmonic Fourier series.

3. **Separated Standardized Pulls vs. Global Heteroscedastic Monte Carlo Tails:**
   - **Per-Cadence Standardized Pulls ($z_i = \Delta F_i / \sigma_{i,\mathrm{rescaled}}$):** Yields $+3\sigma = 41$ ($+4\sigma = 0$) and $-3\sigma = 46$ ($-4\sigma = 1$), matching unit-Gaussian $\mathcal{N}(0,1)$ expectations ($39.8$ expected per tail).
   - **Global Unscaled Residual Outliers ($\Delta F_i \gtrless \pm 3\sigma_{\mathrm{res}}$):** Yields $88$ positive ($6$ above $+4\sigma_{\mathrm{res}}$) and $107$ negative ($13$ below $-4\sigma_{\mathrm{res}}$) outliers. Across 3,000 heteroscedastic white-noise Monte Carlo realizations ($90$ expected; $5\text{--}95\%$ range: $76\text{--}106$), the positive tail ($88, p = 0.640$) matches background noise, while the negative tail ($107, p = 0.035$) reflects orbit-edge scattered-light dips ($67$ positive and $59$ negative when orbit edges are trimmed).

4. **Rotation-Invariant Circular Phase Tests & Statistical Power:**
   - Evaluates Kuiper's test ($V = 0.1033, p = 0.836$), Rayleigh's test ($Z_1^2 = 0.384, p = 0.825$), the two-harmonic $Z_2^2$ test ($Z_2^2 = 2.607, p = 0.626$), and an exact binomial test within the restricted X-ray IBS beaming window $\phi_{\mathrm{orb}} \in [0.55, 0.95]$ ($38/88$ events, $p = 0.587$).
   - Quantifies both conditional detection power ($\ge 19\text{--}21$ detected events required for $80\%\text{--}90\%$ Kuiper power) and end-to-end full-pipeline power for 200 injected 2-min flares ($A_{\mathrm{peak}} = 1.0\,F_{\mathrm{peak}}$), which yields Kuiper $p < 0.05$ in only $5.3\%$ of trials.

5. **Full-Pipeline Pre-Detrending Flare Injection–Recovery & Rate Upper Limits:**
   - Injects exposure-integrated piecewise FRED flares directly into the un-detrended light curve across $\tau \in [2, 5, 15, 30, 60, 80, 100]\ \mathrm{min}$ and $A_{\mathrm{peak}}/F_{\mathrm{peak}} \in [0.20, 3.50]$, verifying $T_{\mathrm{SG}} = 99.65\%\text{--}99.40\%$ filter transmission.
   - Establishes 90% completeness thresholds of $A_{90,\mathrm{single}} = 1.86\text{--}0.80\,F_{\mathrm{peak}}$ ($34.2\text{--}14.7\ \mathrm{e^- s^{-1}}$) and $A_{90,\mathrm{MF}} = 2.02\text{--}0.48\,F_{\mathrm{peak}}$ ($37.2\text{--}8.8\ \mathrm{e^- s^{-1}}$) for $\tau = 5\text{--}100\ \mathrm{min}$ ($2.89\text{--}3.40\,F_{\mathrm{peak}}$ at $\tau = 2\ \mathrm{min}$), constraining flare rates above $A_{90}$ to $R_{90}(k=0) < 0.0624\ \mathrm{flares\ day^{-1}}$ ($R_{90}[k=1] < 0.1054\ \mathrm{day^{-1}}$) across $\epsilon_{90} T_{\mathrm{exp}} = 36.89\ \mathrm{d}$.

6. **Correlated Red Noise, Same-CCD Control Star & Candidate Event Inspection:**
   - Characterizes low-frequency red noise via log-binned Lomb–Scargle periodograms ($\alpha_{\mathrm{LF}} = 0.38 \pm 0.04$ untrimmed; $\alpha_{\mathrm{LF,trim}} = 0.23 \pm 0.05$ orbit-trimmed) and time-averaged binned RMS ($z_{\mathrm{perm}} = +4.2\sigma\text{ to }+7.0\sigma$ pooled excess on $20\text{--}120\ \mathrm{min}$ timescales, $\sigma_{\mathrm{excess}} \approx 3.5\%\text{--}4.1\%\,F_{\mathrm{peak}}$), compared against a same-CCD control star aperture.
   - Inspects the Sector 70 rising-branch candidate excursion at $\mathrm{BTJD}\ 3209.98\text{--}3210.05$ ($1.68\ \mathrm{h}$, $\phi_{\mathrm{orb}} = 0.26\text{--}0.63$) in 1D `SAP` photometry ($\Delta F_{\mathrm{SAP}} = +2.97 \pm 0.435\ \mathrm{e^- s^{-1}}$, $\mathrm{S/N}_{\mathrm{local}} = 6.83\sigma$, $Z_{\mathrm{global}} = 5.97\sigma$ across $286$ windows in Sector 70) and phase-matched TPF difference imaging ($\Delta F_{\mathrm{TPF,ap}} = +3.02\ \mathrm{e^- s^{-1}}$, photon $\mathrm{S/N} = 8.7$, centroid offset $2.77^{\prime\prime} \pm 2.95^{\prime\prime}$).

---

## Summary of Key Observational & Statistical Results

| Metric / Parameter | Sector 70 (2023) | Sector 92 (2025) | Combined / Global Result |
| :--- | :---: | :---: | :---: |
| **TESS Camera / CCD** | 1 / 1 | 4 / 3 | — |
| **BTJD Time Span** | 3208.57 – 3232.96 | 3803.44 – 3828.07 | 40.99 d Net Exposure |
| **Raw / Flagged / Valid ($\texttt{QUALITY}=0$)** | 17,888 / 3,587 / 14,301 | 18,756 / 3,546 / 15,210 | 36,644 / 7,133 / 29,511 |
| **Crowding Metric (`CROWDSAP`)** | 0.3032 (69.7% contam.) | 0.1286 (87.1% contam.) | — |
| **PSF Flux Fraction (`FLFRCSAP`)** | 0.4759 | 0.6593 | — |
| **Median `PDCSAP_FLUX` ($\mathrm{e^- s^{-1}}$)** | 9.38 ($T_{\mathrm{mag,inf}}=18.01$) | 9.84 ($T_{\mathrm{mag,inf}}=17.96$) | 9.61 (Cat. $T=18.61 \rightarrow 5.40$) |
| **Median `SAP_BKG` ($\mathrm{e^- s^{-1}}$)** | 306.9 | 1792.6 | — |
| **Median Fractional Error ($\sigma_{\mathrm{phot}}$)** | 0.5291 (52.91%) | 0.8370 (83.70%) | 0.7191 ($\mathrm{med}[F_i/\sigma_i]=1.49$) |
| **Detrended Residual Scatter ($\sigma_{\mathrm{res}}$)** | 0.5087 ($\sigma_{\mathrm{res}}/\sigma_{\mathrm{phot}}=0.961$) | 0.7681 ($\sigma_{\mathrm{res}}/\sigma_{\mathrm{phot}}=0.918$) | 0.6562 ($\sigma_{\mathrm{res}}/\sigma_{\mathrm{phot}}=0.913$) |
| **`PDCSAP` Peak-to-Peak ($\Delta F_{\mathrm{pp,PDC}}$)** | $15.59\ \mathrm{e^- s^{-1}}$ | $13.91\ \mathrm{e^- s^{-1}}$ | $14.72\ \mathrm{e^- s^{-1}}$ ($F_{\mathrm{peak}}=18.44$) |
| **TPF Diff. Image Centroid Offset** | $3.82^{\prime\prime} \pm 2.63^{\prime\prime}$ ($\mathrm{S/N}=101.0$) | $1.39^{\prime\prime} \pm 2.15^{\prime\prime}$ ($\mathrm{S/N}=64.1$) | $< 4^{\prime\prime}$ ($< 1.5\sigma_{\mathrm{tot}}$) |
| **Standardized Pulls ($z_i \gtrless \pm 3\sigma$)** | — | — | $+3\sigma = 41,\ -3\sigma = 46$ (Exp: 39.8) |
| **Global Outliers ($\Delta F_i \gtrless \pm 3\sigma_{\mathrm{res}}$)** | — | — | $+3\sigma_{\mathrm{res}} = 88\ (p=0.640),\ -3\sigma_{\mathrm{res}} = 107\ (p=0.035)$ |
| **Circular Phase Uniformity ($T_{\mathrm{asc}}$)** | — | — | Kuiper $p = 0.836$, Rayleigh $p = 0.825$ |
| **90% Flare Rate Limit ($A \ge A_{90}$)** | — | — | $< 0.0624\ \mathrm{day^{-1}}$ ($k=0$ across $36.89\ \mathrm{d}$) |

---

## Repository Structure

```text
PSR-J2339-0533-Optical-Variability/
├── PSR-J2339-0533-Optical-Variability.ipynb   # Interactive Jupyter / Google Colab Notebook (v6.0)
├── psr_j2339_0533_optical_variability.py      # Standalone Python execution script (v6.0)
├── requirements.txt                           # Required Python dependencies
├── README.md                                  # Repository documentation
└── figures/                                   # 300 DPI publication figures generated by pipeline
    ├── J2339_LightCurve_Residuals.png         # Fig 1 (Light curve, pulls & MC outlier histograms)
    ├── J2339_Crowding_DifferenceImaging.png   # Fig 2 (TPF difference S/N maps & physical fluxes)
    ├── J2339_InjectionRecovery.png            # Fig 3 (FRED recovery curves & matched-filter heatmap)
    └── J2339_RedNoise_CandidateEvent.png      # Fig 4 (Binned RMS, log-binned PSD & S70 event)
