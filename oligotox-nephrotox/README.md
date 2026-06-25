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
| `schema.md` | Variable dictionary: predictors, exposure context, graded label, provenance. |
| `data/seed_inventory.csv` | Tier-2 anchor set: approved + late-clinical oligos joined to known renal signals + sources. |

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

1. Verify seed-inventory anchors against primary sources; fill `sequence_5to3`.
2. Mine Tier-1 in-vitro supplementary tables to grow N (the modeling backbone).
3. Add FAERS renal-AE disproportionality as a supporting clinical signal.
