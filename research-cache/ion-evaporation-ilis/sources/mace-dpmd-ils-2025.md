# "Ionic Liquid Molecular Dynamics Simulation with Machine Learning Force Fields: DPMD and MACE"
URL: https://arxiv.org/html/2503.18249
Accessed: 2026-03-12

## Key results
- MACE force accuracy: RMSE 0.011 eV/Å, MAE 0.008 eV/Å
- DPMD force accuracy: RMSE 0.053 eV/Å, MAE 0.039 eV/Å
- System size: 10 ion pairs (~0.77-1.6 nm boxes) — small
- ILs tested: PYR14BF4, LiTFSI/PYR14TFSI

## Training data requirements
- PYR14BF4: 30,812 DFT structures (5k equilibrated + 6k non-equilibrated + 19,812 iterative)
- LiTFSI/PYR14TFSI: 22,992 structures across 5 concentrations
- Critical: need both equilibrated AND non-equilibrated structures

## Properties reproduced
- Density (MACE within 1% of experimental for binary systems)
- Diffusion coefficients
- Radial distribution functions
- Molecular configuration distributions

## Limitations
- DPMD produced density 20% off (1.28 vs 1.07 g/cm³ experimental) despite faster dynamics
- Pre-trained foundation models (MPA-0, OMAT-0) failed without fine-tuning
- Only bulk properties tested — no interface, no external field
- Small system sizes (10 ion pairs)
- Question of whether models capture correct physics vs just fitting

## Relevance to ILIS
- Nobody has trained MLFF for IL/vacuum interface under field
- The tools exist but the specific application is untouched
- Enhanced sampling (umbrella sampling, metadynamics) + MLFF = potential attack vector for ion extraction free energy
- Need larger systems for slab geometry (~500-1000 ion pairs minimum)
