# EAGLE-Net for RNA-Seq Cancer-Type Classification

This repository contains the implementation used to develop and evaluate EAGLE-Net, an evolutionary gene-subset optimisation and attention-gated multi-branch deep-learning framework for RNA-Seq-based cancer-type classification.

The experiments use the UCI Gene Expression Cancer RNA-Seq dataset, comprising 801 tumour samples, 20,531 gene-expression features and five cancer classes: BRCA, COAD, KIRC, LUAD and PRAD.

Dataset source:
https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq

Direct download:
https://archive.ics.uci.edu/static/public/401/gene+expression+cancer+rna+seq.zip

## Implementation

The workflow begins by loading the RNA-Seq expression matrix and removing the non-informative sample identifier column. Cancer labels are encoded for supervised classification, and the data are partitioned using repeated stratified cross-validation.

All preprocessing and feature-selection operations are performed independently within the training partition of each fold. Standardisation parameters are estimated from the training samples and subsequently applied to the corresponding validation and held-out evaluation samples.

The original gene-expression space is first reduced using ANOVA-based feature ranking. The highest-ranked genes form the candidate pool for evolutionary optimisation. A compact subset is then selected using a fitness function that favours genes with strong class-discriminative evidence while penalising pairwise redundancy.

The selected expression vector is passed to EAGLE-Net. The model contains a gated gene-token attention branch, a residual one-dimensional convolutional branch and a dense global-expression branch. The attention branch projects the selected expression values into token representations, applies a learned gating operation and then models interactions using multi-head self-attention. The convolutional branch extracts local patterns from the selected expression sequence, while the dense branch models global nonlinear relationships across the complete selected feature vector. The three branch representations are combined using learned branch-wise fusion before final softmax classification.

## Experimental design

Model evaluation is based on five-fold stratified cross-validation repeated twice, producing ten held-out evaluation folds. An internal validation split is used within each training fold for early stopping and model monitoring.

The default implementation retains 500 ANOVA-ranked candidate genes and uses evolutionary optimisation to select 64 features. The evolutionary search uses a population of 30 chromosomes, 25 generations, set-based crossover, elitism, a mutation probability of 0.10 and a redundancy penalty of 0.10.

EAGLE-Net is trained using the Adam optimiser with a learning rate of 0.001, a batch size of 32 and a maximum of 50 epochs. Early stopping is applied using validation loss with a patience of 10 epochs. Gaussian-noise regularisation, dropout and batch normalisation are used during training. Class-weighted categorical cross-entropy is applied to account for the unequal class distribution.

The repository also includes the implemented comparator models and the EAGLE-Net ablation variants used in the evaluation. These include the deep ensemble, optimised multilayer perceptron, denoising autoencoder classifier, gene-patch transformer, residual one-dimensional convolutional network, EAGLE-Net without the convolutional branch, EAGLE-Net without attention and EAGLE-Net without the gating operation.

## Evaluation

Performance is calculated using accuracy, precision, recall, macro F1-score, weighted F1-score, balanced accuracy, Matthews correlation coefficient and ROC-AUC. Results are aggregated across the ten held-out evaluation folds and reported as mean and standard deviation.

The analysis also includes component ablation, class-wise confusion matrices, one-vs-rest ROC and precision-recall curves, training and validation behaviour, Gaussian-noise perturbation testing and computational-cost measurements.


## Software environment

The implementation uses Python with TensorFlow/Keras for model construction and training. Scikit-learn is used for stratified cross-validation, standardisation, ANOVA feature ranking, class-weight calculation and metric computation. NumPy and pandas are used for numerical and tabular processing, while Matplotlib is used for visualisation.

Random seeds are fixed for Python, NumPy and TensorFlow. Small numerical differences may occur across hardware, CUDA and TensorFlow versions because some GPU operations are not fully deterministic.

## Data and code availability

The RNA-Seq dataset is publicly available from the UCI Machine Learning Repository:

https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq

The implementation is available at:

https://github.com/divsal009/Genomic



GitHub:
https://github.com/divsal009
