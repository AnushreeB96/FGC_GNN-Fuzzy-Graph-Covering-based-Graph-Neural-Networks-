# FGC-GNN

FGC-GNN is a fuzzy graph covering based graph neural network framework designed for handling multi-omics datasets to implement cancer prediction tasks

The framework integrates multiple omics modalities including:

BRCA 
- Gene Expression
- Copy Number Variation (CNV)
- Mutation
- Protine-Expression Layer

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


into a unified graph-based deep learning architecture.

---

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
Patient Similarity Graph Construction
      ↓
Omics-specific Graph Convolutions
      ↓
Cross-Omics Attention Fusion
      ↓
Classification Head
      ↓
Prediction
```

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

- ROC-AUC
- F1 Score
- Accuracy

---

# Output Files

The pipeline automatically saves:

- Cross-validation results
- Training curves
- Test predictions
- Best model checkpoints


