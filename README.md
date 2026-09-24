# Quantum Scattering

Numerical experiments on one-dimensional quantum scattering through a symmetric double-barrier potential. The project compares stationary scattering, time-dependent wave packets, finite-box diagonalization, and complex scaling within one consistent model.

The calculations are written in Python with NumPy, SciPy, and Matplotlib. Scripts, generated figures, animations, numerical data, and the full report are included in the repository.

## Main results

The double barrier supports resonant tunnelling: transmission is normally suppressed below the barrier height, but rises sharply when the incident energy matches a quasi-bound state in the central well.

The stationary calculation gives two low-energy transmission peaks:

| Resonance | Transmission peak | Complex pole | Width |
| --- | ---: | ---: | ---: |
| First | 0.62097030 | 0.620971 - 0.000058i | 0.000116 |
| Second | 1.32882395 | 1.327197 - 0.015447i | 0.030894 |

The first resonance is extremely narrow, while the second is visibly broader. The complex-scaled spectrum reproduces this difference through the imaginary parts of the resonance poles.

![Transmission probability through the double barrier](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part3_stationary_scattering/transmission_profile.png)

## Wave-packet scattering

Time-dependent packets are constructed from the stationary scattering states. Changing the momentum distribution produces three clear regimes: reflection in a low-transmission interval, splitting when the packet overlaps both transmitting and reflecting energies, and almost complete transmission at high energy.

| Blocked | Partially transmitted | Passing |
| --- | --- | --- |
| ![Blocked wave packet](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/blocked.png) | ![Partially blocked wave packet](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/partially_blocked.png) | ![Passing wave packet](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/pass.png) |

Animated versions of these calculations, together with narrow packets centred on both resonances, are available in the [`part4_wavepacket_scattering`](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering) directory.

### Scattering animations

The animations make the difference between the three energy regimes easier to see than a single snapshot.

| Low-transmission packet | Mixed-transmission packet | High-energy packet |
| --- | --- | --- |
| ![Blocked packet animation](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/blocked.gif) | ![Partially blocked packet animation](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/partially_blocked.gif) | ![Passing packet animation](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/pass.gif) |

- **Blocked:** the packet reaches the barrier and returns to the incident side. Only a small transient amplitude enters the central region.
- **Partially blocked:** the initial momentum distribution covers both high- and low-transmission components. The packet therefore separates into visible reflected and transmitted pieces.
- **Pass:** the energy range lies in a region where the transmission is already close to one, so the reflected component is very small.

### Packets centred on the resonances

The first resonance is so narrow that the momentum distribution must also be very narrow. By the uncertainty relation, this produces a packet that is broad in position space. The second resonance has a larger width and can support a more localized incident packet.

| First resonance | Second resonance |
| --- | --- |
| ![Wave packet at the first resonance](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/first_resonance_zoom.gif) | ![Wave packet at the second resonance](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part4_wavepacket_scattering/second_resonance_zoom.gif) |

In both cases, most spectral components lie inside a transmission peak and pass through the double barrier. The contrast in spatial width reflects the large difference between the two resonance widths.

## Free propagation

Before introducing the potential, the code checks the motion of a free Gaussian packet. Its centre moves at the group velocity set by the mean momentum, while the packet spreads because different momentum components acquire different phases.

![Free Gaussian wave-packet propagation](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part1_free_gaussian/free_propagation.gif)

This provides a useful reference for the later scattering animations: translation and ordinary dispersion are already present without a potential, whereas splitting and strong reflection are produced by the double barrier.

## Numerical approach

The project is organized into six calculations.

1. **Free Gaussian packet** — examines the effects of initial width and mean momentum, then follows free propagation and spreading.
2. **Regularized Dirac delta** — tests a finite-cutoff delta representation against a smooth function and checks convergence as the cutoff increases.
3. **Stationary scattering** — solves the finite-difference Schrödinger equation across the double barrier and extracts reflection and transmission amplitudes.
4. **Time-dependent scattering** — superposes stationary states with Gaussian momentum weights to simulate reflected and transmitted packets.
5. **Finite-box basis** — constructs the Hamiltonian in a sine basis, validates it with a shifted harmonic oscillator, and identifies the bound state and box-discretized continuum states.
6. **Complex scaling** — rotates the continuum spectrum into the complex plane, isolates stable resonance poles, and compares their Breit-Wigner profiles with the real-energy transmission curve.

### Finite-box spectrum

The sine-basis calculation first reproduces the harmonic-oscillator spectrum. Applied to the double-barrier potential, it finds one negative-energy bound state and a dense sequence of positive-energy box states. Two box states lie close to the resonance energies found from scattering.

![Selected bound and resonance-like box states](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part5_box_basis/three_localized_states.png)

### Complex-scaled spectrum

Under complex scaling, continuum eigenvalues rotate into the lower half of the complex-energy plane. The resonance poles remain nearly stationary as the rotation angle changes, making them distinguishable from the discretized continuum.

| Complex eigenvalues | Breit-Wigner comparison |
| --- | --- |
| ![Complex-scaled eigenvalue spectrum](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part6_complex_scaling/complex_eigenvalues_all.png) | ![Breit-Wigner and finite-difference transmission](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output/part6_complex_scaling/breit_wigner_profiles_zoom.png) |

## Repository structure

```text
Yifeng CHEN 999016959/
├── Quantum Scattering Project Report.docx
└── Codes and Figures/
    ├── part1.py ... part6.py
    ├── run_all.py
    ├── pyproject.toml
    ├── src/quantum_scattering/
    └── output/
```

The six `part*.py` scripts reproduce the corresponding sections of the report. The reusable numerical routines are kept in `src/quantum_scattering`, while `output` contains the generated figures, animations, and CSV data.

## Running the calculations

Python 3.10 or newer is required.

```bash
cd "Yifeng CHEN 999016959/Codes and Figures"
python -m pip install -e .
python run_all.py --profile quick
```

Three calculation profiles are available:

- `quick` uses smaller grids and fewer animation frames for a short test run;
- `reference` reproduces the standard figures at the report settings;
- `full` uses the largest grids, including the full complex-scaling calculation.

Individual sections can also be run separately:

```bash
python part3.py
python part4.py --profile reference
python part6.py --profile full
```

Part 6 is the most computationally demanding calculation. To regenerate only static figures for Parts 1 and 4, add `--skip-gifs`.

## Report and outputs

The full derivation, parameter choices, and discussion are in [`Quantum Scattering Project Report.docx`](Yifeng%20CHEN%20999016959/Quantum%20Scattering%20Project%20Report.docx).

All generated results are grouped by calculation in [`Codes and Figures/output`](Yifeng%20CHEN%20999016959/Codes%20and%20Figures/output).
