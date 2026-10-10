# QSAR-Based Prediction of Alzheimer's Disease Bioactivity Using Morgan Fingerprints and Molecular Descriptors with Machine Learning

## About the Project

Alzheimer's disease is a progressive neurodegenerative disorder associated with memory loss and cognitive decline. Acetylcholinesterase (AChE) is an important therapeutic target in Alzheimer's disease research because it breaks down acetylcholine, a neurotransmitter involved in memory and learning.

This project aims to develop machine learning-based Quantitative Structure–Activity Relationship (QSAR) models to predict the bioactivity of chemical compounds targeting AChE. The models use molecular structures represented as SMILES strings and convert them into numerical features using molecular fingerprints and molecular descriptors.

The project compares three molecular representation techniques: Morgan fingerprints, RDKit molecular descriptors, and PaDEL molecular descriptors. Multiple machine learning regression algorithms are trained and evaluated to identify the best-performing approach for predicting pIC50 values.

This work was carried out by Team CADD NEXUS as part of the Computer-Aided Drug Design course in the MSc Data Science and Bio AI program at Digital University Kerala.

## Aim

To develop and evaluate machine learning-based QSAR models for predicting the pIC50 values of compounds targeting acetylcholinesterase using molecular features derived from SMILES representations.

## Objectives

- Collect experimentally measured AChE bioactivity data from BindingDB.
- Clean and preprocess the dataset by handling missing values, duplicate compounds, invalid SMILES, and unusable IC50 measurements.
- Convert IC50 values into pIC50 values for regression modelling.
- Generate Morgan fingerprints using RDKit.
- Calculate molecular descriptors using RDKit and PaDEL-Descriptor.
- Develop and compare multiple machine learning regression models.
- Evaluate model performance using R², RMSE, and cross-validation.
- Identify the most suitable molecular representation and regression algorithm.
- Analyze important molecular descriptors associated with predicted bioactivity.
- Explore the prediction of AChE inhibitory activity for new compounds similar to Donepezil.

## Dataset

The experimental bioactivity dataset was obtained from BindingDB, a database containing experimentally measured protein–ligand binding affinity information.

Source: https://www.bindingdb.org/

The original dataset contained approximately 9,388 records and included molecular structures, IC50 measurements, compound identifiers, and other metadata.

After data cleaning and preprocessing, approximately 6,641 compounds were retained with usable pIC50 values. Invalid molecular structures were subsequently removed during molecular validation.

The main information used for modelling included:

- SMILES: textual representation of the chemical structure.
- IC50: concentration required to inhibit a biological target by 50%.
- pIC50: logarithmic representation of IC50 used as the prediction target.
- BindingDB Reactant Set ID: compound identifier.

## Methodology

### 1. Data Collection and Preprocessing

The dataset was obtained from BindingDB and processed using Python and pandas. Relevant columns were selected, missing values were removed, and duplicate SMILES entries were filtered.

IC50 measurements were converted into numeric values, and records that could not be processed were excluded. The IC50 values were transformed into pIC50 values to establish the regression target. Molecular structures were validated using RDKit, and invalid SMILES representations were removed.

### 2. Molecular Feature Extraction

Three molecular representation techniques were used to convert chemical structures into numerical features suitable for machine learning.

**Morgan Fingerprints**

Morgan fingerprints were generated using RDKit with a radius of 2 and a fingerprint length of 2,048 bits. These fingerprints represent local atomic environments and molecular substructures. Zero-variance features were removed before model training.

**RDKit Molecular Descriptors**

RDKit was used to calculate molecular descriptors representing physicochemical and structural properties. Features with excessive missing values and low variance were filtered, resulting in a reduced descriptor set for modelling.

**PaDEL Molecular Descriptors**

PaDEL-Descriptor was used to generate a large collection of molecular descriptors through the PaDELpy interface. Batch processing was used to handle the compounds. Missing and infinite values, unsuitable descriptors, and zero-variance features were filtered. Correlation-based feature reduction was also performed to reduce redundancy.

### 3. Machine Learning Model Development

Multiple regression algorithms were implemented to learn the relationship between molecular features and pIC50 values.

The algorithms included:

