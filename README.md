# Entanglement-Enhanced Quantum Radar via Dual-Arm GKSL Dynamics and Fidelity-Based Target Discrimination

**Authors:** Kumar Gautam, Kaumud Sharma

## Overview

This repository contains the manuscript, simulation code, and figures for a paper that extends the five-layer fibre-optic classical-quantum (Cq) channel framework of "A Rigorous Quantum Communication Framework for Optical Fibre Channels" to **quantum illumination / quantum radar**.

The core probe is upgraded from a single-mode coherent state to a **two-mode squeezed vacuum (TMSV)** state generated via spontaneous parametric down-conversion (SPDC): the signal mode illuminates the target region while the idler mode is retained locally as a quantum reference (the **quantum vacuum-seeded receiver**, QVR, architecture). The paper derives the full open-system dynamics of this dual-arm system, a fidelity-based detection metric, a three-parameter estimation theory, and an anti-jamming security guarantee.

## Key Contributions

- **Dual-arm GKSL master equation** (Theorem 1) for the coupled signal (round-trip atmospheric loss + turbulence dephasing) and idler (quantum-memory decoherence) arms, including a weak common-oscillator cross-dephasing term — with an explicit, physically grounded account of *why* that cross-term exists (shared laser/local-oscillator phase noise) and *why* it is not due to correlated baths
- **Exact bosonic Kraus-operator representations** (Theorem 2) for both arms, plus a first-order Duhamel treatment of the cross-decoherence correction
- **Uhlmann photon fidelity** between the full two-mode returned state and the ideal noiseless TMSV reference as the central detection metric (Definition 4, Theorem 3), with a careful distinction from the *discrimination* fidelity between the two hypothesis states
- A **Neyman-Pearson optimal detector** analysis bounded via the Fuchs–van de Graaf inequalities and the quantum Stein lemma (Theorem 4) — explicitly *not* using the quantum Chernoff bound, since that bound characterises a different (symmetric-error) hypothesis-testing problem
- A **fidelity–QCRB link theorem** (Theorem 5) bounding expected fidelity loss above in terms of estimator covariance
- The **three-parameter QFIM** for target reflectivity κ, round-trip delay τ (range), and Doppler shift Δω (Theorem 6), showing a block-diagonal structure (reflectivity decouples from kinematics at leading order) via an explicit parity argument
- A **classical coherent-state benchmark** at matched loss and mean photon number, showing the quantum advantage is **bounded and loss-limited**, not unconditional Heisenberg (∝ n̄²) scaling — a point the paper is explicit about correcting relative to an earlier draft
- **Dual-layer anti-jamming security** (Theorems 8–9), porting the Semigroup Julia Inversion Problem (SJIP) NP-hardness result from the fibre-communication eavesdropping context to spoof-state synthesis by a radar jammer
- An **adaptive Bayesian estimation algorithm** (Algorithm 1) for the three-parameter radar space, validated numerically, including a weak-commutativity check (Proposition 2) needed for the adaptive POVM sequence to jointly saturate the SLD-QCRB

## Repository Contents

```
.
├── paper/              # Manuscript source (LaTeX) and compiled PDF
├── simulations/        # Python implementation of Algorithm 1 (adaptive Bayesian radar estimator)
├── figures/            # Generated figures (QFIM convergence, fidelity vs. range, dB-advantage plots)
└── README.md
```

*(Adjust the folder names above to match the actual repository layout.)*

## Simulation Details

Numerical validation of Algorithm 1 was implemented in **Python** using a sequential Monte Carlo / particle-filter approximation.

