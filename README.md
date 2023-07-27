# MODA

This repository contains the code, the notebooks, and the supplementary material for "An overview on multi-omic single-cell data joint analysis: good practices and results".

It aims to give some guidelines and good practice for whoever wants to start working with multi-Omic data analysis, specifically scRNA-seq + scATAC-seq datasets.

## How to cite

Martini L., Bardini R., Savino A., and Di Carlo S. An overview on multi-omic single-cell data joint analysis: good practices and results, 2023 (submitted to NAR Genomics and Bionformatics)

## Description

This repository aims to not only share the code to obtain the results but gives step-by-step commented workflow notebooks, for the three different methods discussed in the paper.
Specifically, the repo comprises of three sections, one for each pipeline (`Monocle3`/`Cicero`, `Seurat`/`Signac`, `Scanpy`/`Episcanpy`), consisting of the notebooks with the commented code and results. For each one it is also provided a HTML image to just look at them.

## Experimental setup

One can directly access the compiled notebooks to look at the commented pipeline and results. In each pipeline subfolder one can find a html file with the corresponding pipeline workflow.

If you want to work directly on the code the Rmarkdown and jupyter files are available. They provide a cell-divided script, where each chunck can be run separately.

Depending on the language you need to set up the environment.

### R
We made use of the renv library for ensuring reproducibility.
After installing R version 4.2.1, run the `Renv` (v. 0.15.5) package installation

```
install.packages("renv")
```
From inside one of the R pipeline folders, create an R project and run: 

```
renv::init()
renv::restore()
```

This will take the renv.lock situated in the working directory and restore the necessary packages.

### Python

One can find the requirement file for the needed packages in the Scanpy-Episcanpy folder.

After installing them, you can work on the jupyter notebook directly.

## Data Required

The needed data can be retrieved by https://www.10xgenomics.com/resources/datasets/10-k-human-pbm-cs-multiome-v-1-0-chromium-controller-1-standard-2-0-0

Specifically one needs to download the following files:
* Filtered feature barcode matrix MEX (DIR)
* Filtered feature barcode matrix (HDF5)
* ATAC peak locations (BED)
* ATAC Per fragment information file (TSV.GZ)
* ATAC Per fragment information index (TSV.GZ index)

All the files need to be unzipped (except ATAC Per fragment information file (TSV.GZ)), and put on the DATA/filtered_feature_bc_matrix/ folder.

Moreover, you need to download the reference dataset for the Seurat cell-type annotation from https://atlas.fredhutch.org/data/nygc/multimodal/pbmc_multimodal.h5seurat.
The file must be in the DATA/ref/ folder.

More data required are the garnett classifier (downloadable here https://cole-trapnell-lab.github.io/garnett/classifiers/) and the genomic annotations, which are provided in the DATA folder.

Since the co-accessbility calculation on the whole genome is a very long and computationally heavy calculation we provide als provide also the co-accessibility table resulted from it in the DATA/conns folder.
## R markdown Rendering

To run and render the markdown file run the following lines:

from the Monocle3-Cicero folder
```
Rscript -e "rmarkdown::render('Monocle-Cicero.Rmd')"
```
from the Seurat-Signac folder
```
Rscript -e "rmarkdown::render('Seurat-Signac.Rmd')"
```

Running the code will also output all the plots generated in the notebooks, saved in the Results/IMAGES folder.

## Repository structure
```
|
├── Monocle3-Cicero                            // Monocle3 and Cicero pipeline folder
|    ├── renv.lock                             // renv file for virtual environment setup
|    ├── Monocle-Cicero.Rmd                    // R markdown 
|    └── Monocle-Cicero_html.html              // HTML image
|    
├── Scanpy-Episcanpy                           // Scanpy and Episcanpy pipeline folder
|    ├── requirements.txt                      // requirement file for the required packages
|    ├── Scanpy-Episcanpy.ipynb                // Jupyter notebook
|    └── Scanpy-Episcanpy.ipynb                // HTML image
|    
├── Seurat-Signac                              // Seurat and Signac pipeline folder
|    ├── renv.lock                             // renv file for virtual environment setup
|    ├── Seurat-Signac.Rmd                     // R markdown 
|    └── Seurat-Signac_html.html               // HTML image
|
├── DATA                                       // Data folder
|    ├── conns                                 // Folder for the co-accessibility matrix
|    ├── filtered_feature_bc_matrix            // Folder for dataset files from 10X genomic
|    ├── garnett                               // Folder forr Garnet classifier
|    ├── genomes                               // Folder for the genomic annotations
|    └── Ref                                   // Folder for Seurat reference dataset
|
├── Results                                    // Results folder
|    └── IMAGES                                // Images produced
|
├── Supplementary Material.docx                // Supplementary material to the paper
|
└── README.md                                  // This README file    
```
