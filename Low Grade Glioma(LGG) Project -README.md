# Differential Gene Expression Profiling and Unsupervised Clustering to Predict Gliomas Prognosis

## Authors (@slack):
- Sanzida Akhter Anee (@Sanzida)
- Idahosa Clinton (@doc_idahosa)
- Sk Arif (@arif_shaikh)
- Nada Ghozlan (@Nad1)
- Mennatallah Mohamed Ebrahim Mahmoud (@Mennatallah)
- Stéphie Raveloson (@StephieRav)
- Chidimma Nwaku (@Mma)
- Zaka Ullah (@Zaka)


## My Role
In this project, I focused on implementing the Machine Learning models, specifically K-Nearest Neighbors (KNN) and Random Forest, to predict the IDH status of gliomas. Here are the key aspects of my contributions:

- **Data Preprocessing**: I assisted in the preprocessing of RNA-seq data, ensuring it was normalized and filtered appropriately for analysis.
- **Feature Selection**: I applied variance thresholding for feature selection to reduce dimensionality and enhance model performance.
- **Model Implementation**: I developed and trained the KNN and Random Forest models using Python. I evaluated model performance based on accuracy, confusion matrices, and classification reports.
- **Performance Evaluation**: I analyzed and interpreted the results, comparing the performance of both models to determine which provided better classification for IDH-mutant and wild-type gliomas.

