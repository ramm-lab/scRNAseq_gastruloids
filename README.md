# scRNA-seq of mouse gastruloids at t96 vs t120

Single-cell RNA-seq analysis of mouse gastruloids from GEO series [GSE274389](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE274389). It compares the 96 h and 120 h timepoints, and the two 120 h conditions (dox96-G vs dox96-R).

## Data

| File | Sample | Timepoint |
|------|--------|-----------|
| `GSM8448423_t96.h5` | `t96` | 96 h |
| `GSM8448424_t120_dox96-G.h5` | `t120_G` | 120 h, dox at 96 h (G) |
| `GSM8448425_t120_dox96-R.h5` | `t120_R` | 120 h, dox at 96 h (R) |

## Analysis (`t96_t120.ipynb`)

1. **Load and merge** the three samples into one AnnData object.
2. **QC**: keep cells with 500–8000 genes and < 20% mitochondrial reads; keep genes found in ≥ 3 cells.
3. **Doublet removal** with Scrublet, run on each sample separately.
4. **Normalisation**: scale to 10,000 counts per cell, log1p, then select highly variable genes.
5. **Clustering**: PCA (40 PCs), UMAP, Leiden (resolution 0.5). Low-quality clusters (6–9) are removed.
6. **Genes of interest**: Adam/Mmp/Timp proteases, EGF/TGF-β/BMP/Notch/Nodal pathway genes, Tbxt, and others, plotted on the UMAP.
7. **Differential expression**:
   - all cells, t120 vs t96
   - t120 cells only (re-clustered), t120_G vs t120_R

## Outputs (`results/`)

- `DE_t120_vs_t96_global.csv`: DE genes, t120 vs t96 (p < 0.05)
- `DE_t120G_vs_t120R.csv`: DE genes, t120_G vs t120_R (p < 0.05)
- `cluster_markers.csv`: marker genes for each cluster
- `qc_*.png`, `scrublet_scores.png`: QC plots
- `umap_*.png`: UMAPs of clusters, cell types, genes of interest and top DE genes

