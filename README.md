# Contrastive_Learning

# Multimodal Cancer Analysis: Combining WSI and Gene Expression

A personal project exploring how to combine histology images and gene expression data for cancer analysis using contrastive learning.

## What This Project Does

This project takes a different approach to analyzing cancer data. Instead of traditional supervised learning, I use **gene expression similarity to guide image learning**. The idea is simple: if two patients have similar gene expression profiles, their tissue should look similar too.

**Main Components:**
- Download and preprocess whole slide images (WSI) from cancer patients
- Download matching gene expression data
- Use gene similarities to create training pairs for a computer vision model
- Train a model to recognize tissue patterns that correspond to molecular similarities

## Dataset

- **Source**: TCGA breast cancer data
- **Patients**: 5 cases with both WSI and RNA-seq data
- **WSI**: Large microscopy images (~1GB each)
- **Gene Expression**: ~16,000 genes per patient
- **Final Training Data**: 7,500 image patches + 500 training triplets

## How It Works

### 1. Data Processing
```
WSI Images → Extract patches → Remove background → Color normalize → Augment
Gene Data → Filter genes → Normalize counts → Calculate similarities
```

### 2. Smart Training Pair Creation
Instead of random pairs, I create training triplets based on gene expression:
- **Anchor**: Random tissue patch from Patient A
- **Positive**: Tissue patch from Patient B (similar genes to A)
- **Negative**: Tissue patch from Patient C (different genes from A)

### 3. Model Training
- Used ResNet-18 with contrastive learning (triplet loss)
- Model learns to recognize tissue patterns that match molecular similarities
- Trained for 20 epochs, loss improved from 0.93 to 0.50

## Key Results

**Gene Expression Analysis:**
- Found 3 distinct molecular groups among the 5 patients
- Similarity ranges from -0.44 (very different) to 0.10 (most similar)

**Model Training:**
- Successfully generated 500 high-quality training triplets
- Model converged well with steady loss reduction
- Learned to distinguish tissue patterns based on molecular similarity


## What I Learned

**Technical Skills:**
- Working with large medical image files (gigabytes each)
- Processing gene expression data from TCGA
- Implementing contrastive learning with custom triplet generation
- Handling multimodal data alignment and preprocessing

**Biological Insights:**
- Found meaningful molecular subgroups in just 5 patients
- Learned how gene expression patterns can guide image analysis
- Understood the connection between molecular and morphological features

## Limitations & Future Work

**Current Limitations:**
- The small dataset limits clinical applications, but it demonstrates the potential of using molecular data to guide image analysis in cancer research.
- Only 5 patients (proof of concept scale)
- CPU training only (slow and limits model complexity)

**Next Steps:**
- Scale to 50-100 patients for more robust results
- Add survival/treatment outcome prediction
- Try larger models (ResNet-50, Vision Transformers)
- Compare against traditional approaches
- Add proper cross-validation
