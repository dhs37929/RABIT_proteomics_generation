# RABIT: Real-world AI-based Biomarker Inference Technology
RABIT is a machine learning model that generates in silico plasma proteomics from OMOP-formatted EHR data alone. The 2923 proteins that are generated can then be used for any downstream analysis the same way measured proteomics would normally be used. 

## Overview
This repository contains the code used for RABIT model training and its downstream applications as shown in our manuscript. Due to HIPAA constraints, we cannot share the actual EHR or protein data that were used for the study. Due to UK Biobank's policies, we cannot share their EHR or measured proteomic data. RABIT was trained using the UK Biobank's cohort of ~50,000 patients with paired EHR-plasma proteomics whose data can be requested from UK Biobank directly. 

The "example_files" folder included in this respository contains randomized synthetic data. This data has been stripped of any patient identifiers and its values are completely random. The purpose of the data is to illustrate the format of the data generated/expected.

## Installation and Usage
First, clone the repo:
```bash
git clone https://github.com/dhs37929/RABIT_proteomics_generation.git
```
To train RABIT (using random example data provided):
```bash
python RABIT_model_training.ipynb
```
To reproduce downstream analysis (using random example data provided):
```bash
python /any/of/the/notebooks/below
```


## Descriptions of Contents
- The "RABIT_model_training.ipynb" file contains the code to train the RABIT model. The training consists of two parts: generating a dense 768-dimensional representation of EHR for each patient followed by training a multilayer perceptron training head for each protein. The EHR is cut to include all data up-to-and-including the day the measured proteomics were collected. The measured protein panel used for training (from UK Biobank) consisted of 2923 proteins measured on the Olink platform. Our code uses a time-to-event EHR foundation model called [MOTOR](https://huggingface.co/StanfordShahLab/motor-t-base) to create the dense representations. However, the pipeline is designed to run with any dense representation you wish to use. Using our example data, the code should run using the "ehr_representations_randomized" (simulating the EHR dense representation generated from OMOP tables) and "measured_proteomics_randomized" (simulating the panel of measured proteins to predict) files. However, the outputs will not have any meaning. 

- The "disease_onset_model_training.ipynb" file provides the code used to train the 5 year disease onset prediction models shown in Figure 2. The trained models were frozen and validated on two independent validation cohorts, a ~450,000 patient cohort from the UK and a ~1,000,000 cohort from Stanford Health Care. 

- The "biological_validation.ipynb" file provides the code used to conduct biological validations using knowledge graphs and genome-wide association studies shown in Figure 3. The PrimeKG knowledge graph used can be downloaded from the original study: [Chandak et al](https://dataverse.harvard.edu/citation?persistentId=doi:10.7910/DVN/IXA7BM). 

- The "aging_clock_organ_specific.ipynb" file provides the code used for the organ-specific aging anlaysis shown in Figure 4. The organ-specific signatures can be downloaded from the original study: [Oh et al](https://www.nature.com/articles/s41591-025-03565-2).

- The "antitnf_instant_cohort_study.ipynb" file provides the code used to train and analyze models for predicting anti-TNF therapy response in rheumatoid arthritis patients shown in Figure 5. 


