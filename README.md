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
- Gene expression normalization and log transformation.
#### 2. Feature selection:
- Applied one-vs-rest t-test for each subtype and picked 69 significant genes.
- Applied pair-wise t-tests between selected subtype pairs.
- Finally extracted 87 genes as features for later classification.
#### 3. K-fold cross-validation:
- Split the 626 training samples into ten folds. 
- Trained with nine folds and tested with one fold.
- Average the predictions from ten-fold training as the evaluation for the classifier.
#### 4. Machine learning classifiers:
- Support Vector Machine (SVM) with different kernels (linear, polynomial, and radial).
- Random forest (RF).
- K nearest neighbors (KNN) with different neighbor numbers (K = 3,5,7).
#### 5. Prediction and model selection:
- The classifier with the highest accuracy is SVM with radial kernel and trained on the PAM50 genes. 
- The final classifier achieved an average accuracy of 0.9 during the ten-fold training and test.
- Applied the final classifier to the 582 samples with unknown labels to estimate their breast cancer/normal subtypes.
#### 6. Survival analysis:
- Exclude control samples within the TCGA dataset.
- Applied survival analysis on the samples with survival records.
- The conclusion is that basal-like and Luminal A have better prognoses compared with other subtypes.

## Coding pipelines:
The whole analysis pipeline can be found in this report: [Click here]