## Links
- [DE_Analysis R Code](https://github.com/sanzidaanee/Hackbio-cancer-internship/blob/main/Stage%204/Code/DEA.Rmd)
- [KNN python code](https://github.com/Clintonidahosa/Python_projects/blob/main/Low%20Grade%20Gliomas(KNN%20project).md)
- [Random Forest Python Code](https://github.com/Clintonidahosa/Python_projects/blob/main/Low%20Grade%20Glioma%20(Random%20Forest%20project).md)
- [Dataset](https://github.com/sanzidaanee/Hackbio-cancer-internship/tree/main/Stage%204/Data)

## Introduction
Gliomas are brain tumors that originate from glial cells, which represent 80% of all primary malignant brain tumors in the central nervous system (CNS) [1].

There are different grades of gliomas, ranging from low-grade (Grade I-II), which are typically slower-growing, to high-grade gliomas (Grade III-IV), which are more aggressive and harder to treat [2]. Mutations in the isocitrate dehydrogenase (IDH) genes (IDH1 and IDH2) identify a subset of glioblastomas with a favorable prognosis [3].

## Methods

### Gene Expression Profiles Data
RNA-seq data of low-grade gliomas (LGG) along with clinical information and IDH mutation statuses (IDH1 and IDH2) with 516 tumor samples were downloaded from The Cancer Genome Atlas (TCGA) [4]. The dataset contained 60,660 genes across 534 patient samples, of which 460 had mutant IDH and 34 had wild-type IDH.

### Data Processing
All datasets were normalized and filtered through quantile normalization using gene length in the `edgeR` package [5] and log2 transformation of expression matrices.

### Differential Expression Analysis
Using the `edgeR` package [5], differentially expressed genes (DEGs) were identified. We used a p-value threshold of 0.01, false discovery rate (FDR) < 0.01, and a log2 fold change (logFC) cutoff of 1, where logFC > 1 for upregulated genes and logFC < -1 for downregulated genes.

### Enrichment of DEGs
We used the `biomaRt` package [6] for gene annotation and the `TCGAbiolinks` package [7] for pathway enrichment analysis at the gene ontology biological process level.

### Machine Learning Model
We used feature selection and machine learning techniques to predict IDH status:

- **Random Forest:** Recursive Feature Elimination (RFE) was used to select the top 100 features. A Random Forest classifier was trained on the selected features, and its performance was evaluated using accuracy, a confusion matrix, and a classification report [8].
- **K-Nearest Neighbors (KNN):** Variance thresholding was applied for feature selection, followed by KNN model training and evaluation with accuracy and performance metrics [8].

## Results

### Differential Expression Analysis
We filtered 34,539 genes with 419 wild-type and 94 mutant samples from 60,660 genes. After DE analysis, we identified 5,916 DEGs, revealing significant clustering of upregulated genes in IDH-mutant samples. 

A volcano plot (Fig. 1) and heatmap (Fig. 2) were generated to visualize these findings:

- **Figure 1:** Volcano plot of low-grade gliomas (LGG) dataset, showing log2-fold change and adjusted p-value. Red points indicate upregulated genes, and blue points indicate downregulated genes.
<img src="https://drive.google.com/uc?export=view&id=1eRohYAQwp7LbqDgDL4nk6NM0JSSoTZda" alt="My Image" width="600" height="400">
 
- **Figure 2:** Heatmap of hierarchical clustering of 5,916 DEGs. Red and green indicate high and low expression genes, respectively.
<img src="https://drive.google.com/uc?export=view&id=10AazIoEm7yFp2d4b3BsuJeN36Epr-npH" alt="Embedded Image" width="600" height="400">

Following the analysis, 1,681 upregulated and 4,235 downregulated genes were identified as common.

### Enrichment Analysis
- **Upregulated Genes:** Enriched in synaptic transmission, cell-cell signaling, transmission of nerve impulse, and homophilic cell adhesion (Fig. 3).
<img src="https://drive.google.com/uc?export=view&id=1l38PCIfWrSQ3kzoSRKF7uXEdLtrhjTNn" alt="Embedded Image" width="600" height="400">
 
- **Downregulated Genes:** Enriched in anterior-posterior pattern formation, skeletal system development, and embryonic morphogenesis (Fig. 4).
<img src="https://drive.google.com/uc?export=view&id=1xl6IIIvJLY_bW49PXGoMYESfbSPsDhA8" alt="Embedded Image" width="600" height="400">

### Machine Learning Models
- **Random Forest:** Achieved 99% accuracy, with high precision and recall for both mutant and wild-type classes, demonstrating superior performance.
- **KNN:** Achieved 83% accuracy, performing well for mutant samples but requiring improvements for wild-type classification.

## Conclusion
- IDH status significantly influences glioma heterogeneity.
- Mutant IDH gliomas show unique gene expression profiles compared to wild-type tumors.
- The Random Forest model outperformed KNN in classifying IDH status, especially for wild-type samples.

## References
1. Ahir, B. K., Engelhard, H. H., & Lakka, S. S. (2020). Tumor development and angiogenesis in adult brain tumors: glioblastoma. Molecular neurobiology, 57, 2461-2478.
2. Reardon, D. (2018). What Makes a Brain Tumor High-Grade or Low-Grade? Dana-Farber Blog. Retrieved from [link](https://blog.dana-farber.org/insight/2018/04/makes-brain-tumor-high-grade-low-grade/).
3. Nakhate, V., Lasica, A. B., & Wen, P. Y. (2024). The Role of Mutant IDH Inhibitors in the Treatment of Glioma. Current Neurology and Neuroscience Reports, 1-13.
4. The Cancer Genome Atlas. (2015). Data Portal. National Cancer Institute. Retrieved from [link](https://tcga-data.nci.nih.gov/tcga/tcgaHome2.jsp).
5. McCarthy DJ, Chen Y, Smyth GK (2012). "Differential expression analysis of multifactor RNA-Seq experiments with respect to biological variation." Nucleic Acids Research, 40(10), 4288-4297. DOI:10.1093/nar/gks042.
6. Durinck, S., Spellman, P. T., Birney, E., & Huber, W. (2009). Mapping identifiers for the integration of genomic datasets with the R/Bioconductor package biomaRt. Bioinformatics, 25(18), 2410-2411. DOI:10.1093/bioinformatics/btp515.
7. Colaprico, A., et al. (2016). TCGAbiolinks: an R/Bioconductor package for integrative analysis of TCGA data. Nucleic Acids Research, 44(8), e71. DOI:10.1093/nar/gkv1507.
8. Liaw, A., & Wiener, M. (2002). Classification and Regression by randomForest. R News, 2(3), 18-22.
