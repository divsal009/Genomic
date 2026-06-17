# EAGLE-Net for RNA-Seq Cancer-Type Classification

This repository contains the code used for the EAGLE-Net experiments on RNA-Seq cancer-type classification.

The experiments use the UCI Gene Expression Cancer RNA-Seq dataset, which contains 801 tumour samples, 20,531 gene-expression features and five cancer classes: BRCA, COAD, KIRC, LUAD and PRAD.

Dataset source:
https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq

Direct download:
https://archive.ics.uci.edu/static/public/401/gene+expression+cancer+rna+seq.zip

## Implementation

The code loads the RNA-Seq expression matrix, removes the sample identifier column, encodes the class labels and creates repeated stratified cross-validation splits.

Preprocessing and feature selection are carried out separately within each training fold. Standardisation parameters are fitted on the training data and then applied to the validation and held-out data.

ANOVA ranking is used to reduce the original feature space. The highest-ranked genes form the candidate pool for evolutionary selection. A compact subset is then selected using a fitness function based on class discrimination and pairwise feature redundancy.

EAGLE-Net contains three parallel branches: a gated gene-token attention branch, a residual one-dimensional convolutional branch and a dense branch. Their outputs are combined using learned fusion weights before softmax classification.

## Experimental design

The experiments use five-fold stratified cross-validation repeated twice, giving ten held-out evaluations. An internal validation split is used for early stopping.

The default configuration retains 500 ANOVA-ranked genes and selects 64 genes through evolutionary optimisation. The evolutionary search uses a population size of 30, 25 generations, set-based crossover, elitism, a mutation probability of 0.10 and a redundancy penalty of 0.10.

The model is trained using Adam with a learning rate of 0.001, a batch size of 32 and a maximum of 50 epochs. Early stopping is based on validation loss with a patience of 10 epochs. Gaussian noise, dropout, batch normalisation and class-weighted categorical cross-entropy are used during training.

The repository also contains the comparator models and ablation variants used in the experiments.

## Evaluation

The evaluation reports accuracy, precision, recall, macro F1-score, weighted F1-score, balanced accuracy, Matthews correlation coefficient and ROC-AUC.

The code also produces confusion matrices, ROC and precision-recall curves, training curves, ablation results, Gaussian-noise experiments and computational-cost measurements.

## Software environment

The implementation uses Python, TensorFlow/Keras, scikit-learn, NumPy, pandas and Matplotlib.

Random seeds are set for Python, NumPy and TensorFlow. Small numerical differences may occur across TensorFlow, CUDA and hardware configurations.

## Data and code availability

The dataset is publicly available from the UCI Machine Learning Repository:

https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq

The code is available at:

https://github.com/divsal009/Genomic
