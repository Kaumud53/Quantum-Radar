# Entanglement-Enhanced Quantum Radar via Dual-Arm GKSL Dynamics and Fidelity-Based Target Discrimination

**Authors:** Kumar Gautam, Kaumud Sharma
**Affiliation:** Department of Quantum Computing, Quantum Research and Centre of Excellence (QRACE), Delhi, India

> Status: Under review

## Abstract

This paper develops a mathematically rigorous quantum radar framework by extending a layered classical-quantum (Cq) channel theory to quantum illumination. The probe state is a two-mode squeezed vacuum (TMSV) state generated via spontaneous parametric down-conversion, establishing a **quantum vacuum-seeded receiver (QVR)** architecture: the signal mode illuminates the target while the idler mode is retained locally as a quantum reference.

The complete dual-arm open-system dynamics are derived: the signal arm (round-trip atmospheric amplitude damping and phase dephasing) and the idler arm (quantum-memory decoherence) are governed by two coupled GKSL master equations, plus a weak, common-oscillator-induced cross-dephasing term that vanishes when the signal and idler reference oscillators are independent.

The central performance metric is the **Uhlmann photon fidelity** between the full two-mode returned state and the ideal noiseless TMSV reference. From this we derive a Neyman-Pearson-optimal detector — bounded via the Fuchs–van de Graaf and quantum Stein inequalities rather than the quantum Chernoff bound — and an upper bound linking estimation precision to expected fidelity loss (the fidelity-QCRB link). We derive the three-parameter quantum Fisher information matrix (QFIM) for the radar parameter vector (target reflectivity, round-trip delay/range, Doppler shift), proving that off-diagonal reflectivity–kinematic couplings vanish to leading order, and benchmark the resulting quantum advantage against the coherent-state QFIM under matched loss and photon number — finding a **bounded, loss-limited advantage rather than unconditional Heisenberg scaling**. The Semigroup Julia Inversion Problem (SJIP) NP-hardness result is ported from the fibre-communication context to establish dual-layer anti-jamming security.

## Key Contributions

1. **Dual-arm GKSL master equation** (Theorem 1) with a physically motivated cross-dephasing term arising from phase noise common to the shared laser source (SPDC pump / idler-readout local oscillator) — not from bath-level correlations, since the atmospheric and quantum-memory reservoirs are physically independent.
2. **Exact bosonic Kraus operator representation** (Theorem 2) for the dual-arm channel, including the countable amplitude-damping family and continuous phase-damping family, with an explicit Duhamel-identity treatment of the cross-term correction.
3. **Uhlmann photon fidelity as the detection metric** (Definition 4, Theorem 3): the *joint* two-mode fidelity between the full bipartite output state and the ideal noiseless TMSV reference — distinguished explicitly from the (physically vacuous) fidelity between reduced single-mode marginals.
4. **Neyman-Pearson detection threshold** (Theorem 4) via the Helstrom POVM, bounded with the Fuchs–van de Graaf inequality (single-shot) and the quantum Stein lemma / quantum relative entropy (asymptotic, many-copy) — rather than the quantum Chernoff bound.
5. **Fidelity-QCRB link** (Theorem 5): a corrected upper bound showing that estimation error depresses expected fidelity below its ideal value (not a lower bound guaranteeing high fidelity from good estimation).
6. **Three-parameter QFIM** (Theorem 6) for Θ = (κ, τ, Δω) — target reflectivity, round-trip delay/range, Doppler shift — block-diagonal to leading order via an explicit σz/σx parity argument.
7. **Classical coherent-state benchmark** (Section V.C) under matched loss and mean photon number, showing the quantum advantage is a **bounded, loss-limited multiplicative factor**, not unbounded Heisenberg (n̄²) scaling — consistent with the "entanglement advantage without entanglement" literature.
8. **Weak-commutativity verification** (Proposition 2) confirming the SLD-QCRB is jointly attainable across all three parameters via an adaptive sequential protocol (Theorem 7, Algorithm 1).
9. **Dual-layer anti-jamming security** (Theorems 8–9): SJIP NP-hardness for spoof-state synthesis, combined with information-theoretic channel non-injectivity.
10. **Numerical validation**: adaptive Bayesian (particle-filter) estimation at a realistic operating point (10 km range, 150 m/s target, r = 2.0 squeezing), reporting 6.0 dB / 4.5 dB / 2.2 dB improvements in reflectivity / range / velocity precision over the coherent-state benchmark.

## Repository Contents

```
.
├── paper/                # Manuscript source (LaTeX) and compiled PDF
├── simulations/          # Python implementation of Algorithm 1 (adaptive Bayesian estimator)
│   ├── qvr_channel.py     # Dual-arm GKSL channel, Kraus operators, covariance propagation
│   ├── qfim.py            # Three-parameter Gaussian QFIM computation
│   ├── fidelity.py        # Uhlmann photon fidelity (Theorem 3) and discrimination fidelity
│   ├── particle_filter.py # Sequential Monte Carlo / adaptive Bayesian estimator (Algorithm 1)
│   └── classical_benchmark.py  # Coherent-state QFIM benchmark (Section V.C)
├── figures/              # Generated figures (Table I operating point, convergence plots)
└── README.md
```

*(Adjust the tree above to match your actual repo layout before pushing.)*

## Model Summary

