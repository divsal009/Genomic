# EAGLE-Net: Evolutionary Attention-Gated Learning Ensemble Network for RNA-Seq Cancer-Type Classification

This repository contains the implementation of **EAGLE-Net**, an **Evolutionary Attention-Gated Learning Ensemble Network** for **RNA-Seq-based multi-class cancer-type classification**.

The framework combines **ANOVA-based gene pre-filtering**, **evolutionary compact gene-subset optimisation**, **gated gene-token attention**, **residual 1D-CNN feature extraction**, **dense global-expression modelling**, and **learned branch-wise fusion**.

## Dataset

This project uses the publicly available **UCI Gene Expression Cancer RNA-Seq dataset**.

**Dataset page:**  
https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq

**Direct dataset download:**  
https://archive.ics.uci.edu/static/public/401/gene+expression+cancer+rna+seq.zip

The dataset contains **801 tumour samples**, **20,531 gene-expression features**, and **5 cancer classes**: **BRCA**, **COAD**, **KIRC**, **LUAD**, and **PRAD**.

The cancer classes correspond to:

- **BRCA** — Breast invasive carcinoma
- **COAD** — Colon adenocarcinoma
- **KIRC** — Kidney renal clear cell carcinoma
- **LUAD** — Lung adenocarcinoma
- **PRAD** — Prostate adenocarcinoma

Each row represents one tumour sample, and each gene-expression column represents one numerical gene-expression feature.

## Proposed Model

The proposed model is **EAGLE-Net: Evolutionary Attention-Gated Learning Ensemble Network**.

EAGLE-Net integrates **ANOVA-based gene pre-filtering**, **evolutionary gene-subset optimisation**, **gene-token embedding**, **gated self-attention**, **transformer-style self-attention**, **residual 1D-CNN local expression modelling**, **dense global-expression modelling**, **learned branch-wise fusion**, **repeated stratified cross-validation**, **ablation analysis**, and **robustness testing**.

## Methodological Workflow

RNA-Seq dataset → Data preprocessing → Label encoding → Z-score standardisation → ANOVA gene pre-filtering → Evolutionary compact gene-subset optimisation → EAGLE-Net multi-branch representation learning → Cancer-type classification → Evaluation, ablation and robustness testing.

## Why Feature Optimisation Is Used

RNA-Seq data are highly dimensional. In this dataset, each sample contains **20,531 gene-expression features**, while the dataset contains only **801 samples**. Directly training deep learning models on all gene features may increase redundancy, noise sensitivity, and overfitting risk.

Therefore, the workflow first applies **ANOVA-based gene ranking** to identify discriminative gene-expression features, followed by **evolutionary compact gene-subset optimisation** to select a smaller and less redundant gene subset. This compact optimised gene subset is then used as input to EAGLE-Net.

## EAGLE-Net Architecture

EAGLE-Net uses three representation-learning branches.

**1. Gated attention branch:** This branch converts selected genes into gene-token representations and applies a gating mechanism before self-attention. It is designed to learn class-relevant relationships among selected genes.

**2. Residual 1D-CNN branch:** This branch treats the selected gene-expression vector as a one-dimensional signal and extracts local expression patterns using convolutional layers and residual connections.

**3. Dense global-expression branch:** This branch captures global nonlinear relationships across the selected gene subset using fully connected layers.

The branch outputs are combined using **learned branch-wise fusion**, allowing the network to adaptively weight attention-based, convolutional, and dense representations.

## Models Evaluated

The following models are evaluated: **EAGLE-Net Proposed**, **EAGLE Deep Ensemble**, **Optimised MLP**, **Residual 1D-CNN**, **Gene-Patch Transformer**, **Denoising Autoencoder Classifier**, **EAGLE-Net without CNN**, **EAGLE-Net without Attention**, and **EAGLE-Net without Gate**.

The ablated models are used to examine the contribution of the CNN branch, attention branch, and gating mechanism.

## Evaluation Metrics

