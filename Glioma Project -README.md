# Differential Gene Expression Profiling and Unsupervised Clustering to Predict Low Grade Gliomas(LGG) Prognosis

**Authors**:  
Idahosa Clinton (@doc_idahosa), Sanzida Akhter Anee (@Sanzida), Sk Arif (@arif_shaikh), Nada Ghozlan (@Nad1), Mennatallah Mohamed Ebrahim Mahmoud (@Mennatallah), Stéphie Raveloson (@StephieRav), Chidimma Nwaku (@Mma), Zaka Ullah (@Zaka), 

## Links
- [DE_Analysis R Code](https://github.com/sanzidaanee/Hackbio-cancer-internship/blob/main/Stage%204/Code/DEA.Rmd)
- [KNN python code](https://github.com/Clintonidahosa/Python_projects/blob/main/TCGA%20LGG%20KNN.md)
- [Random Forest Python Code](https://github.com/Clintonidahosa/Python_projects/blob/main/TCGA_LGG%20Random%20forest.md)
- [Dataset](https://github.com/sanzidaanee/Hackbio-cancer-internship/tree/main/Stage%204/Data)

## Introduction
Gliomas are brain tumors that originate from glial cells, which represent 80% of all primary malignant brain tumors in the central nervous system (CNS) [1]. There are different grades of gliomas, ranging from low-grade (Grade I-II), which are typically slower-growing, than high-grade gliomas (Grade III-IV), which are more aggressive and harder to treat [2]. Mutations occurring in the isocitrate dehydrogenase (IDH) genes (IDH1 and IDH2) identify a subset of glioblastomas with a favorable prognosis [3].

## Methods

### Gene Expression Profiles Data
RNA-seq data of low-grade gliomas (LGG) along with clinical information IDH mutations statuses IDH1 and IDH2 with 516 tumor samples from cancer patients were downloaded from The Cancer Genome Atlas (TCGA) [4]. The selected datasets in total 60660 genes across 534 patient samples of which 460 had mutant IDH and 34 had wild type IDH.

### Data Processing
Through the quantile normalization method by using gene length in edgeR package [5] and log2 transformation of expression matrixes, all datasets were normalized and filtered.

### Differential Expression Analysis
Using edgeR package [5], differentially expressed genes were discovered. We used p-value = 0.01 and FDR < 0.01 as a cutoff value and log 2 fold change (logFC) cutoff value is 1, where >1 for upregulated and < -1 for downregulated genes.

### Enrichment of DEGs
By using biomaRt package [6] for gene annotation and TCGAbiolinks package [7] for pathway enrichment analysis at gene ontology biological process level.

### Machine Learning Model
We used feature selection, machine learning and KNN modelling to predict IDH status.

- **Random Forest**: We used Recursive Feature Elimination (RFE) to select the top 100 features, trained a Random Forest classifier on the selected features, and evaluated model performance with accuracy, confusion matrix, and classification report [8].

- **K-Nearest Neighbors (KNN)**: We applied variance thresholding for feature selection, trained a KNN model, and evaluated predictions with accuracy and performance metrics [8].

## Results

### Differential Expression Analysis
To decipher the heterogeneity within IDH-mutant for low-grade gliomas, we filtered 34539 genes with 419 wild types and 94 mutant samples from 60660 genes.

Then from 34539 filtered genes, after DE analysis, identify 5,916 differentially expressed genes (DEGs) and revealing significant clustering of upregulated genes in IDH-mutant samples. This result aligns with the findings from the referenced paper.

We screened all the DEGs using log2FC = 0.01 and p-value = 1 as the threshold and showed them as volcano plots (Fig. 1).

![Volcano Plot](https://drive.google.com/file/d/1eRohYAQwp7LbqDgDL4nk6NM0JSSoTZda/view?usp=drive_link)
*Figure 1: Volcano plot of low-grade gliomas (LGG) dataset visualizes gene expression data. X-axis shows log2-fold change and Y-axis shows adjusted p-value. Red points indicate upregulated and blue dots indicate downregulated genes.*

Following overlapping, we identified 1681 upregulated and 4235 downregulated common genes.

The results of DE with 5916 genes were plotted as a heatmap (Fig. 2).

![Heatmap Output](path/to/your/heatmap_output_image.png)
*Figure 2: Hierarchical clustering heat map of 5916 DEGs from IDH mutant and wild type for low-grade gliomas (LGG) samples. Red and green indicate high and low expression genes, respectively.*

### Enrichment Analysis
Upregulated genes were enriched in synaptic transmission, cell-cell signaling, transmission of nerve impulse, homophilic cell adhesion and cell-cell adhesion might tend to have a better prognosis compared to more aggressive gliomas (Fig. 3).

Downregulated genes were enriched in anterior or posterior pattern formation, skeletal system development, regionalization, pattern specification process and embryonic morphogenesis indicate that these genes have better prognosis than aggressive gliomas (Fig. 4).

![Upregulated Genes Enrichment](path/to/your/upregulated_genes_ea_image.png)
*Figure 3: Functional enrichment analysis of upregulated genes for low-grade gliomas (LGG).*

![Downregulated Genes Enrichment](path/to/your/downregulated_genes_ea_image.png)
*Figure 4: Functional enrichment analysis of downregulated genes for low-grade gliomas (LGG).*

### Machine Learning Models
The Random Forest model achieved an impressive 99% accuracy, with only one misclassification. Precision, recall, and F1-scores were high for both classes, especially for "Mutant" (precision: 0.99, recall: 1.00) and "WT" (precision: 1.00, recall: 0.96), demonstrating robust performance.

The K-Nearest Neighbors (KNN) model had an accuracy of 83%. It performed well for "Mutant" samples (precision: 0.82, recall: 0.99) but struggled with "WT" samples, achieving a recall of 0.35 and F1-score of 0.50. This highlights significant misclassifications and a need for improvement in classifying "WT."

## Conclusion
Both studies underscore IDH status as a primary factor influencing glioma heterogeneity. Mutant LGGs, particularly those with IDH mutations, shows unique gene expression profiles compared to wildtype tumors. Enriched pathways suggest that IDH-mutant gliomas might be associated with more aggressive, invasive behavior of tumor than wild type. The Random Forest model significantly outperformed the K-Nearest Neighbors (KNN) model, especially in classifying "WT" samples, demonstrating superior overall accuracy and reliability in distinguishing between mutant and wild-type gliomas.

## References
1. Ahir, B. K., Engelhard, H. H., & Lakka, S. S. (2020). Tumor development and angiogenesis in adult brain tumors: glioblastoma. Molecular neurobiology, 57, 2461-2478.
2. What Makes a Brain Tumor High-Grade or Low-Grade? David Reardon, MD. April 3, 2018. [Link](https://blog.dana-farber.org/insight/2018/04/makes-brain-tumor-high-grade-low-grade/).
3. Nakhate, V., Lasica, A. B., & Wen, P. Y. (2024). The Role of Mutant IDH Inhibitors in the Treatment of Glioma. Current Neurology and Neuroscience Reports, 1-13.
4. The Cancer Genome Atlas. (2015). Data Portal. National Cancer Institute. [Link](https://tcga-data.nci.nih.gov/tcga/tc
