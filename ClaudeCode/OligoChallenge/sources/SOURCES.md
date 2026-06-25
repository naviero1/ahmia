# Source manifest — what to fetch to reach ≥100 records

I (Claude) **cannot download these** through this environment (network policy blocks
publishers/USPTO/PMC). **Workflow:** drop the supplementary file (Excel/CSV preferred,
PDF ok) into this `sources/` folder using the suggested filename, and I'll extract and
harmonize each into the dataset against `schema.md`.

Legend — **Open?**: `OA` open access / public domain (easy), `PW` paywalled (may need
institutional access), `?` unverified.

## Tier N — Kidney-specific (priority; keeps dataset nephrotox-focused)

| # | Source | What it yields | Open? | Drop as |
|---|--------|----------------|-------|---------|
| N1 | Moisan/Dieckmann et al., *A Sensitive In Vitro Approach to Assess the Hybridization-Dependent Toxic Potential of High Affinity Gapmer Oligonucleotides*, Mol Ther Nucleic Acids 2017/18 (DOI 10.1016/j.omtn.2017.11.004) | Panel of gapmers + tox readouts; dose-response → many rows | OA | `N1_dieckmann_mtna2018_suppl.xlsx` |
| N2 | Drisapersen ciPTEC study, Mol Ther Nucleic Acids 2019 (PMC6796739) | Albumin/A1M/RAP reabsorption dose-response in human PTEC | OA | `N2_ciptec_drisapersen_mtna2019_suppl.xlsx` |
| N3 | US Patent 11,105,794 B2 — *In vitro nephrotoxicity screening assay* (EGFR/EGF biomarker, PTEC) | Tables of ASOs tested for nephrotox readouts | OA (public domain) | `N3_patent_US11105794.pdf` |
| N4 | US Patent 11,479,818 B2 — same family | More nephrotox-screened oligos | OA | `N4_patent_US11479818.pdf` |
| N5 | US Patent 10,955,407 B2 — *In vitro toxicity screening assay* | Related screened oligos | OA | `N5_patent_US10955407.pdf` |
| N6 | Frazier KS, *Comparative Renal Toxicopathology of Antisense Oligonucleotides* (Toxicol Pathol) | Many ASOs w/ in-vivo renal histopath findings | PW? | `N6_frazier_renal_toxpath_suppl.pdf` |
| N7 | *Nephrotoxicity of marketed antisense oligonucleotide drugs*, Curr Opin Toxicol 2022 (S2468202022000560) | Drug-level renal outcomes table (anchors) | PW? | `N7_nephrotox_review_2022.pdf` |

## Tier H — Large hepatotox/general panels (ONLY if we broaden scope; big N)

| # | Source | What it yields | Open? | Drop as |
|---|--------|----------------|-------|---------|
| H1 | Hagedorn et al., gapmer hepatotox ML dataset (Nucleic Acid Ther ~2018) | Hundreds of sequences + hepatotox class | PW? | `H1_hagedorn_suppl.xlsx` |
| H2 | Burdick et al., Nucleic Acids Res 2014;42:4882 | Sequence motif → tox | PW? | `H2_burdick_nar2014_suppl.xlsx` |
| H3 | Kasuya et al., Sci Rep 2016;6:30377 (PMC4961955) | LNA-gapmer hepatotox panel | OA | `H3_kasuya_scirep2016_suppl.xlsx` |
| H4 | Yoshida/Kasuya 2022 (PMC9303313) — nucleobase mods reduce hepatotox | Gapmer panel + ALT/viability | OA | `H4_kasuya_2022_suppl.xlsx` |
| H5 | Bhamra et al. (Creyon Bio) 2025, ChemRxiv 10.26434/chemrxiv-2025-d2bhr / ChemBioChem 10.1002/cbic.202500584 | Possibly the largest open seq+chem+tox set — check for released data | ? | `H5_creyon_2025_dataset.*` |

## Notes
- Prefer **machine-readable** supplementary (xlsx/csv). If only a PDF table exists, drop the PDF — I'll transcribe and flag `extraction_method=OCR`.
- For each source confirm **redistribution rights**; patents are public domain (safe to republish), journal supplementary often is not (we may store derived features only — see README caveat).
- Citations above with `?`/`~` need their exact DOI/volume verified at extraction time.
