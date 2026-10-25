# Structures of the Basic Reproduction Number $\mathcal{R}_0$

Mathematica notebooks accompanying the review

> Z. Qu and A. Ashwath, *Structures of the Basic Reproduction Number $\mathcal{R}_0$ Across Compartmental Disease Models: A Short Review*. Submitted to the *Bulletin of Mathematical Biology* (2026).

Each notebook derives $\mathcal{R}_0$ for one example model in the paper using the next-generation matrix (NGM) method, so that every expression in the paper can be reproduced symbolically.

## Notebooks

| Notebook | Section | Model | $\mathcal{R}_0$ structure | Paper eq. |
|---|---|---|---|---|
| `Sec2_SEIR.nb` | 2 | SEIR with demography | Product of survival, transmission rate, duration | (2) |
| `Sec3.1_SP_WeightedSum.nb` | 3.1 | Staged progression (SP), $n=3$ stages | Weighted sum $\sum_i P_i\mathcal{R}_0^{(i)}$ | (6) |
| `Sec3.1_DI_WeightedSum.nb` | 3.1 | Differential infectivity (DI), $n=3$ groups | Weighted sum $\sum_i p_i\mathcal{R}_0^{(i)}$ | (7) |
| `Sec3.2_MultiStrain_Max.nb` | 3.2 | Competing strains, $n=3$ strains | Maximum $\max_i \mathcal{R}_0^{(i)}$ | (8) |
| `Sec3.3_Relapse_Cyclic.nb` | 3.3 | SIAR model with relapse | Geometric series $\mathcal{R}_0^{\text{cycle}}/(1-P_\gamma)$ | (11), (14) |
| `Sec3.4_iNTS_Combined.nb` | 3.4 | iNTS, 4 risk groups × 5 infected stages | Combined: SP + cyclic + DI | (17) |
| `Sec3.5_VectorBorne_GeometricMean.nb` | 3.5.1 | SIS host – SI vector | Geometric mean $\sqrt{\mathcal{R}_{VH}\mathcal{R}_{HV}}$ | (19) |
| `Sec4.1_Wolbachia_FitnessRatio.nb` | 4.1 | *Wolbachia* population replacement | Fitness ratio $\mathcal{G}_{0w}/\mathcal{G}_{0u}$ | (21) |
| `Sec4.2_Medea_FitnessRatio.nb` | 4.2 | *Medea* gene drive | Genotypic fitness ratio | (24) |

## Workflow

Every notebook follows the same sequence of cells:

1. `Exit` — restart the kernel.
2. Model definition — the ODE system, force of infection, infected state vector `infectedVars`, and the new-infection and transition vectors `calF` ($\mathcal{F}$) and `calV` ($\mathcal{V}$).
3. Display `calF` and `calV`.
4. Disease-free equilibrium `DFE`, and the Jacobians `F` and `V` evaluated there.
5. Next-generation matrix `NGM` $= FV^{-1}$.
6. Eigenvalues of `NGM`.
7. `R0` — the largest eigenvalue (spectral radius), simplified under positivity assumptions on the parameters.

Run with **Evaluation → Evaluate Notebook**.

## Conventions

- **Notation follows the paper.** Parameters use Greek symbols ($\beta$, $\gamma$, $\mu$, $\sigma$, …); multi-index quantities append the index to the name (e.g. `γ1`, `γ1H`, `μfw`, `ϕ01`).
- **Compartment names.** `E`, `I`, `N` and `D` are protected built-in symbols in Mathematica, so compartments carry an `H` suffix where needed (`SH`, `EH`, `IH`, `RH`, `NH`, `DH`). Stage indices follow the suffix (`IH1`, `IH2`, …).
- **Finite $n$.** Models with $n$ stages, groups, or strains in the paper are coded with $n = 3$.
- **iNTS model.** With 20 infected states, the notebook uses indexed variables (`IH1[k]`, `γ12[k]`, …, $k=1,\dots,4$) built with `Table`. Because $F$ has rank one, $\mathcal{R}_0$ is computed as the trace of the NGM, rather than from a symbolic $20\times20$ eigenvalue problem. A final cell checks the result against the weighted-sum form, Eq. (17), using the stage durations $\tau_j$ and branching probabilities $P_{jk}$ of Eq. (15), with natural death counted as an exit from each stage.

## Requirements

Wolfram Mathematica (notebooks created with version 14.2). No packages are required.

## Contact

Zhuolin Qu, Department of Mathematics, University of Texas at San Antonio — zhuolin.qu@utsa.edu
