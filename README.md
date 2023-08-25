# PRECISE-1K

This repository contains data and code necessary for assembling the PRECISE-1K _E. coli_ K-12 MG1655 expression and transcriptional regulation knowledgebase, including computing and analyzing iModulons, analyzing expression patterns, and generating all figures for the associated [publication](https://www.biorxiv.org/content/10.1101/2021.04.08.439047v2).

This repository also includes data, assembly, iModulon computation, and analysis for the larger, 2710-sample "Public K-12" RNA-seq resource.

To analyze new data with the PRECISE-1K knowledgebase, we recommend starting with the lightweight [precise1k-analyze repository](https://github.com/SBRG/precise1k-analyze).

For an overview of iModulons, we recommend [iModulonDB's About Page](https://imodulondb.org/about.html).

[![DOI](https://zenodo.org/badge/533906640.svg)](https://zenodo.org/badge/latestdoi/533906640)

## Setup

Ensure you have Python 3.6+, Jupyter (`pip install jupyterlab`), and the iModulon analysis package `pymodulon` installed (`pip install pymodulon`). 

`pymodulon` documentation can be found [here](https://pymodulon.readthedocs.io/en/latest/index.html).

Installing `pymodulon` using `pip` will install all other needed packages.

Then, clone this repository onto your local machine by executing the following command in your command prompt/terminal: `git clone https://github.com/SBRG/precise1k.git`. This command will copy this repository to a folder called `precise1k` in the directory from which the command was executed. This repository contains many data files, so cloning may take a few minutes.

## Overview

The repository is split into 2 subdirectories: `data` and `notebooks`. All analyses are presented in the form of Jupyter notebooks in the `notebooks` subdirectory, utilizing data from the `data` directory.

## Data

The `data` directory contains further subdirectories with the following constituent files:

- `annotation`: contains gene and regulatory network annotations for K-12 MG1655
   - `gene_info.csv`: a table of gene metadata for K-12 MG1655, assembled primarily from NCBI RefSeq NC_000913.3 and the E. coli K-12 MG1655 [Bitome](https://academic.oup.com/nar/article/48/18/10157/5911745)
   - `TRN.csv`: a table containing regulatory annotations (i.e. regulator->gene links), assembled primarily from [RegulonDB](https://regulondb.ccg.unam.mx/) and [EcoCyc](https://www.ecocyc.org/)
- `k12_modulome`: contains sample metadata, QC statistics, iModulon M and A matrices, and iModulon metadata for the "Public K-12" dataset, which consists of PRECISE-1K (1035 samples) combined with 1,675 high-quality publicly available samples
   - `A.csv`: the iModulon A (activity) natrix computed for the Public K-12 dataset
   - `Escherichia_coli_20220127.tsv`: raw metadata for publicly-available E. coli RNA-seq data downloaded from SRA on 1/27/2022 using the [modulome workflow](https://github.com/avsastry/modulome-workflow/tree/main/1_download_metadata)
   - `K12_metadata.tsv`: curated public sample metadata for RNA-seq samples identified as coming from E. coli strain K-12
   - `M.csv`: the iModulon M (modulon) matrix computed for the Public K-12 dataset
   - `bioproject_list.csv`: the raw list of unique BioProjects from `Escherichia_coli_20220127.tsv`
   - `bioproject_list_curated.csv`: a manually curated set of BioProjects from `bioproject_list.csv`
   - `component_stats.csv`: raw statistics for the Public K-12 iModulons
   - `counts.csv`: the raw read counts computed from the raw public read data in `K12_metadata.tsv` using the [modulome RNA-seq processing workflow](https://github.com/avsastry/modulome-workflow/tree/main/2_process_data)
   - `imodulon_table.csv`: the iModulon metadata table, containing iModulon regulatory enrichment statistics, functional categorizations, and other metadata
   - `k12_modulome.json.gz`: the `IcaData` object for the Public K-12 dataset, containing the `imodulon_table`, `M`, and `A` matrices - for use with `pymodulon`
   - `k12_only_p1k_ctrl.json.gz` and `k12_only_proj_reg.json.gz`: `IcaData` objects for iModulons computed using _just_ the publicly available data (i.e. without appending it to PRECISE-1K)
   - `metadata_qc.csv`: the final, curated sample metadata for the Public K-12 dataset, _without_ PRECISE-1K metadata
   - `metadata_qc_blah`: intermediate metadata files containing samples that were excluded during various QC steps (see [Public K-12 QC notebook Pt 1](https://github.com/SBRG/precise1k/blob/master/notebooks/k12_modulome/1a__QC_expression_part1.ipynb) and [Public K-12 QC notebook Pt 2](https://github.com/SBRG/precise1k/blob/master/notebooks/k12_modulome/1b__QC_expression_part2.ipynb)
   - `multiqc_stats.tsv`: raw QC statistics for the publicly-available samples
   - NOTE: `log_tpm` files for the public dataset are not provided as they are too large for GitHub - please contact us for these.
- `precise`: contains iModulon files from the [original PRECISE publication](https://www.nature.com/articles/s41467-019-13483-w) (also available at [iModulonDB's PRECISE-278 page](https://imodulondb.org/dataset.html?organism=e_coli&dataset=precise1))
   - `A.csv`: iModulon A (activity) matrix
   - `M.csv`: iModulon M (modulon) matrix
   - `M_thresholds.csv`: thresholds for determining iModulon gene membership from `M`
   - `iM_table.csv`/`imodulon_table.csv`: iModulon metadata, including regulatory enrichments
   - `log_tpm.csv`: log2[TPM] data (i.e. PRECISE itself)
   - `log_tpm_norm.csv`: log2[TPM] data, centered to the control condition (M9 glucose) - also known as the `X` matrix, or the direct input to the ICA pipeline
   - `metadata_qc.csv`: curated sample information for PRECISE - slightly modified from `sample_table.csv`
   - `precise.json.gz`: an `IcaData` object containing PRECISE and its iModulon information, for use with `pymodulon`
   - `sample_table.csv`: metadata as downloaded from iModulonDB
- `precise1k`: expression and iModulon data for the core expression compendium in this resource, PRECISE-1K
   - `multiqc_data`: raw QC statistics for PRECISE-1K samples
   - `subsamples`: sample IDs for random subsamples generated from PRECISE-1K for a specific analysis
   - `A.csv`: the iModulon A matrix for PRECISE-1K
   - `M.csv`: the iModulon M matrix
   - `component_stats.csv`: raw statistics for the PRECISE-1K imodulons
   - `counts.csv`: the raw read count data from which log2[TPM] data was computed; output of [modulome workflow](https://github.com/avsastry/modulome-workflow/tree/main/2_process_data)
   - `crp_binding.csv`: data from a simulated binding curve for CRP analysis (see manuscript Figure 4)
   - `deg_dima_result.csv`: results from comparing differential iModulon activity (DiMA) analysis to differential gene expression (DGE) analysis
   - `imodulon_table.csv`: metadata for PRECISE-1K iModulons, including regulatory enrichment statistics and functional categorizations
   - `log_tpm.csv`: the log2[TPM] data, BEFORE quality control (1055 samples)
   - `log_tpm_norm_qc.csv`: log2[TPM] data, centered to the reference condition (M9 glucose), after QC - aka `X` matrix, direct input to ICA
   - `log_tpm_qc.csv`: the quality-controlled log2[TPM] data, aka PRECISE-1K itself (1035 samples)
   - `log_tpm_qc_w_short_low_fpkm.csv`: log2[TPM] data before removal of ~100 short and very low read count genes
   - `metadata.csv`: metadata for PRECISE-1K samples BEFORE quality control (1055 samples)
   - `metadata_qc.csv`: post-QC sample metadata for PRECISE-1K (1035 samples)
   - `multiqc_stats.tsv`: summary of QC statistics for raw read data from `multiqc_data` subdirectory
   - `precise1k.json.gz`: `IcaData` object containing iModulon matrices, iModulon and sample metadata, etc. - for use with `pymodulon`
- `regulation`: contains raw files used to generate the TRN used for regulatory enrichment analysis
- `sequence_files`: contains the reference genome sequences used for alignment of raw reads in modulome processing workflow

## Notebooks (Analyses)

The `notebooks` directory contains analyses, split between the `k12_modulome` and `precise1k` datasets. The PRECISE-1K analysis notebooks are described below (Public K-12 analyses are very similar):

- `blah_figs`: contains figure panel files used to generate paper figures; has corresponding `blah.ipynb` notebook
- `1__QC_expression.ipynb`: notebook for visualizing QC statistics and excluding non-high-quality data after raw read processing
- `1b__differential_gene_expression_R.ipynb`: an R notebook for running traditional DGE
- `2__choose_dimensionality.ipynb`: final step of OptICA dimensionality selection method to determine final `M` and `A` matrices
- `3__create_ica_data.ipynb`: compiles final `M` and `A` matrices, sample metadata, TRN, gene information into `pymodulon`-ready `IcaData` object, as well as computing iModulon thresholds to determine iModulon membership, and computing regulatory enrichment statistics
- `4__annotate_imodulons.ipynb`: manual annotation and curation of iModulons
- `fig__characterize_ytfs.ipynb`: analysis of putative regulons YmfT and YgeV (Figure 3 in manuscript)
- `fig__investigate_activities.ipynb`: DiMA analysis, activity clustering (stimulons), CRP regulon segmentation
- `fig__investigate_expression.ipynb`: analyses of PRECISE-1K itself, i.e. the log2[TPM] expression data (Figure 1)
- `fig__subsamples.ipynb`: analysis of PRECISE-1K subsample iModulon sets (subsample `IcaData` objects not included due to GitHub size limitations, request if needed)
- `fig__summarize_dataset.ipynb`: overview of sample conditions in PRECISE-1K
- `fig__summarize_imodulons.ipynb`: overview of iModulon categories, enrichments, and regulatory coverage (Figure 2)
- `generate_p1k_subsamples.ipynb`: for generation of PRECISE-1K subsamples analyzed in `fig__subsamples.ipynb`
- `workflow__add_new_data.ipynb`: new data addition workflow example analysis of aerobic transition (Figure 6); for adding new data, it's recommended to start with lightweight [precise1k-analyze repository](https://github.com/SBRG/precise1k-analyze)

## Additional Information

The iModulons computed from PRECISE-1K can be explored through an interactive web interface at [iModulonDB](https://imodulondb.org/dataset.html?organism=e_coli&dataset=precise1k).

Please cite our [Biorxiv preprint](https://www.biorxiv.org/content/10.1101/2021.04.08.439047v2) if you find this repository useful! This link will be updated when this work is published.
