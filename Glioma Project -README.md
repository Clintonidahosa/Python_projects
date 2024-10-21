# Differential Gene Expression Profiling and Unsupervised Clustering to Predict Low Grade Gliomas(LGG) Prognosis

**Authors**:  
Sanzida Akhter Anee [@Sanzida](https://github.com/Sanzida), [@doc_idahosa](https://github.com/doc_idahosa), Sk Arif [@arif_shaikh](https://github.com/arif_shaikh), Nada Ghozlan [@Nad1](https://github.com/Nad1), Mennatallah Mohamed Ebrahim Mahmoud [@Mennatallah](https://github.com/Mennatallah), Stéphie Raveloson [@StephieRav](https://github.com/StephieRav), Chidimma Nwaku [@Mma](https://github.com/Mma), Zaka Ullah [@Zaka](https://github.com/Zaka), Idahosa Clinton 

## Project Overview
Gliomas are brain tumors that originate from glial cells, representing 80% of all primary malignant brain tumors in the central nervous system (CNS). This project aims to perform differential gene expression profiling and unsupervised clustering to predict gliomas prognosis based on RNA-seq data of low-grade gliomas (LGG) and their IDH mutation statuses.

## My Role
In this project, I focused on implementing the Machine Learning models, specifically K-Nearest Neighbors (KNN) and Random Forest, to predict the IDH status of gliomas. Here are the key aspects of my contributions:

- **Data Preprocessing**: I assisted in the preprocessing of RNA-seq data, ensuring it was normalized and filtered appropriately for analysis.
- **Feature Selection**: I applied variance thresholding for feature selection to reduce dimensionality and enhance model performance.
- **Model Implementation**: I developed and trained the KNN and Random Forest models using Python. I evaluated model performance based on accuracy, confusion matrices, and classification reports.
- **Performance Evaluation**: I analyzed and interpreted the results, comparing the performance of both models to determine which provided better classification for IDH-mutant and wild-type gliomas.

## Links
- [DE_Analysis R Code](https://github.com/sanzidaanee/Hackbio-cancer-internship/blob/main/Stage%204/Code/DEA.Rmd)
- [KNN python code](https://github.com/Clintonidahosa/Python_projects/blob/main/TCGA%20LGG%20KNN.md)
- [Random Forest Python Code](https://github.com/Clintonidahosa/Python_projects/blob/main/TCGA_LGG%20Random%20forest.md)
- [Dataset](https://github.com/sanzidaanee/Hackbio-cancer-internship/tree/main/Stage%204/Data)

## Introduction
- **Glioma Background**: Gliomas are classified into different grades, where low-grade gliomas (Grade I-II) are slower-growing, while high-grade gliomas (Grade III-IV) are more aggressive.
- **IDH Mutations**: Mutations in the IDH1 and IDH2 genes identify a subset of glioblastomas with a favorable prognosis.

## Methods
- **Gene Expression Profiles**: RNA-seq data were sourced from The Cancer Genome Atlas (TCGA) with a focus on 516 tumor samples.
- **Machine Learning Models**: The project employed KNN and Random Forest to predict IDH status, achieving high accuracy in model evaluation.

## Results
The Random Forest model achieved 99% accuracy with high precision and recall, while the KNN model had an accuracy of 83% but highlighted areas for improvement in classifying wild-type samples.

## Conclusion
This project underscores the significance of IDH status in glioma prognosis and demonstrates the efficacy of machine learning models in predicting genetic status based on gene expression profiles.

## References
## References
1. Ahir, B. K., Engelhard, H. H., & Lakka, S. S. (2020). Tumor development and angiogenesis in adult brain tumors: glioblastoma. Molecular neurobiology, 57, 2461-2478.
2. What Makes a Brain Tumor High-Grade or Low-Grade? David Reardon, MD. April 3, 2018. [Link](https://blog.dana-farber.org/insight/2018/04/makes-brain-tumor-high-grade-low-grade/).
3. Nakhate, V., Lasica, A. B., & Wen, P. Y. (2024). The Role of Mutant IDH Inhibitors in the Treatment of Glioma. Current Neurology and Neuroscience Reports, 1-13.
4. The Cancer Genome Atlas. (2015). Data Portal. National Cancer Institute. [Link](https://tcga-data.nci.nih.gov/tcga/tcgaHome2.jsp)