| Parameter | Symbol | Value |
|---|---|---|
| Squeezing parameter | r | 2.0 (n̄ ≈ 13.8 photons) |
| Signal wavelength | λ_s | 1.55 µm |
| Target range | R | 10 km |
| Target reflectivity | κ | 0.1 |
| Target velocity | v | 150 m/s |
| Atmospheric loss rate | γ_loss^(s) | 0.05 dB/km |
| Atmospheric dephasing rate | γ_φ^(s) | 0.01 rad/km |
| Memory loss / dephasing rates | γ_loss^(i), γ_φ^(i) | 10⁻⁴ dB/µs, 10⁻⁵ rad/µs |
| Shared-oscillator correlation | C_si | 0.01 |
| Measurement rounds | M | 100 |
| Particles | N_p | 500 |

True parameters: κ = 0.1, τ = 66.7 µs, Δω = 2π × 19.4 kHz (a target at 10 km moving at 150 m/s), estimated from a deliberately offset Gaussian prior.

**Reported quantum advantage** (TMSV vs. matched-photon-number coherent-state benchmark, at this fixed operating point):

- 6.0 dB improvement in reflectivity estimation precision
- 4.5 dB improvement in range estimation precision
- 2.2 dB improvement in velocity estimation precision

These are **finite, loss-limited gains at a fixed operating point** — not evidence of asymptotic Heisenberg scaling, since the QFIM's quadratic-in-n̄ scaling is only exact in the idealised, noiseless-channel limit.

### Reproducing the Results

```bash
# example — update to match actual script names
pip install numpy scipy matplotlib
python simulations/run_algorithm1_radar.py
```

This regenerates the posterior convergence plots for (κ, τ, Δω), the achieved-CRB-vs-QCRB comparison, and the dB-advantage figures reported in Section VII.

## Scope and Honesty Notes

This manuscript incorporates several explicit corrections relative to earlier drafts, each documented in-text at the point it matters:

- The **fidelity metric** is defined only between full two-mode joint states (Definition 4), not single-mode marginals — using marginals would make the metric blind to the signal-idler entanglement the receiver is built to exploit.
- The **fidelity-QCRB link theorem** (Theorem 5) is an *upper bound* on expected fidelity, not a lower bound: high fidelity is not claimed to be necessary for accurate estimation.
- The **detection threshold** (Theorem 4) is derived from the Fuchs–van de Graaf inequalities and the quantum Stein lemma, not the quantum Chernoff bound, which applies to a different (symmetric-error) hypothesis-testing problem.
- The **quantum advantage is explicitly bounded and loss-limited**, not unconditional Heisenberg scaling — the paper corrects an earlier claim to the contrary and re-derives the numerical dB figures accordingly (including a corrected classical-benchmark Doppler QFI that revises the reported velocity-estimation advantage down from 5.2 dB to 2.2 dB).
- **Dimensional consistency** of the atmospheric noise rates (Definition 3) and the anti-jamming bound (Theorem 9) is corrected to use round-trip *time* (t = 2L/v_g) rather than round-trip *distance* in the exponent.
- The **weak-commutativity condition** (Proposition 2) required for a single adaptive POVM sequence to saturate the full multiparameter QCRB is stated and verified explicitly, rather than assumed via LAN alone.

## Citation

If you use this work, please cite:

```bibtex
@article{gautam_sharma_quantum_radar,
  title   = {Entanglement-Enhanced Quantum Radar via Dual-Arm GKSL Dynamics
             and Fidelity-Based Target Discrimination},
  author  = {Gautam, Kumar and Sharma, Kaumud},
}
```

*(Update with the final venue, volume, page numbers, and DOI once published.)*

## Related Work

This paper is a direct extension of the authors' fibre-optic Cq channel framework:

> K. Gautum and K. Sharma, "A Rigorous Quantum Communication Framework for Optical Fibre Channels: Integrated Control, Computational Hardness, and Noise-Assisted Security," *IEEE Trans. Quantum Eng.*, 2024 (submitted).

## Acknowledgements

The authors thank Prof. K. R. Parthasarathy for invaluable guidance on quantum stochastic differential equations and their application to open quantum systems. KS acknowledges support from the Quantum Research and Centre of Excellence, Delhi.
