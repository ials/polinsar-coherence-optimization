# PolInSAR Dashboards

Interactive, client-side reconstructions of Polarimetric SAR Interferometry (PolInSAR) papers
and models. Each dashboard is a single self-contained HTML file — all computation (coherence
models, eigensolvers, Monte-Carlo noise simulation, grid-search inversion) runs live in your
browser via plain JavaScript, numerically verified against the source paper's equations.

**Live site:** https://ials.github.io/polinsar-coherence-optimization/

## Dashboards

### [Single-Baseline Polarimetric SAR Interferometry](papathanassiou-cloude-2001.html)
> K.P. Papathanassiou, S.R. Cloude, *IEEE Transactions on Geoscience and Remote Sensing*,
> vol. 39, no. 11, Nov. 2001.

Given a random-volume-over-ground (RVoG) scene, the interferometric coherence γ(w) depends
on the choice of polarization w only through the ground-to-volume amplitude ratio m(w). Since
m(w) is a generalized Rayleigh quotient of the ground and volume Pauli coherency matrices, its
extremal values are exactly a generalized eigenvalue problem — the origin of "polarimetric
coherence optimization." Solved here in closed form (exact under the paper's reflection-symmetry
ground model). Includes inversion-conditioning analysis (why a wide ground-to-volume-ratio
spectrum estimates height more reliably) and a simulated tree-height validation.

### [Tropical Forest Canopy Height — Temporal Decorrelation Models](forest-canopy-td.html)
> H. Luo, C. Yue, Y. Wu, X. Zhang, C. Lu, G. Ou, *Ecological Indicators* 166 (2024) 112566.

Runs all four of the paper's real stage-3 inversion algorithms live — RVoG, RMoG, RVoG+VTD,
and the paper's own faster single-loop RVoG+VTDs — demonstrating why repeat-pass temporal
decorrelation (mostly wind-driven canopy motion) makes a TD-blind model systematically
overestimate canopy height, and how each compensation strategy fixes it. Reproduces the
paper's real accuracy/efficiency numbers from AfriSAR Gabon mangrove validation (canopy up to
65 m, 4602 LiDAR RH100 points).

### [Multi-Baseline Forest Height — Analytic + Geometric RVoG](multibaseline-rvog-forest-height.html)
> B. Zhang, H. Zhu, W. Song, J. Zhu, J. Dai, J. Zhang, C. Li, *Forests* 2024, 15, 1496.

Reconstructs the paper's multi-baseline RVoG framework: each interferometric baseline traces
its own straight coherence locus in the unit circle, and noisy observations scatter into an
elliptical coherence region whose eccentricity is used to select the most trustworthy
reference baseline. Rather than discarding the other baselines, their geometric constraints
(perpendicular distance to each baseline's own fitted line) are minimized jointly with the
reference baseline's analytic RVoG fit — shown live, with an empirically-tuned cost function,
to sharpen and stabilize the height estimate versus single- or dual-baseline alternatives.
Reproduces the paper's real validation numbers from the Mabounie (AfriSAR) and Krycklan sites
(RMSE improved 39% and 17% respectively over the traditional optimal-single-baseline method).

### [Adaptive Volume Coherence Optimization — Single-Polarization Bistatic InSAR](adaptive-volume-coherence-optimization.html)
> J. Wan, C. Wang, Y. Lei, E. Chen, A. Fu, Y. Liu, L. Zhao, X. Liu, J. Xu, Y. Fan, Q. Song,
> *GIScience & Remote Sensing*, 63:1, 2637240 (2026).

Reconstructs Ada-VolOpt, the paper's method for inverting forest height from **single-polarization**
LuTan-1 bistatic InSAR: splitting each SLC into azimuth sub-looks (time-frequency analysis) to expand
the observation space, fitting the resulting coherences to the RVoG line in the complex unit circle, and
resolving the classic 1-D ground/volume ambiguity by requiring every sub-look's implied ground-to-volume
ratio to stay physically valid in [0, 1] simultaneously. A slope-adaptive RVoG lookup then inverts forest
height while correcting for the terrain-slope bias that otherwise distorts κ<sub>z</sub> and the local
incidence angle. Reproduces the paper's real validation numbers across the Hainan (tropical), Yanbian
(mixed), and Genhe (boreal) test sites (5.04 m / 3.41 m / 2.44 m accuracy; 8% / 10% / 33% improvement
over a method that ignores ground scattering).

## Running locally

Each dashboard is a single self-contained HTML file. It only requires internet access once,
to load [Plotly.js](https://plotly.com/javascript/) from a CDN. Open it directly in any modern
browser — no build step, no server required.

## Notes on fidelity

Each dashboard's own footer documents its modeling simplifications, closed-form derivations,
and exactly which panels use the paper's real reported numbers versus illustrative synthetic
data built to match the paper's qualitative and (where stated) quantitative findings — none of
the papers' original underlying datasets are redistributed here.
