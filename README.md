# rareUTRvariants-gnomAD-annotation Pipeline

An end-to-end bioinformatics pipeline for processing and annotating rare UTR variants derived from Whole Genome Sequencing (WGS) data. This workflow handles coordinate transformation (hg19 to hg38), VCF normalization, population frequency annotation via gnomAD, and prioritized filtering.

---

## Workflow Overview

This pipeline integrates clinical WGS data with large-scale population genomic databases. It is designed for researchers seeking to identify rare and potentially pathogenic variants in 3' and 5' Untranslated Regions (UTRs).

### Key Features:
- **Automation:** Streamlined processing from raw Excel lists to annotated candidate variants.
- **Precision:** Uses `bcftools` for VCF normalization to ensure high-accuracy matching against gnomAD.
- **LiftOver:** Seamless conversion of legacy hg19 coordinates to the hg38 reference genome.
- **Prioritization:** Automated categorization of variants into "Ultra-Rare" and "gnomAD-Absent" tiers.

---

## Pipeline Stages

1. **Data Integration:** Merging multiple WGS datasets (`WGS140`, `WGS240`, `WGS335`).
2. **Coordinate Conversion:** UCSC LiftOver from hg19 to hg38.
3. **VCF Construction:** Creation of standardized VCF files including anchor-base recovery for indels.
4. **Normalization:** Left-alignment and parsimony normalization via `bcftools`.
5. **gnomAD Querying:** Automated API-less local VCF querying for population frequencies (AF, AC, AN, NFE-specific metrics).
6. **Annotation:** Linking multi-patient recurrence data with population frequencies.
7. **Filtering:** Tier-based prioritization of candidate variants.

---

## Required Input Files

To run the pipeline, ensure the following files are in your project directory:

- **Source Data:** `WGS140.xlsx`, `WGS240.xlsx`, `WGS335.xlsx`.
- **References:** `hg19ToHg38.over.chain`, `hg38.fa` (with `.fai` index).
- **Population Data:** gnomAD v3.1.2 genome VCF files (split by chromosome).

---

## Filtering Strategy

The pipeline automatically categorizes variants into two high-priority lists:

- **Tier 1 (Recurrent Ultra-Rare):** Variants with `AF_nfe < 0.001` observed in 2 or 3 distinct patients in the cohort.
- **Tier 2 (Novel candidates):** Variants completely absent from the gnomAD database.

---

## Software Requirements

- **R Environment:** `dplyr`, `purrr`, `readxl`, `writexl`, `Biostrings`.
- **Bioinformatics Tools:** `bcftools`, `tabix`, `bgzip`, `liftOver`.

---

## Usage

1. Open `Full_rareUTRvariants_Pipeline_TR_revised_EN.Rmd` in RStudio.
2. Ensure the working directory contains the `data/` and `reference/` folders.
3. Run the chunks sequentially or use the "Knit" button to generate a full technical report.

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## Author

**[Dr. Kursat Oguz YAYKASLI, PhD]**  
