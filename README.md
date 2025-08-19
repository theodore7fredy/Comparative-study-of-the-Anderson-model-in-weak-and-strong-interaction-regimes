# Comparative study of the Anderson model in weak and strong interaction regimes
**Implementations in Julia (`HierarchicalEOM.jl`) and Python (`QuTiP`)**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Julia](https://img.shields.io/badge/Julia-1.10%2B-blue)]()
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)]()

> This repository presents a systematically analyzing key observables, including spectral density $A(\omega)$, impurity occupation, time-dependent current, and differential conductance for the single impurity coupled to two fermionic reservoirs (Anderson model) for weak and strong interaction regimes and we reveal clear and quantifiable contrasts, using **HierarchicalEOM.jl** ( based on Julia) and **QuTiP** (based in Python).

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
We benchmark two HEOM implementations on the Single Impurity Anderson Model to capture:
- **Spectral density** $\(A(\omega)\)$
- **Occupation** $\(\langle n_\sigma \rangle\)$
- **Electric Current** $\(I(\omega)\)$
- **Differential Conductance** $\(G(\omega)\)$

We provide scripts to **presente the kondo effects and hubbards pics at the fermi level**, **generate all plots**, and **compare for the two cases (weak and strong)** runtime, accuracy, and convergence behavior (hierarchy depth, quadrature/Padé parameters, etc.).

---

## Physics background
The Singe Interaction Anderson Model Hamiltonian:

$$
H = \varepsilon \left( d_{\uparrow}^\dagger d_{\uparrow} + d_{\downarrow}^{\dagger}
d_{\downarrow} \right) + U \left( d_{\uparrow}^\dagger d_{\uparrow}
d_{\downarrow}^{\dagger} d_{\downarrow} \right) +
\sum_{\alpha = L, R} \sum_{\sigma_f = \uparrow, \downarrow} \sum_k
\varepsilon_{\alpha, \sigma_f, k} c_{\alpha, \sigma_f, k}^\dagger c_{\alpha, \sigma_f, k} +
\sum_{\alpha = L, R} \sum_{\sigma_f = \uparrow, \downarrow} \sum_k
g_{\alpha, k} c_{\alpha, \sigma_f, k}^\dagger d_{\sigma_f} + g_{\alpha, k}^*
d_{\sigma_f}^{\dagger} c_{\alpha, \sigma_f, k},
$$

with $\(\alpha \in \{L, R\}\)$ leads (chemical potentials $\(\mu_L,\mu_R\))$ and temperature $\(T\)$.
- **Weak interaction**: Kondo resonance near $\(\omega=0\)$, **Hubbard peaks** near $\(\epsilon_d\) and \(\epsilon_d + U\)$.
- **Strong interaction**: Kondo peak suppressed; **Hubbards peaks diverges**

---

## Methods
- **Julia / `HierarchicalEOM.jl`**: HEOM based on **collection of methods to compute bosonic
and fermionic spectra, stationary states, and the full dynamics in the extended space of all
Auxiliary Statistical Operators (ASOs)**, efficient for deep hierarchies.
- **Python / `QuTiP`**: HEOM following the **Tanimura** formalism with respect hierarchie; user-friendly prototyping and integration with the broader QuTiP ecosystem.

Key numerical controls (both stacks):
- Hierarchy depth / truncation
- Bath decomposition (Padé / Matsubara), number of terms
- Time stepping / steady-state solvers
- Broadening and frequency grids for \(A(\omega)\)
- Convergence checks (observables vs. hierarchy depth, bath terms)

---

## Repository structure

