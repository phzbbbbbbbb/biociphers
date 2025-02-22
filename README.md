# Identifying common transcriptome signatures of cancer by interpreting deep learning models
Anupama Jha\*, Mathieu Quesnel-Vallieres\*, David Wang, Andrei Thomas-Tikhonenko, Kristen W. Lynch and Yoseph Barash

*Equal contribution

## Correspondence to: 

Anupama Jha <anupamaj@seas.upenn.edu>

Mathieu Quesnel-Vallieres <mathieu.quesnel-vallieres@pennmedicine.upenn.edu>

Yoseph Barash <yosephb@pennmedicine.upenn.edu>.

[Biociphers Lab](https://www.biociphers.org/), Department of CIS and genetics, University of Pennsylvania

## Citation

> Jha, Anupama, Mathieu Quesnel-Valli�res, Andrei Thomas-Tikhonenko, Kristen W. Lynch, and Yoseph Barash. 
"Identifying common transcriptome signatures of cancer by interpreting deep learning models." 
[bioRxiv (2021).](https://www.biorxiv.org/content/10.1101/2021.11.11.467790v1.abstract)

[comment]: <> ([![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3820839.svg)](https://doi.org/10.5281/zenodo.3820839))

This repo contains source code to reproduce results from Jha and Quesnel-Vallieres et al. work currently under peer-review. Source code is available under a BSD 3-clause license.

## Introduction
We train interpretable deep learning models capable of distinguishing between normal and cancer samples. 
We assembled a large RNA-Seq dataset comprising 13461 samples from 19 normal tissue types and 18 cancer types and 
split the data into two classes reflecting cancer state: normal or tumor (5,622 total normal samples and 7,839 total tumor samples). 
Samples were sourced from TCGA, GTEx and 12 other datasets 
(see [manuscript](https://www.biorxiv.org/content/10.1101/2021.11.11.467790v1.abstract) for details on the datasets). We train feed-forward neural 
networks for these data using three types of transcriptomic data: gene expression of protein-coding genes (19657 genes), gene expression of 
lncRNA (14257 lncRNAs) and inclusion of splicing junctions (40147 splice junctions). These trained models are interpreted to find pan-cancer 
transcriptomic signature of cancer comprising of protein-coding, lncRNA gene expression and alternative splicing. Feature attributions 
(similar to feature importance scores) are computed using [EIG](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-020-02055-7). 
Then we perform downstream analysis of the high attribution features to show their functional composition.

## How to run the analysis?
### Prerequisites

To run our analysis, we recommend generating a virtual enviroment and installing the prerequisite libraires from the 
[requirements.txt](https://bitbucket.org/biociphers/pan-cancer/raw/ace2c5fa16b85ab6cd6d5e95f2b3d74c84b8de5c/requirements.txt) as illustrated below.

```
python3 -m venv <your_target_directory>/pan_cancer_venv
source <your_target_directory>/pan_cancer_venv/bin/activate
pip install -r requirements.txt
```

### Reproducing figures
The following notebooks contain all the relevant analyses for producing the figures in our paper. Everything needed to run these notebooks is already present in this repo.

| File | Description |
| :--- | :---------- |
| [Performance of the DNN, SVM and RF models](https://bitbucket.org/biociphers/pan-cancer/raw/1c0e84ceca322b9b07137178e14a6184ebba7c53/src/model_performance.ipynb) |  model_performance.ipynb notebook contains AUPRC and accuracy metrics for the DNN, SVM and RF models for protein-coding genes, lncRNAs and splice junctions. |
| [AUPRC plots of the DNN, SVM and RF models](https://bitbucket.org/biociphers/pan-cancer/raw/1c0e84ceca322b9b07137178e14a6184ebba7c53/src/auprc_plots.ipynb) | auprc_plots.ipynb notebook contains AUPRC plots for the DNN, SVM and RF models for protein-coding genes, lncRNAs and splice junctions..  |
| [UMAP visualizations for Supplementary Figure S2](https://bitbucket.org/biociphers/pan-cancer/raw/1c0e84ceca322b9b07137178e14a6184ebba7c53/src/umap_visualizations.ipynb) | umap_visualizations.ipynb notebook contains umap visualizations for mean correction as well as latent embeddings produced by the DNN model. It also shows agreement between attributions generated by mean-corrected and combat-correct protein-coding DNN model.|


### Models predictions and attributions
#### Data download

Please download data and trained models from [here](https://majiq.biociphers.org/data/pan_cancer_data.tar.gz), decompress the file and place it in the results folder. 
The file is named pan_cancer_data.tar.gz (compressed size: 13 GB, decompressed size: 20 GB).

#### Reproduce predictions and attributions
To run this analysis, you will need the data and models already downloaded in the results folder. 
Once you have the data, you can run the whole pipeline for generating predictions and interpretations using: 

```
cd src/
sh run_pred_and_interpret.sh
```

This pipeline generates the predictions from the already trained models on the datasets used in the paper and generates feature attributions for the 
protein-coding genes, lncRNAs and splice junctions. Note that results/paper_results already contains the end product of this pipeline and new output will
be stored in results/run_results directory. This script assumes that data and models are present in results/pan_cancer_data folder. If you haven't downloaded 
the data, see instructions in the Data download section. 

#### Reproduce predictions
You can run the pipeline for generating predictions using: 

```
cd src/
sh run_pred.sh
```

#### Reproduce attributions

You can run the pipeline for generating attributions using: 

```
cd src/
sh run_interpret.sh
```



