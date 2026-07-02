# PolInSAR Coherence Optimization Dashboard

An interactive reconstruction of the core contribution of:

> K.P. Papathanassiou, S.R. Cloude, "Single-Baseline Polarimetric SAR Interferometry,"
> *IEEE Transactions on Geoscience and Remote Sensing*, vol. 39, no. 11, Nov. 2001.

Given a random-volume-over-ground (RVoG) scene, the interferometric coherence γ(w) depends
on the choice of polarization w only through the ground-to-volume amplitude ratio m(w). Since
m(w) is a generalized Rayleigh quotient of the ground and volume Pauli coherency matrices, its
extremal values are exactly a generalized eigenvalue problem — the origin of "polarimetric
coherence optimization." This dashboard solves that eigenproblem live (closed-form, under the
paper's reflection-symmetry ground model) and visualizes the resulting optimum coherences,
inversion conditioning, and a simulated tree-height validation.

**Live demo:** see the GitHub Pages link in the repo's "About" section (or `https://<username>.github.io/polinsar-coherence-optimization/`).

## Running locally

This is a single self-contained `index.html` file. It only requires internet access once,
to load [Plotly.js](https://plotly.com/javascript/) from a CDN. Open it directly in any
modern browser — no build step, no server required.

## Notes on fidelity

All computation (the eigensolver, the RVoG coherence model, Monte-Carlo N-look noise
simulation) runs client-side in JavaScript and was numerically verified against the paper's
equations. Panels 4-5 use illustrative synthetic data (not the paper's real Oberpfaffenhofen
dataset, which is not publicly redistributable) — this is disclosed in the dashboard's footer.
