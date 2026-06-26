# Variable dictionary — oligo nephrotoxicity dataset

Three blocks: **predictors** (oligo design + sequence-derived), **exposure
context**, **endpoints/label**, plus mandatory **provenance**. Designed so a
row can come from an in-vitro panel or a clinical drug and stay comparable.

## Table design (normalized, per-measurement grain)

Two joined tables so one in-vitro study (oligo × dose × model × readout) can
legitimately contribute many rows, while oligo design is stored once:

- **`data/oligos.csv`** — one row per unique oligo (block A predictors). PK `oligo_id`.
- **`data/measurements.csv`** — one row per measurement (blocks C + D + E).
  FK `oligo_id` → oligos. **This is the table that scales to ≥100 records.**

Sequence-derived features (block B) are computed from `oligos.csv` into a
derived file later; they are not hand-entered.

## A. Oligo design (predictors)

| Field | Type | Notes |
|-------|------|-------|
| `drug_name` / `oligo_id` | str | Stable identifier. |
| `oligo_class` | enum | `gapmer_ASO`, `siRNA`, `GalNAc_siRNA`, `splice_switch_ASO`, `PMO`, `aptamer`, `other`. |
| `target` | str | Gene / molecular target. |
| `length_nt` | int | For duplex siRNA, guide-strand length. |
| `sequence_5to3` | str | 5′→3′. **Extract from authoritative source — never guess.** |
| `backbone_chemistry` | str | PS vs PO content/pattern; stereochemistry if known. |
| `sugar_mods` | str | 2′-MOE, 2′-OMe, cEt, LNA, 2′-F, morpholino, DNA. |
| `gapmer_design` | str | e.g. `5-10-5`; blank if N/A. |
| `conjugation` | enum | `GalNAc`, `lipid_LNP`, `PEG`, `none`. |

## B. Sequence-derived features (computed)

| Field | Notes |
|-------|-------|
| `cpg_count`, `cpg_motifs` | TLR9 / innate-immune risk. |
| `gc_pct` | |
| `predicted_tm` | Hybridization affinity (gapmer toxicity link). |
| `offtarget_count` | Genome-wide near-complement hits. |
| `toxic_motif_flags` | Known hepatotoxic/nephrotoxic motifs. |

## C. Exposure context (in-vitro rows)

| Field | Notes |
|-------|-------|
| `model_system` | `ciPTEC`, `RPTEC/TERT1`, `HK-2`, `primary_PTEC`, `kidney_organoid`, `in_vivo_animal`, `clinical`. |
| `delivery` | **`gymnotic_free_uptake` vs `transfection`** — required; not comparable across modes. |
| `concentration`, `conc_units` | Capture full dose-response when available. |
| `exposure_h` | Duration. |
| `donor_id`, `passage`, `n_replicates` | Reproducibility. |

## D. Endpoint & graded label

Heterogeneous sources → keep the **raw readout** AND a harmonized **graded
label**. Do not collapse to binary too early.

| Field | Notes |
|-------|-------|
| `nephrotox_grade` | `0` none · `1` functional-reversible (LMW proteinuria, reabsorption inhibition) · `2` tubular injury (KIM-1/NGAL↑, histopath) · `3` clinical AKI / glomerulonephritis. |
| `endpoint_raw` | Free text: actual measured readout + value. |
| `endpoint_units` | |
| `readout_type` | `viability`, `protein_reabsorption`, `injury_biomarker`, `histopath`, `clinical_outcome`, `transcriptomic`. |

Endpoint readouts to prioritize (oligo nephrotox is often functional, not
cytotoxic): receptor-mediated reabsorption (albumin / A1M / RAP uptake),
KIM-1, NGAL, clusterin, cystatin C, lysosomal load, mitochondrial function,
innate-immune cytokines / complement — alongside ATP/LDH viability.

## E. Provenance (mandatory — NCATS scores transparency)

| Field | Notes |
|-------|-------|
| `evidence_source` | `in_vitro_human`, `in_vitro_animal`, `in_vivo_animal`, `clinical`. |
| `evidence_confidence` | `high` / `medium` / `low`. |
| `source_ref`, `source_doi` | Citation. |
| `source_table` | Which figure/table the value came from. |
| `extraction_method` | `manual`, `OCR`, `author_data`. |
| `redistribution_ok` | Can the raw value be republished? If no, store derived features only. |
| `curator`, `curation_date`, `curation_notes` | |
