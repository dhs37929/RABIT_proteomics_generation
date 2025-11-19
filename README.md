# RABIT: Real-world AI-based Biomarker Inference Technology
RABIT is a machine learning model that generates high-fidelity in silico plasma proteomics consisting of 2923 proteins from OMOP-formatted EHR data alone at the cost of electricity. The 2923 RABIT proteins can then be used for any downstream analysis typically conducted using measured proteomics. Here (future link to manuscript), we demonstrate RABIT proteins encode clincially and biologically meaningful information through vignettes exploring their use in disease onset prediction across hundreds of diseases, organ specific aging clocks, and anti-TNF response prediction in rheumatoid arthritis patients.  

## Overview
This repository contains the full codebase for training the RABIT model and running all downstream analyses presented in our manuscript. RABIT was trained on the UK Biobank’s cohort of ~50,000 individuals with paired EHR and plasma proteomics, enabling generation of high-fidelity in silico protein profiles. These RABIT-inferred proteins show strong concordance with measured proteomes including sex-specific differences and age-related trajectories at the single-protein level.

We further validated RABIT’s ability to encode clincially and biologically useful information by demonstrating significant improvements in disease-onset prediction over EHR-only models across two independent validation cohorts spanning the UK and Stanford Health Care. To illustrate its potential impact, we also performed an “instant” retrospective cohort study predicting anti-TNF response in rheumatoid arthritis using 687 patients, a cohort multiple times larger than most published analyses, thereby enhancing both predictive performance and the discovery of mechanistic biomarker candidates.

RABIT was designed to exponentially scale and accelerate biomedical research, with broad applicability across diseases and clinical fields. Our goal is for RABIT to shift the paradigm of high-dimensional biological research by removing the traditional logistical and financial barriers to enable creative biomedical research across all domains. 

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

Due to HIPAA constraints, we cannot share the actual EHR or protein data that were used for the study. Due to UK Biobank's policies, we cannot share their EHR or measured proteomic data. However, the "example_files" folder included in this respository contains randomized synthetic data. This data has been stripped of any patient identifiers and its values are completely random. The purpose of the data is to illustrate the format of the data generated/expected.

## Descriptions of Contents
- The "RABIT_model_training.ipynb" file contains the code to train the RABIT model. The training consists of two parts: generating a dense 768-dimensional representation of EHR for each patient followed by training a multilayer perceptron training head for each protein. The EHR is cut to include all data up-to-and-including the day the measured proteomics were collected. The measured protein panel used for training (from UK Biobank) consisted of 2923 proteins measured on the Olink platform. Our code uses a time-to-event EHR foundation model called [MOTOR](https://huggingface.co/StanfordShahLab/motor-t-base) to create the dense representations. However, the pipeline is designed to run with any dense representation you wish to use. Using our example data, the code will run using the "ehr_representations_randomized" (simulating the EHR dense representation generated from OMOP tables) and "measured_proteomics_randomized" (simulating the panel of measured proteins to predict) files. These synthetic data placeholders can be replaced with OMOP data from the [UK Biobank](https://www.ukbiobank.ac.uk/use-our-data/apply-for-access/). Data from Stanford University is owned by Stanford University. Access to this data must be requested and approved by the institution and the appropriate Institutional Review Boards (IRBs).


- The "disease_onset_model_training.ipynb" file provides the code used to train the 5 year disease onset prediction models shown in Figure 2. The trained models were frozen and validated on two independent validation cohorts, a ~450,000 patient cohort from the UK and a ~1,000,000 cohort from Stanford Health Care. 

- The "biological_validation.ipynb" file provides the code used to conduct biological validations using knowledge graphs and genome-wide association studies shown in Figure 3. The PrimeKG knowledge graph used can be downloaded from the original study: [Chandak et al](https://dataverse.harvard.edu/citation?persistentId=doi:10.7910/DVN/IXA7BM). 

- The "aging_clock_organ_specific.ipynb" file provides the code used for the organ-specific aging anlaysis shown in Figure 4. The organ-specific signatures can be downloaded from the original study: [Oh et al](https://www.nature.com/articles/s41591-025-03565-2).

- The "antitnf_instant_cohort_study.ipynb" file provides the code used to train and analyze models for predicting anti-TNF therapy response in rheumatoid arthritis patients shown in Figure 5. 


