# scalar-cloud-catalog-search
# Resonant Scalar Cloud Search with Public LVK Data

This folder contains the manuscript, figure products, postprocessed summary
tables, and scripts used for the ApJL draft on resonant scalar clouds in public
LIGO-Virgo-KAGRA compact-binary data.

The repository intentionally does not include public strain files or public
posterior HDF5 files.  Those files should be downloaded from GWOSC and the
corresponding LVK parameter-estimation releases.

## Main Results in This Snapshot

- Broad eps_B=15 catalog screen: 134 candidate black-hole components from 72
  events.
- Final eps_B=15 Ns=800 follow-up: 40 target components completed.
- Conditional saturated-cloud exclusions: 36 components from 34 events.
- Tightest direct retained limit: (S_c/M^2)_95 = 6.67e-3 for GW230518_125908
  at mu = 3.34e-12 eV.
- Strongest saturated-cloud model-to-limit ratio: 23.6.
- eps_B=5 gives direct sensitivity but no default T_cloud >= 1e8 yr exclusion.

GW230518_125908 was also checked with detector subsets.  The validation logs
show ln B = -0.08 for H1 alone, ln B = 5.47 for L1 alone, ln B = 2.74 for the
H1,L1 network, and ln B = 1.94 after notching the local L1 band around 44 Hz.

## Folder Layout

- `paper/`: AASTeX manuscript, compiled PDF, references, and figure files.
- `scripts/`: local postprocessing and figure-generation scripts.
- `data/eps15_ns800_final/`: final eps_B=15 Ns=800 summary tables and model
  comparison products.
- `data/eps5_eps15_catalog/`: lifetime-threshold summary table for eps_B=15
  and eps_B=5.
- `validation/`: GW230518_125908 detector-subset validation logs.
- `hpc_campaigns/`: Slurm campaign scripts used for the final follow-up runs.

## Reproduce the Local Summary and Figures

From the original project root, after unpacking the HPC result tarball:

```bash
python analyze_eps15_ns800_followup.py \
  --base hpc_final_20260608_175421 \
  --outdir analysis_outputs/eps15_ns800_final_20260608_175421

python make_apjl_fig2_catalog_summary.py
python make_apjl_interval_figure.py
python make_eps_lifetime_threshold_figures.py
```

The manuscript was compiled with:

```bash
cd apjl_scalar_cloud_resonance
latexmk -pdf -interaction=nonstopmode -halt-on-error ms.tex
```

