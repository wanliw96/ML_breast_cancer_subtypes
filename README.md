# ML_breast_cancer_subtypes

Different subtypes of breast cancer have been shown to associate with different prognoses, responses to particular treatments, and the likelihood of metastasis. Gene expression profiling of breast cancers is one of the techniques that allowed for an informative classification of this disease. In this project, the goal is to take the RNA-seq data from the TCGA breast cancer samples and use different machine learning methods to classify the breast cancer samples into 5 intrinsic subtypes. 

## Data

The Cancer Genome Atlas (TCGA) project has profiled many molecular characteristics of a large set of breast cancer and adjacent normal tissues. Gene expression was profiled using RNA-seq for about 1200 breast cancer/normal samples. Of these 1200 samples, about 500 were also profiled using gene expression microarrays. PAM50 is a famous classifier that can use 50 genes to clearly classify breast cancer into five intrinsic subtypes using microarray data. Here we also have PAM50 results as the ground truth for comparison.

- RNASeqData.BRCA.TCGA.txt: <br /> Matrix with RNA-seq dataset. Columns represent each breast cancer/normal sample, and rows represent individual genes.
- PAM50.class.microarray.txt: <br /> PAM50 classification for part of the samples in the RNA-seq dataset that also have microarray data for the same samples. This can be used as the ground truth for this set of samples.
- SurvivalData.txt: <br /> This matrix contains information about the time until each patient either died or the time until the last follow-up (last known alive). It also contains information about whether the patient still had a tumor at the time of death or the last follow-up.
- PAM50.genes.txt: <br /> Set of genes included in the PAM50 classifier. This set of 50 genes has previously been selected based on their ability to discriminate the five breast cancer intrinsic subtypes using microarray data.

## Analysis steps
#### 1. Data normalization: 
- Removed the no-expression genes.
- Gene expression normalization and log-transformation.
#### 2. Feature selection:
- Applied one-vs-rest t-test for each subtype and picked 69 significant genes.
- Applied pari-wise t-test between selected subtype pairs.
- Finally extracted 87 genes as features for next-step classification.
