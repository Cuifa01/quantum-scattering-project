# Quantum Scattering

This project studies one-dimensional quantum scattering through a symmetric double-barrier potential. It combines stationary-state calculations, time-dependent wave-packet simulations, a finite-box basis method, and complex scaling.

The main numerical results include:

- free propagation of Gaussian wave packets;
- a finite-cutoff representation of the Dirac delta function;
- transmission spectra and resonant-tunnelling peaks;
- reflected and transmitted wave-packet dynamics;
- bound and continuum states from a sine-basis Hamiltonian;
- resonance poles and widths obtained by complex scaling.

## Code

The Python project is in `Yifeng CHEN 999016959/Codes and Figures`.

- `part1.py` to `part6.py` reproduce the six sections of the report.
- `run_all.py` runs the complete calculation.
- `src/quantum_scattering` contains the numerical methods.
- `output` contains the generated figures, data, and animations.

## Running the project

Python 3.10 or newer is required.

```bash
cd "Yifeng CHEN 999016959/Codes and Figures"
python -m pip install -e .
python run_all.py --profile quick
```

Use the `reference` or `full` profile for higher-resolution calculations. The complex-scaling calculation in Part 6 is the most computationally demanding part.

## Report

The project report is included as `Yifeng CHEN 999016959/Quantum Scattering Project Report.docx`.

