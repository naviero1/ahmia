# OligoTox — Nephrotoxicity Curated Dataset (Phase 2 entry)

Working space for an entry to the **NIH/NCATS Oligonucleotide Toxicity (OligoTox)
Open Data Challenge**, Phase 2 (Data Generation Phase, submission window
1 May – 31 Dec 2026). Endpoint focus: **kidney toxicity / nephrotoxicity**.
Approach: **curate an openly-releasable dataset** spanning all oligo classes
(ASO, siRNA, splice-switching/PMO, aptamer) from published in-vitro
proximal-tubule studies + clinical/regulatory renal-safety signals.

> ⚠️ This folder is intentionally separate from the surrounding Ahmia codebase,
> which is unrelated. If this advances toward a submission it should move to its
> own repository.

## Why curation needs an in-vitro backbone (not just drug labels)

There are only ~24 approved nucleic-acid drugs and a handful with clear renal
signals — too few rows, and almost no *within-chemistry sequence variation*,
which is the signal a sequence→toxicity model needs. So:

- **Backbone (high N):** per-sequence panels from the in-vitro screening
  literature (human proximal-tubule uptake/function assays, gapmer
  hybridization-tox panels). Mine the **supplementary tables**.
- **Anchors (high confidence, low N):** marketed/late-clinical oligos with
  documented clinical renal outcomes. This is what `data/seed_inventory.csv` is.

## Files

| File | Purpose |
|------|---------|
| `schema.md` | Variable dictionary + two-table design. |
| `data/oligos.csv` | Oligo dictionary — one row per unique oligo (design predictors). PK `oligo_id`. |
| `data/measurements.csv` | Measurement fact table — one row per oligo×model×dose×readout. **Scales to ≥100.** |
| `sources/SOURCES.md` | Prioritized fetch list; drop supplementary files in `sources/` for extraction. |

## Record count (target ≥100)

Scope = **strict kidney, per-measurement grain**. Current = **22** measurements
(clinical/animal anchors only). Remaining ~78+ come from kidney in-vitro
supplementary tables (see `sources/SOURCES.md`, Tier N) once dropped into `sources/`.

## Status & honest caveats

- **Preliminary.** Every `nephrotox_grade` and field in the seed inventory is a
  curation judgment that must be verified against the cited primary source
  before any release. `sequence_5to3` is deliberately left `TBD` rather than
  guessed — to be extracted from authoritative references (NAR 2023; FDA/EMA labels).
- **Class imbalance:** most rows are "no reported renal signal"; true positives
  cluster in PS-gapmer ASOs. siRNA/aptamer renal data is thin → "broad class"
  is ASO-heavy. State this coverage limit in any submission.
- **Confounder:** in-vitro free-uptake (gymnotic) vs transfection is not
  comparable across studies — it is a required column in `schema.md`.
- **Redistribution:** the deliverable must be openly releasable. Flag any source
  we cannot legally republish and store only derived features for those.

## Next steps

1. Drop kidney source files (Tier N in `sources/SOURCES.md`) into `sources/`.
2. I extract each into per-measurement rows → grow `measurements.csv` past 100.
3. Verify anchors against primary sources; fill `sequence_5to3` in `oligos.csv`.
4. Compute sequence-derived features (block B) into a derived file.
