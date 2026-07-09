# Mutation timing, accumulation and selection in the male germline shape inheritance risk for developmental disorders

Code accompanying:

Neville MDC, Neuser S, Sanghvi R, Christopher J, Roberts K, Smith K, O'Neill L, Hayes J, Cagan A, Hurles ME, Goriely A, Abou Jamra R, Rahbari R. *Mutation timing, accumulation and selection in the male germline shape inheritance risk for developmental disorders.* Cell Genomics (in press).

Corresponding authors: Matthew D. C. Neville (mn7@sanger.ac.uk), Raheleh Rahbari (rr11@sanger.ac.uk)

## Contents

- **`DDfathers_figures.Rmd`** — generates all main and supplementary figures from the files in `data/`. This is the entry point for reproducing the paper's figures.
- **`DDfathers_figures.html`** — a knitted copy of the above, so the code and its output (figures, printed stats) can be browsed directly without running anything.
- **`DDfathers_processing.Rmd`** — documents the upstream NanoSeq/HPC processing pipeline (read mapping, variant calling, QC filtering, VEP annotation, dN/dS setup) that produces the inputs used by `DDfathers_figures.Rmd`. This file would require accessing raw EGA sequencing data and adaption of computationally intensive bash/HPC job scripts to your local environment to run.
- **`data/`** — small, processed input files required to run `DDfathers_figures.Rmd` (sample metadata, variant tables, burden/VAF summaries, the combined supplementary tables workbook).
- **`output/`** — figures (PDF) are written here when `DDfathers_figures.Rmd` is run. Not included in the repository; created automatically on first run.

## Running the figures code

Open `DDfathers_figures.Rmd` in RStudio and knit, or run interactively. It reads all inputs from `data/` (relative paths) and writes all figures as PDF to `output/`.

Required R packages: tidyverse, readxl, patchwork, ggpubr, ggrepel, scales, grid, png.

## A note on TwinsUK control data

Several figures compare the DD-father sperm cohort in this study to sperm samples from TwinsUK volunteers (Neville et al., 2025, https://doi.org/10.1038/s41586-025-09448-3). TwinsUK individual-level genotype and phenotype data are not permitted to be publicly shared or deposited due to the original consent given at the time of data collection, and access is subject to governance oversight. All data access requests are overseen by the TwinsUK Resource Executive Committee (TREC). For information on access to these data and how to apply, see https://twinsuk.ac.uk/resources-for-researchers/access-our-data/.

`DDfathers_figures.Rmd` runs in one of two modes, decided automatically by whether the restricted-access TwinsUK files are present in `data/`:

- **With TwinsUK access**: if you have been granted access and have placed the individual-level TwinsUK files in `data/` (their filenames appear throughout the notebook wherever `dataPath` is read inside an `if (twinsUKDataAvailable)` block, e.g. `tukGermanPanelVafSums.tsv`, `twinsUK_burdensFiltered_targ.tsv`, `twinsUK_analysisTargVars.tsv`), the figures are reproduced exactly as published, including the TwinsUK comparison points. The presence of `data/tukGermanPanelVafSums.tsv` specifically is what the notebook checks to decide which mode to run in.
- **Without TwinsUK access (default for this repository)**: DD-father (and Apert-father) data is plotted directly, and the TwinsUK trend line/bar is drawn from a small set of pre-computed aggregate summaries also included in `data/` (`twinsUK_*Fits.tsv`, `twinsUK_cohortFraction.tsv`, `twinsUK_exomePanelCorrection_stats.tsv`). These contain only fitted values, confidence intervals, and reported statistics (an Age grid, or a handful of proportions/counts summed across the whole TwinsUK cohort) — never individual TwinsUK data points. The code and comments in `DDfathers_processing.Rmd` (section "TwinsUK model fits") show exactly how these summaries were derived from the restricted-access data.

## Raw sequencing data

Sperm NanoSeq sequencing data have been deposited at the European Genome-Phenome Archive as [EGAD00001016416](https://ega-archive.org/datasets/EGAD00001016416) and are publicly available as of the date of publication.

Whole genome sequencing data have been deposited at the European Genome-Phenome Archive as [EGAD00001016417](https://ega-archive.org/datasets/EGAD00001016417) and are publicly available as of the date of publication.

## License

See [LICENSE](LICENSE).

Exception: data/GraphicFig1a.png and data/GraphicFig4a_purple.png are schematic illustrations created with BioRender.com and are excluded from the repository's MIT license. They remain © BioRender and are included here solely so that DDfathers_figures.Rmd can reproduce the published figure panels - they are not licensed for reuse, modification, or redistribution.
