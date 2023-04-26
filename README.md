# PRECISE-1K

This repository contains data and code necessary for assembling the PRECISE-1K _E. coli_ K-12 MG1655 expression and transcriptional regulation knowledgebase, including computing and analyzing iModulons, analyzing expression patterns, and generating all figures for the associated publication. ([publication](https://www.biorxiv.org/content/10.1101/2021.04.08.439047v2))

This repository also includes data, assembly, iModulon computation, and analysis for the larger, 2710-sample "Public K-12" RNA-seq resource.

To analyze new data with the PRECISE-1K knowledgebase, we recommend starting with the lightweight [precise1k-analyze repository](https://github.com/SBRG/precise1k-analyze).

## Setup

Ensure you have Python 3.6+, Jupyter (`pip install jupyterlab`), and the iModulon analysis package `pymodulon` installed (`pip install pymodulon`). 

`pymodulon` documentation can be found [here](https://pymodulon.readthedocs.io/en/latest/index.html).

Installing `pymodulon` using `pip` will install all other needed packages.

Then, clone this repository onto your local machine by executing the following command in your command prompt/terminal: `git clone https://github.com/SBRG/precise1k.git`. This command will copy this repository to a folder called `precise1k` in the directory from which the command was executed. This repository contains many data files, so cloning may take a few minutes.

## Overview

The repository is split into 2 subdirectories: `data` and `notebooks`. All analyses are presented in the form of Jupyter notebooks in the `notebooks` subdirectory, utilizing data from the `data` directory.

### Data

The `data` directory contains further subdirectories with the following constituent files:

- `annotation`: contains gene and regulatory network annotations for K-12 MG1655
   - `gene_info.csv`: a table of gene metadata for K-12 MG1655, assembled primarily from NCBI RefSeq NC_000913.3 and the E. coli K-12 MG1655 [Bitome](https://academic.oup.com/nar/article/48/18/10157/5911745)
   - `TRN.csv`: a table containing regulatory annotations (i.e. regulator->gene links), assembled primarily from [RegulonDB](https://regulondb.ccg.unam.mx/) and [EcoCyc](https://www.ecocyc.org/)
- `k12_modulome`
- `precise`
- `precise1k`
- `regulation`
- `sequence_files`

## Additional Information

The iModulons computed from PRECISE-1K can be explored through an interactive web interface at [iModulonDB](https://imodulondb.org/dataset.html?organism=e_coli&dataset=precise1k).

Please cite our [Biorxiv preprint](https://www.biorxiv.org/content/10.1101/2021.04.08.439047v2) if you find this repository useful! This link will be updated when this work is published.