- Linear Regression
- Ridge Regression
- Lasso Regression
- K-Nearest Neighbors (KNN)
- Support Vector Regression (SVR)
- Random Forest Regressor
- Gradient Boosting Regressor
- Extra Trees Regressor

The dataset was divided into training and testing subsets using an 80:20 split. Five-fold cross-validation was used to assess model performance and stability. Feature scaling was incorporated into the modelling pipelines where appropriate.

### 4. Model Evaluation

The models were evaluated using the following metrics:

**R² Score:** Measures how much variation in the target values is explained by the model. Higher values generally indicate better predictive performance.

**Root Mean Squared Error (RMSE):** Measures the magnitude of prediction errors. Lower values indicate smaller errors.

Cross-validation mean R² and standard deviation were also used to compare model performance across different folds.

### 5. Feature Importance Analysis

Feature importance analysis was performed using the Extra Trees model trained on PaDEL descriptors. The most important descriptors were examined to understand which structural and physicochemical properties contributed to the model's predictions.

The reported important features included C2SP3, E1v, nF8Ring, XLogP, nHssNH, apol, CrippenLogP, nF10Ring, ETA_Shape_Y, and maxssCH2.

### 6. Prediction on New Compounds

The developed models were also explored for predicting the bioactivity of compounds structurally similar to Donepezil. Similar compounds were obtained from PubChem, their SMILES representations were processed, and the selected model was used to predict pIC50 values.

The predicted compounds were ranked according to their estimated activity. These results represent computational predictions and require independent experimental validation.

## Results and Model Comparison

The best-performing model for each molecular representation was identified by comparing the reported test-set R² and RMSE values.

| Molecular Representation | Best Model | Test R² | Test RMSE |
|---|---|---:|---:|
| Morgan Fingerprints | Random Forest | 0.7283 | 0.8041 |
| RDKit Descriptors | Support Vector Regression | 0.6526 | 0.8951 |
| PaDEL Descriptors | Extra Trees | 0.6942 | 0.8001 |

Morgan fingerprints combined with Random Forest achieved the highest reported test R², indicating the strongest explained variance among the three selected models.

PaDEL descriptors combined with Extra Trees achieved the lowest reported RMSE among these models. RDKit descriptors combined with SVR also demonstrated predictive capability, although its reported performance was lower than the other two approaches.

The comparison suggests that molecular representation plays an important role in QSAR modelling and that nonlinear algorithms can capture relationships between molecular structure and AChE inhibitory activity.

These metrics are taken from the academic report and have not been independently reproduced here.

## Technologies and Tools Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- RDKit
- PaDEL-Descriptor
- PaDELpy
- Scikit-learn
- Matplotlib
- Seaborn
- BindingDB
- PubChem

## Project Structure

The repository can be organized into the following folders and files:

- README.md – Project overview, methodology, and results.
- notebooks/ – Jupyter notebooks containing data preprocessing, feature extraction, model training, and evaluation.
- data/ – Permitted input data or sample datasets and instructions for obtaining the original dataset.
- results/ – Model evaluation metrics, visualizations, and feature importance results.
- reports/ – Academic project report, subject to permission for public sharing.


## Conclusion

This project demonstrates the application of machine learning and cheminformatics techniques to QSAR modelling for predicting AChE inhibitory bioactivity.

Three molecular representations were compared using multiple regression algorithms. Random Forest with Morgan fingerprints achieved the highest reported test R², while Extra Trees with PaDEL descriptors achieved the lowest reported RMSE among the selected best-performing models.

The findings highlight the importance of molecular feature representation and nonlinear machine learning methods in computational bioactivity prediction. The workflow provides an academic foundation for exploring molecular structure–activity relationships and prioritizing compounds for further investigation.

## Submitted By Team CADD NEXUS

## References

- BindingDB: https://www.bindingdb.org/
- PubChem: https://pubchem.ncbi.nlm.nih.gov/
- RDKit Documentation: https://www.rdkit.org/docs/
- Scikit-learn Documentation: https://scikit-learn.org/stable/
- PaDEL-Descriptor: https://github.com/dataprofessor/padel

## Disclaimer

This project is intended for academic and research purposes only. Predicted bioactivity values do not establish drug safety, clinical effectiveness, or suitability for treating Alzheimer's disease. Experimental validation is required before any potential compound can be considered for further development.
