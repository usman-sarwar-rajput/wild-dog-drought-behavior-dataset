# African Wild Dog: open drought behavior dataset and analysis

Species-specific secondary-analysis release, prepared 22 November 2026. This is a curated subset/derivative of existing open research, **not a newly collected dataset or a validated disaster-warning system**. Original researchers retain credit for field data. The manuscripts are exploratory and not peer reviewed.

## Dataset at a glance

| Property | Value |
|---|---|
| Animals in source subset | 22 |
| Analytical units | 18 |
| Source rows | 138 |
| Analysis rows | 136 |
| Dates | 2011-12-01 to 2022-04-01 |
| Outcome | 95% Brownian-bridge home-range area (km²) |
| Exposure | three-month SPI |
| Complete five-stage animal sequences | 0 |

## Download and contents

- [Analysis-ready CSV](data/analysis_data.csv) and [data dictionary](DATA_DICTIONARY.md).
- [Source records](source/source_records.csv), [provenance and checksums](source/PROVENANCE.json).
- `analysis/`: statistical contrasts and coefficients, validation splits, held-out predictions, model metrics, metadata and the exploratory saved forest.
- `scripts/`: source preprocessing, independent species reanalysis and validation.
- [Professional PDF manuscript](paper/wild_dog_professional_manuscript.pdf), [editable Word manuscript](paper/wild_dog_professional_manuscript.docx), and scientific figures in `paper/figures/`.
- `CHECKSUMS.json`: integrity hashes for all release files except this hash manifest itself.

## Original sources and credit

Original investigators: **West, Rafiq, Converse, Wilson, Jordan, Golabek, McNutt and Abrahms**. [Dataset DOI](https://doi.org/10.5061/dryad.k98sf7mgm); [related journal paper](https://doi.org/10.1111/1365-2656.14192).

Actual input source: https://github.com/Abrahms-Lab/CarnivoreSpaceUse-Droughts

The source is the author GitHub version at commit 4ad426c48d557393cdb60f4baa3fd0c4850f7a05. It is not byte-identical to the Dryad release. Only this species and the BB95 isopleth are retained. Pack/pride-month duplicates are averaged before modeling.

## Reproduce and verify

Use a compatible Python environment and the recorded dependency versions:

```bash
python -m pip install -r requirements.txt
python scripts/validate.py
python scripts/reproduce.py
python scripts/validate.py
```

Run from the repository root. Reanalysis writes to ignored `reproduced/`, preserving the published data and results. Validation checks source-to-analysis preprocessing, release hashes, saved prediction metrics, validation splits and, when regenerated outputs exist, agreement with published results. Loading the optional joblib artifact is unnecessary for reanalysis; only load serialized models from trusted sources with compatible library versions.

The primary statistical model uses log outcomes, unit effects and, for monthly data, calendar month and year effects. Daily herbivore contrasts compare CD/HD/HW and cannot distinguish season from drought. Monthly uncertainty includes unit/year clustering sensitivity. The original multiplicity family contains 11 primary contrasts across seven species: `analysis/multiplicity_family.csv` retains those summary p-values so separate reruns preserve the original adjustment. It does not contain other species observation data.

AI comparisons use a mean baseline, seasonal ridge and random forests, with an additional contemporaneous drought-index forest for monthly data. Group-held-out and forward-time validation are reported separately. The saved full-data forest is not evidence of out-of-sample performance; use the held-out predictions and scores.

## Five stages and limitations

Requested stages are baseline, near-before, during drought, early-after and late environmental normalization. Stages are assigned only where the observation and index rules support them. Late environmental normalization does not establish behavioral recovery.

Author GitHub version at commit 4ad426c48d557393cdb60f4baa3fd0c4850f7a05. All seven CSV hashes differed from Dryad; results apply to this GitHub version. Pack/pride-month duplicate rows averaged. Counts are available event-stage windows, not independent disasters. Late-normal is environmental only. The three-month index has 0 records at or below -1. Results cannot be transferred to the different Dryad version without reanalysis.

No drought causation, earthquake prediction, five-stage classification accuracy or operational early warning is established by these analyses. Full methodology, limitations and results are in the manuscript.

## License and citation

Source-data terms: **MIT (Abrahms-Lab)**. Original repository contributions: MIT. See [LICENSE](LICENSE) and [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for scope and retained notices. Cite the original dataset and paper above when using these records; identify this repository and its commit as the secondary processing version. No new DOI is claimed.

This repository is maintained under `usman-sarwar-rajput`. Repository maintenance is not a claim of authorship of the original field study.
