# PBMC scRNA-seq Analysis (Seurat, 10x PBMC3k)

This project contains an R Markdown workflow (`scRNAseq.Rmd`) for analysing 10x Genomics PBMC3k single-cell RNA-seq data using **Seurat**.  
The notebook walks through data import, quality control, dimensionality reduction, clustering, and cell type annotation.

## Main steps

1. **Downloads**
   - Install/load required R packages (Seurat, dplyr, patchwork, DT, ggplot2).
   - Download and unpack the PBMC3k count matrix from 10x Genomics.

2. **Preprocessing & QC**
   - Create a Seurat object.
   - Compute standard QC metrics (nFeature_RNA, nCount_RNA, percent.mt).
   - Visualise QC metrics and filter out low-quality cells (feature/UMI cutoffs, high mitochondrial content).

3. **Normalisation & Feature Selection**
   - Log-normalise counts (`NormalizeData`).
   - Identify highly variable genes (`FindVariableFeatures`).

4. **Dimensionality Reduction & Clustering**
   - Scale data and run PCA.
   - Inspect PCs via loadings, heatmaps, and elbow plot.
   - Build a neighbour graph and compute UMAP embeddings.
   - Explore the effect of number of PCs and clustering resolution, then fix on **10 PCs, resolution 0.3**.

5. **Marker Detection & Cell Type Annotation**
   - Use `FindAllMarkers` (ROC test, only positive markers) to identify cluster markers.
   - Build a composite marker score (AUC × log₂ fold change × specificity) and select one top marker per cluster.
   - Visualise marker expression on UMAP and assign labels:
     - Naive CD4 T, CD14⁺ Mono, NK/CD8 T, B cells, CD16⁺ Monocytes, Dendritic cells, Platelets.

## Files in this repository

- `scRNAseq.Rmd` - R Markdown notebook containing the full PBMC scRNA-seq analysis workflow (QC, normalization, PCA, UMAP, clustering, marker detection, and cell type annotation).
- `scRNAseq.html` - Rendered HTML report generated from `scRNAseq.Rmd`, with all figures, tables and narrative results.
