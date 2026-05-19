# FGC-GNN

FGC-GNN is a fuzzy graph covering based graph neural network framework designed for handling multi-omics datasets to implement cancer prediction tasks

The framework integrates multiple omics modalities 
into a unified graph-based deep learning architecture.
like :

BRCA 
- Gene Expression
- Copy Number Variation (CNV)
- Mutation

ROSMAP
- Gene Expression
- DNA Methylation
- miRNA Expression


LUSC
- Gene Expression

LAML
- Gene Expression
- Copy Number Variation (CNV)
- DNA Methylation
- miRNA Expression
- Mutation Features
- RPPA Proteomics


# Key Features

- Multi-omics data integration
- Patient similarity graph construction using cosine similarity
- Custom fuzzy graph convolution layer
- Attention-based message passing
- Cross-omics attention fusion
- Gated omics feature learning
- Focal loss for class imbalance handling
- Hyperparameter optimization with stratified cross-validation
- GPU acceleration with mixed precision training

---

# Workflow

```text
Multi-Omics Data
      ↓
Preprocessing & Normalization
      ↓
Patient Similarity Graph Construction (Gene-level)
      ↓
Omics-specific Graph Convolutions (Based on Fuzzy Graph Covering)
      ↓
Cross-Omics Attention Fusion
      ↓
Classification Head
      ↓
Prediction
```
---
# Multi-Omics Datasets

The framework supports multiple benchmark cancer datasets collected from Kaggle.

| Dataset | Link | Files / Modalities |
|----------|------|--------------------|
| BRCA | https://www.kaggle.com/datasets/samdemharter/brca-multiomics-tcga | `data.csv` |
| ROSMAP | https://www.kaggle.com/datasets/abbiirr/rosmap | `1_tr.csv`, `1_te.csv`, `1_featname.csv`, `2_tr.csv`, `2_te.csv`, `2_featname.csv`, `3_tr.csv`, `3_te.csv`, `3_featname.csv`, `labels_tr.csv`, `labels_te.csv` |
| LUSC | https://www.kaggle.com/datasets/noepinefrin/tcga-lusc-lung-cell-squamous-carcinoma-gene-exp | `LUSCexpfile.csv` |
| LAML | https://www.kaggle.com/datasets/jnikita/survboard | `LAML_data_complete_modalities_preprocessed.csv` |


---


# Model Architecture

The model consists of:

- Custom `FuzzyCoverConv` graph convolution layers
- Residual feature projections
- Layer normalization and dropout
- Learnable omics gating mechanisms
- Multi-head cross-omics attention
- Fully connected prediction layers

Each omics modality is processed independently before being fused into a shared representation for final prediction.

---

# Training Strategy

The framework uses:

- `AdamW` optimizer
- Cosine annealing learning rate scheduler
- Gradient clipping
- Early stopping
- Automatic mixed precision (AMP)

Hyperparameters such as hidden dimensions, dropout, learning rate, focal loss parameters, and training epochs are optimized using 5-fold stratified cross-validation.

---

# Evaluation Metrics

Performance is evaluated using:

- AUC
- F1 Score
- Accuracy

---

# Output Files

The pipeline automatically saves:

- Cross-validation results
- Training curves
- Test predictions
- Best model checkpoints


## Experimental Setup

All experiments for the proposed FGC-GNN framework were conducted using JupyterLab in a high-performance computing environment equipped with an NVIDIA RTX A5000 GPU and 128 GB RAM. The implementation was developed using Python-based deep learning libraries with GPU acceleration and automatic mixed precision (AMP) training to improve computational efficiency and memory utilization.

# Datasets and Data Splitting

The framework was evaluated on multiple cancer-related multi-omics datasets, including:

BRCA
ROSMAP
LUSC
LAML

For all datasets, the samples were divided into:

80% training/validation set
20% untouched test set

The held-out test set remained completely unseen during hyperparameter optimization and model selection to ensure unbiased performance evaluation.

# Cross-Validation Strategy

A 5-fold stratified cross-validation strategy was employed on the training portion of the data to preserve class distribution across folds. Hyperparameter optimization was performed independently within the cross-validation process.

For the BRCA dataset, the following hyperparameter search space was used:
<<<<<<< HEAD
'''
=======

>>>>>>> 19ddc84068e6800893c5755c4d3b9e7b2c6b1d8a
PARAM_GRID = {
    'hidden_channels': [128, 256, 512],
    'lr'             : [1e-3, 2e-4],
    'weight_decay'   : [1e-4, 1e-5],
    'dropout'        : [0.3, 0.5],
    'focal_gamma'    : [1, 2],
    'focal_alpha'    : [0.5, 0.75],
    'epochs'         : [400, 700, 1000],
}
<<<<<<< HEAD
'''
For the remaining datasets (ROSMAP, LUSC, and LAML), the following parameter configuration was used:

'''
=======

For the remaining datasets (ROSMAP, LUSC, and LAML), the following parameter configuration was used:

>>>>>>> 19ddc84068e6800893c5755c4d3b9e7b2c6b1d8a
PARAM_GRID = {
    'hidden_channels': [32, 64, 128],
    'lr'             : [1e-3, 2e-4],
    'weight_decay'   : [1e-3, 1e-4],
    'dropout'        : [0.3, 0.5],
    'focal_gamma'    : [0.5, 1],
    'focal_alpha'    : [0.5, 0.75],
    'epochs'         : [100, 200, 400],
}
<<<<<<< HEAD
'''
=======
>>>>>>> 19ddc84068e6800893c5755c4d3b9e7b2c6b1d8a
# Training Configuration

The proposed FGC-GNN model was trained using the following optimization strategy:

Optimizer: AdamW
Learning Rate Scheduler: Cosine Annealing
Loss Function: Focal Loss
Gradient Clipping: Applied to stabilize training
Early Stopping: Used to prevent overfitting
Mixed Precision Training: Enabled through AMP for faster computation and reduced GPU memory consumption
Repeated Evaluation with Multiple Random Seeds

To ensure robustness and reduce randomness-induced bias, the final optimized model was evaluated 10 independent times using different random seeds on the untouched 20% test set. The reported performance metrics represent the aggregated outcomes across these repeated runs.

# Evaluation Metrics

# Model performance was assessed using the following metrics:

AUC
F1 Score
Accuracy
# Reproducibility

The entire experimental pipeline, including preprocessing, graph construction, model training, cross-validation, and evaluation, was automated within the JupyterLab environment to ensure reproducibility and consistency across experiments.

