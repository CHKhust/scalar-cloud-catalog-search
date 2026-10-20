# Constraints on phenomenological modifications to compact binary gravitational waveforms

Analysis code, saved numerical results, figures, and manuscript source for the study by Hao-Kang Chen, Pan-Pan Wang, and Cheng-Gang Shao.

## Download

**[Download the analysis package from the NEW release](https://github.com/CHKhust/scalar-cloud-catalog-search/releases/tag/NEW)**

Open the release page, expand **Assets**, and download the uploaded analysis ZIP. Extract the archive and open its `scalar-cloud-catalog-search` directory. All paths and commands below refer to that extracted directory.

The uploaded analysis package contains the numerical data. GitHub's automatically generated **Source code** archives correspond to the tagged repository tree. The earlier catalog ZIP retained on the repository homepage is a historical version.

## Included material

| Directory or file | Contents |
| --- | --- |
| `manuscript/` | Manuscript TeX source, bibliography, abstract, and figure assets |
| `release/scalar_cloud_PRD.pdf` | Compiled manuscript |
| `data/` | Saved nested samples, original weights, run metadata, conditional mass arrays, prior samples, and plotting inputs |
| `code/` | Analysis code and scripts for checking and reproducing saved results |
| `code/frozen_reference/` | Original Bilby inference code and configuration |
| `code/frozen_mapping/` | Conditional superradiant-saturation mass transformation |
| `tools/` | File verification and manuscript build helpers |
| `docs/` | Data dictionary, reproduction instructions, and historical-material index |
| `audit/` | File identities and verification records |
| `MANIFEST.json` | File sizes and SHA256 checksums |

The ten saved analyses contain 410931 weighted samples in total. Each analysis includes 56 sampled parameters, including 40 detector calibration parameters. The package contains four analyses of GW230518_125908 and three recoveries of each of two injected signals. Repeated injection analyses use independent sampler seeds with the same noise realization within each signal set.

Four conditional boson rest-energy distributions and two independently generated prior sample sets are included. The mass transformation uses the superradiant-saturation history and induced prior specified in Appendix D.1 of the manuscript. Results from individual analyses retain their original weights and are reported separately.

## Verify and reproduce the saved results

Use a Python environment compatible with `requirements.txt`. From the extracted package directory:

```bash
python -m pip install -r requirements.txt
python -B tools/verify_repository.py
python -B code/reproduce_saved_results.py --out build/recomputed
python -B code/check_injection_truth.py --out build/injection_truth.json
```

Use a new output directory or file for each command with `--out`. These commands check and process the archived samples and weights. The original inference environment, data identities, and sampling settings are recorded in the preserved run metadata.

Figure reproduction commands and font requirements are given in `docs/REPRODUCTION.md`. The original public strain and posterior inputs are identified in the manuscript and acquired separately.

## Build the manuscript

An existing TeX Live or MiKTeX installation with REVTeX 4.2, pdfLaTeX, and BibTeX is required.

```bash
python -B tools/build_manuscript.py --out build/paper
```

If the TeX executables are outside the system PATH, supply their directory with `--tex-bin`. Use a new output directory for each build.

## Historical material

The earlier catalog and diagnostic calculations are indexed in `docs/HISTORICAL_COMPANION.json`. The historical companion archive is a separate distribution file. Its expected filename, size, and SHA256 checksum are recorded in that index.

## Citation

```bibtex
@misc{Chen2026ScalarCloudCode,
  author = {Chen, Hao-Kang and Wang, Pan-Pan and Shao, Cheng-Gang},
  title = {{Scalar-cloud catalog search: Analysis scripts and derived products}},
  howpublished = {GitHub repository},
  year = {2026},
  url = {https://github.com/CHKhust/scalar-cloud-catalog-search}
}
```

## License and attribution

See `LICENSE_NOTICE.md` in the analysis package for licensing information and third-party attribution.
