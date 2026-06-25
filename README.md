# Scalar-cloud tidal-resonance catalog search

This repository contains the analysis code, manuscript source, figures, and derived
tables used for the scalar-cloud tidal-resonance catalog search.  It is organized
as a reproducibility package for the paper rather than as a general-purpose
software library.

## Contents

- `src/` contains the Python and shell scripts used for catalog selection,
  posterior reweighting, cloud-history postprocessing, injection checks, and
  figure generation.
- `campaigns/` contains the Slurm campaign scripts used on the cluster for the
  high-resolution and validation runs.
- `data/derived/` contains the postprocessed CSV and JSON products used in the
  manuscript figures and numerical statements.
- `figures/` contains the EPS, PDF, and PNG figure files used by the manuscript.
- `manuscript/` contains the PRD manuscript source, bibliography, compiled PDF,
  and cover letter.
- `docs/` contains a data manifest and a code/data audit.

The raw public LVK strain and posterior files are not included because they are
large public data products.  They can be downloaded from GWOSC and Zenodo with
the manifest/download scripts in `src/`.

## Python environment

The plotting and postprocessing scripts require Python 3.10 or newer and the
packages listed in `requirements.txt`.

The full catalog scans also require an LVK/LAL environment with `lalsimulation`
and access to the public strain and posterior files.  The cluster jobs were run
in a conda environment named `ligo-lal`.

## Reproducing the manuscript figures from included derived data

From the repository root:

```bash
python src/make_apjl_fig1_mechanism.py
python src/make_apjl_fig2_catalog_summary.py
python src/make_prd_fig3_final_intervals.py
python src/make_eps_lifetime_threshold_figures.py
```

These commands read only `data/derived/` and write updated files to `figures/`.
They do not download LVK data or rerun the expensive posterior reweighting scans.

## Rebuilding the manuscript

From the repository root:

```bash
cd manuscript
latexmk -pdf -interaction=nonstopmode -halt-on-error scalar_cloud_PRD_work.tex
```

The manuscript directory already includes the bibliography and the PRD PDF used
at packaging time.

## Rerunning the scan campaigns

The Slurm scripts in `campaigns/` are included for provenance.  They assume a
cluster layout close to

```bash
export LIGO_DATA_ROOT=$HOME/LIGO_data_upload
export ROOT=$HOME/scalar_cloud_ligo
```

Change these paths before running on another system.  The public data download
helpers are:

```bash
python src/build_reweight_target_manifest.py
python src/download_reweight_target_data.py --help
python src/prefetch_hpc_ligo_data.py --help
```

The `src/make_*campaign*.py` helpers generate cluster submission directories
from the corresponding derived tables.  They are included to document how the
long scans were launched, but they are not required for reproducing the
manuscript figures from the packaged data.

## Main derived products used by the paper

- Formal saturated-cloud result:
  no threshold crossing remains that can be interpreted as a saturated cloud
  constraint after the \(\ln\Lambda_{\rm prof}\le3\) likelihood requirement.
- Likelihood-thresholded saturated-cloud diagnostic:
  `data/derived/analysis_outputs/singlepoint_refine_nmu301/final_threshold_saturated_cloud_crossings_322_Amax0p7_logB3.csv`
- Refined threshold diagnostic source table:
  `data/derived/analysis_outputs/singlepoint_refine_nmu301/intervals_322_Amax0p7_logB3/cloud_exclusion_intervals_by_source.csv`
- Large-amplitude no-logB products, if present, are deprecated diagnostic
  stress-test products.  They are not used in any published figure, table,
  retained direct limit, or saturated-cloud threshold diagnostic.  They are
  kept only to document the superseded workflow and are stored under
  `data/derived/diagnostics/large_amplitude_no_logB_cut_diagnostic_only/`.
- Superseded saturated-cloud interval products from the older no-veto workflow
  are stored under
  `data/derived/diagnostics/legacy_superseded_outputs/` and are not manuscript
  inputs.
- Injection sanity summary:
  `data/derived/analysis_outputs/injection_exact_sanity_20260620_150845/injection_exact_sanity_results/coverage_by_amplitude.csv`
- Lifetime-threshold comparison:
  `data/derived/analysis_outputs/eps5_eps15_catalog/eps15_eps5_survival_threshold_counts.csv`

See `docs/DATA_MANIFEST.md` and `docs/CODE_AUDIT.md` for the file-level summary
and audit notes.
