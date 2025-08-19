# Comparative study of the Anderson model in weak and strong interaction regimes
**Implementations in Julia (`HierarchicalEOM.jl`) and Python (`QuTiP`)**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Julia](https://img.shields.io/badge/Julia-1.10%2B-blue)]()
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)]()

> This repository presents a side-by-side, reproducible comparison of the **single-impurity Anderson model (SIAM)** across **weak** and **strong** interaction regimes, using **HierarchicalEOM.jl** (Julia, influence functional decomposition) and **QuTiP** (Python, Tanimura HEOM).

---

## Table of Contents
- [Overview](#overview)
- [Physics background](#physics-background)
- [Methods](#methods)
- [Repository structure](#repository-structure)
- [Getting started](#getting-started)
  - [Julia setup](#julia-setup)
  - [Python setup](#python-setup)
- [Quick start: run the benchmarks](#quick-start-run-the-benchmarks)
- [Reproducibility](#reproducibility)
- [Results & figures](#results--figures)
- [Configuration](#configuration)
- [Citing](#citing)
- [References](#references)
- [License](#license)

---

## Overview
We benchmark two HEOM implementations on the SIAM to capture:
- **Spectral density** \(A(\omega)\)
- **Occupation** \(\langle n_\sigma \rangle\)
- **Current and differential conductance**
- **Kondo resonance** (in weak/intermediate interaction regimes)
- **Hubbard side peaks** (strong interaction)

We provide scripts to **reproduce datasets**, **re-generate all plots**, and **compare** runtime, accuracy, and convergence behavior (hierarchy depth, quadrature/Padé parameters, etc.).

---

## Physics background
The SIAM Hamiltonian:
\[
H = \epsilon_d \sum_\sigma n_\sigma + U n_\uparrow n_\downarrow +
\sum_{k,\alpha,\sigma} \epsilon_{k\alpha}\, c^\dagger_{k\alpha\sigma} c_{k\alpha\sigma} +
\sum_{k,\alpha,\sigma}\big( V_{k\alpha}\, d^\dagger_\sigma c_{k\alpha\sigma} + \text{h.c.} \big),
\]
with \(\alpha \in \{L, R\}\) leads (chemical potentials \(\mu_L,\mu_R\)) and temperature \(T\).
- **Weak interaction**: Kondo resonance near \(\omega=0\).
- **Strong interaction**: Kondo peak suppressed; **Hubbard peaks** near \(\epsilon_d\) and \(\epsilon_d + U\).

---

## Methods
- **Julia / `HierarchicalEOM.jl`**: HEOM based on **influence functional decomposition**, efficient for deep hierarchies.
- **Python / `QuTiP`**: HEOM following the **Tanimura** formalism; user-friendly prototyping and integration with the broader QuTiP ecosystem.

Key numerical controls (both stacks):
- Hierarchy depth / truncation
- Bath decomposition (Padé / Matsubara), number of terms
- Time stepping / steady-state solvers
- Broadening and frequency grids for \(A(\omega)\)
- Convergence checks (observables vs. hierarchy depth, bath terms)

---

## Repository structure