| Quantity | Symbol | Notes |
|---|---|---|
| Squeezing parameter | r | Mean photon number n̄ = sinh²r |
| Signal round-trip loss rate | γ_loss^(s) | Beer–Lambert, Eq. (5) |
| Signal round-trip dephasing rate | γ_φ^(s)(τ) | Kolmogorov turbulence (Rytov variance), Eq. (8) |
| Idler memory loss/dephasing | γ_loss^(i), γ_φ^(i) | Quantum-memory decoherence |
| Cross-dephasing rate | γ_cross | Shared local-oscillator phase noise, bounded by oscillator linewidth, Eq. (22) |
| Target reflectivity | κ | Enters as effective transmissivity η̃_s = κη_s |
| Round-trip delay | τ = 2L/c | Encodes range R = cτ/2 |
| Doppler shift | Δω | Target radial velocity |

Detection metric: Uhlmann fidelity **F(ρ_si^(out), ρ_si^(ref))** between the full two-mode returned state and the ideal noiseless TMSV state (Eq. 40–41), reducing in the weak-noise regime to Eq. (43).

## Simulation Parameters (Table I)

| Parameter | Value |
|---|---|
| Squeezing parameter r | 2.0 (n̄ ≈ 13.8 photons) |
| Signal wavelength | 1.55 µm |
| Target range | 10 km |
| Target reflectivity κ | 0.1 |
| Target velocity | 150 m/s |
| Atmospheric loss rate | 0.05 dB/km |
| Atmospheric dephasing rate | 0.01 rad/km |
| Memory loss rate | 10⁻⁴ dB/µs |
| Memory dephasing rate | 10⁻⁵ rad/µs |
| Bath correlation C_si | 0.01 |
| Signal-arm thermal background n̄_th^(s) | 0 |
| Measurement rounds M | 100 |
| Particles N_p | 500 |

## Results

- QFIM at the true operating point (numerically exact, not the weak-noise closed form — see Section VII.A for why the closed-form expressions are inapplicable at this κ):

  F(Θ_true) = [[8.47, 0, 0], [0, 12.34, −3.21], [0, −3.21, 18.76]]

- Estimator convergence to within the offset-prior neighborhood in ~40 rounds; achieved CRB approaches the QCRB to within ~8–15% by round 50.
- Quantum advantage over the matched coherent-state benchmark: **6.0 dB** (reflectivity), **4.5 dB** (range), **2.2 dB** (velocity) — bounded, loss-limited gains at fixed channel parameters, not evidence of asymptotic Heisenberg scaling.

## Corrections from Earlier Drafts

This version supersedes an earlier draft and fixes several issues raised in review:

- Atmospheric loss/dephasing rate definitions corrected for dimensional consistency (Definition 3); free-space turbulence (Rytov/Kolmogorov) dephasing replaces the fibre-optic polarisation-mode-dispersion expression.
- The cross-decoherence term is re-derived as a **shared-local-oscillator phase-noise effect**, not a bath correlation (the two reservoirs are physically independent).
- Exact bosonic (infinite-dimensional) Kraus operators replace an earlier qubit-truncated form that failed completeness on Fock states with n > 1.
- The detection/reference fidelity confusion (marginal vs. joint-state fidelity) is resolved: only the full two-mode Uhlmann fidelity is used as the detection-relevant quantity.
- The Neyman-Pearson threshold no longer relies on the quantum Chernoff bound (a symmetric-error quantity); it uses the Fuchs–van de Graaf bound (single-shot) and the quantum Stein lemma (asymptotic).
- The fidelity-QCRB theorem's sign error is corrected: it is now stated as an **upper bound** (estimation error depresses expected fidelity), not a lower bound.
- The QFIM/classical-benchmark scaling claim is corrected from "Heisenberg scaling" to a **bounded, loss-limited quantum advantage**, consistent with known quantum-illumination results in the presence of loss and thermal noise.
- A factor-of-2 error in the classical coherent-state Doppler QFIM is corrected, revising the reported velocity-estimation quantum advantage from 5.2 dB to 2.2 dB.
- Weak-commutativity of the SLDs (Proposition 2) is verified explicitly, justifying joint attainability of the SLD-QCRB via the adaptive protocol.

## Reproducing the Simulations

```bash
pip install -r requirements.txt
python simulations/particle_filter.py --config configs/table1.yaml
```

This reproduces the QFIM evaluation (Eq. 75), the particle-filter convergence trajectories, and the dB-improvement comparison against the classical benchmark (Section VII.B).

## Citation

If you use this work, please cite:

```bibtex
@article{gautam_sharma_quantum_radar,
  title   = {Entanglement-Enhanced Quantum Radar via Dual-Arm GKSL Dynamics and Fidelity-Based Target Discrimination},
  author  = {Gautam, Kumar and Sharma, Kaumud},
  journal = {Under review},
  year    = {2026}
}
```

## Related Work

This paper extends the five-layer fibre-optic classical-quantum channel framework of:

> K. Gautam and K. Sharma, "A rigorous quantum communication framework for optical fibre channels: Integrated control, computational hardness, and noise-assisted security," *IEEE Trans. Quantum Eng.*, 2024 (submitted).

## Acknowledgments

The authors gratefully acknowledge Prof. K. R. Parthasarathy for invaluable guidance on quantum stochastic differential equations and their application to open quantum systems. K.S. acknowledges support from the Quantum Research and Centre of Excellence, Delhi.