Model performance is assessed using **accuracy**, **precision**, **recall**, **weighted F1-score**, and **ROC-AUC**. Repeated cross-validation results are reported as **mean ± standard deviation**.

## Main Result

The proposed **EAGLE-Net** achieved the strongest repeated cross-validation performance:

| Metric | Performance |
|---|---:|
| **Accuracy** | **0.9988 ± 0.0040** |
| **Precision** | **0.9988 ± 0.0038** |
| **Recall** | **0.9988 ± 0.0040** |
| **Weighted F1-score** | **0.9987 ± 0.0040** |
| **ROC-AUC** | **1.0000 ± 0.0001** |

## Output Figures

The workflow generates the following figures:

**Fig 1. EAGLE-Net workflow diagram** — Shows the full modelling pipeline from RNA-Seq input to cancer-type classification.

**Fig 2. PCA visualisation of RNA-Seq gene-expression profiles** — Shows tumour samples projected onto the first two principal components.

**Fig 3. Training and validation curves for EAGLE-Net** — Shows training and validation accuracy and loss across epochs.

**Fig 4. Comparative weighted F1-score** — Compares EAGLE-Net with deep learning comparator models.

**Fig 5. Ablation analysis** — Shows the effect of removing the CNN branch, attention branch, and gating mechanism.

**Fig 6. Robustness analysis** — Shows model stability under Gaussian noise perturbation.

## Output Tables

The notebook generates **Table 1. Comparative model performance**, **Table 2. EAGLE-Net ablation analysis**, and **Table 3. Robustness analysis under Gaussian noise perturbation**.


## Installation

Clone the repository:

git clone https://github.com/divsal009/Genomic.git
cd Genomic

Install the required Python packages:

pip install -r requirements.txt

If `requirements.txt` is not available, install the main dependencies manually:

pip install numpy pandas matplotlib scikit-learn tensorflow requests

## How to Run

Open the notebook **EAGLE_Net_RNASeq_Cancer_Classification.ipynb** and run all cells in order.

The notebook performs **online dataset download**, **dataset extraction**, **RNA-Seq data loading**, **data preprocessing**, **label encoding**, **z-score standardisation**, **ANOVA-based gene pre-filtering**, **evolutionary compact gene-subset optimisation**, **EAGLE-Net model training**, **comparator model training**, **repeated stratified cross-validation**, **ablation analysis**, **robustness testing**, **training and validation curve generation**, and **publication-ready metric tables and figures**.

## Code Availability

Author-generated code supporting this work is available in this repository:

https://github.com/divsal009/Genomic

The repository includes code for **dataset download**, **preprocessing**, **ANOVA-based gene pre-filtering**, **evolutionary feature optimisation**, **EAGLE-Net model construction**, **model training**, **repeated cross-validation**, **ablation analysis**, **robustness testing**, **visualisation**, and **result reporting**.

## Data Availability

The dataset used in this project is publicly available from the **UCI Machine Learning Repository**:

https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq

The dataset is downloaded directly from the public repository during execution. No private, identifiable, or newly collected human participant data are used.

## Ethics Statement

This study uses a publicly available, de-identified dataset and does not involve direct recruitment of human participants, intervention, collection of new biological samples, or access to identifiable personal data. Accordingly, separate ethical approval is not required.

## Limitations

The results should be interpreted within the scope of the evaluated public RNA-Seq dataset. Although EAGLE-Net achieved strong repeated cross-validation performance, further validation on **independent RNA-Seq cohorts**, **larger multi-cancer datasets**, and **biologically annotated gene sets** is required before translational or clinical use.

## Citation

If you use this repository, please cite the related manuscript once available.

Suggested citation format:

Saleela D, et al. EAGLE-Net: An Evolutionary Attention-Gated Learning Ensemble Network for RNA-Seq Cancer-Type Classification.

## Author

**Divya Saleela**  
Postdoctoral Research Fellow  
University of Southampton  

GitHub: https://github.com/divsal009

## License

This repository is provided for academic and research use. Please check the dataset licence and repository licence before reuse or redistribution.
