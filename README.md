QSAR-Based Prediction of Acetylcholinesterase Inhibitory Activity

Machine-learning QSAR project comparing molecular fingerprints and descriptors to predict the bioactivity of compounds targeting acetylcholinesterase (AChE), a therapeutic target investigated in Alzheimer's disease research.
> **Project type:** Academic team project — Computer-Aided Drug Design (CADD), Semester 2  
> **Team:** CADD NEXUS  
> **Institution:** Digital University Kerala  
> **Tools:** Python, RDKit, PaDEL-Descriptor/PaDELpy, pandas, NumPy, scikit-learn, Matplotlib, Seaborn
Overview
This project develops and evaluates regression models that predict the pIC₅₀ activity of compounds from their SMILES representations. Experimental activity data were obtained from BindingDB and curated before molecular features were generated.
Three molecular representations were compared:
Morgan fingerprints: radius 2, 2,048-bit representation generated with RDKit.
RDKit molecular descriptors: physicochemical and structural descriptors.
PaDEL descriptors: a broader set of molecular descriptors, filtered before model training.
The workflow covers data curation, molecular representation, model training, cross-validation, test-set evaluation, feature-importance analysis, and exploratory prediction on compounds similar to donepezil.
Objectives
Curate AChE inhibitor data containing molecular SMILES and experimental IC₅₀ values.
Remove missing, duplicate, invalid, and unusable records.
Transform IC₅₀ values into pIC₅₀ values for regression.
Generate Morgan fingerprints, RDKit descriptors, and PaDEL descriptors.
Compare multiple regression algorithms using cross-validation and held-out test data.
Examine descriptor importance and explore predictions for new compounds.
Methodology
Data acquisition: AChE-related compound activity data from BindingDB.
Curation: select relevant fields, handle missing values and duplicates, parse IC₅₀ values, and validate SMILES with RDKit.
Target transformation: convert usable IC₅₀ measurements to pIC₅₀. Confirm the units and treatment of censored values (such as `>` or `<`) before reproducing the analysis.
Feature engineering: generate Morgan fingerprints, RDKit descriptors, and PaDEL descriptors; filter unsuitable or low-variance features.
Model development: compare Linear Regression, Ridge, Lasso, K-Nearest Neighbors, Support Vector Regression, Random Forest, Gradient Boosting, and Extra Trees where implemented for the corresponding feature set.
Evaluation: use an 80:20 train/test split and five-fold cross-validation; report R² and RMSE, and include MAE if calculated.
Interpretation: compare representations and inspect feature importance for the PaDEL/Extra Trees model.
Exploratory screening: rank predictions for a set of donepezil-like compounds. These are computational predictions and require independent experimental validation.
Selected Results
The submitted report reports the following best test-set results for each feature representation:
Feature representation	Best model	Test R²	Test RMSE
Morgan fingerprints	Random Forest	0.7283	0.8041
PaDEL descriptors	Extra Trees	0.6942	0.8001
RDKit descriptors	Support Vector Regression (SVR)	0.6526	0.8951
Interpretation: Morgan fingerprints produced the highest reported test R², while PaDEL descriptors produced the lowest reported RMSE among these three best-performing models. R² and RMSE measure different aspects of performance, so neither result alone establishes that a compound is a safe or effective drug.
These figures are transcribed from the academic report and should be reproduced from the final notebooks before being treated as independently verified results.


Install the project dependencies:
```bash
pip install -r requirements.txt
```
RDKit and PaDEL-Descriptor can have environment-specific installation requirements. Verify that the installed versions work in your environment and document any additional PaDEL Java/software setup.
Reproducing the Analysis
Obtain the relevant AChE activity dataset from BindingDB and read `data/README.md` for the expected filename and columns.
Run the notebooks in numerical order.
Confirm that preprocessing and feature generation are fitted without using held-out test data.
Review the generated model-comparison tables and figures in `results/`.
Record the software versions, random seeds, data filters, and final metrics.
The repository should contain the code and instructions needed to reproduce the analysis. If the original raw dataset cannot be redistributed, provide the source link and data-preparation instructions instead of committing it.
Limitations and Responsible Use
This is an academic computational study, not a validated clinical or drug-development tool.
Predicted pIC₅₀ values are estimates of activity against the modeled target; they do not establish clinical efficacy, safety, selectivity, brain penetration, or suitability for treating Alzheimer's disease.
Experimental measurements may differ across assays and sources.
The treatment of IC₅₀ values reported with inequality signs can affect the target values; document the exact handling used.
Similar compounds can receive similar predictions, and the model may be unreliable for molecules outside the training-data chemical space.
Predictions require independent validation and should not be interpreted as medical advice.
Team and Acknowledgements
This work was completed by Team CADD NEXUS as part of the Computer-Aided Drug Design course at Digital University Kerala.

BindingDB: https://www.bindingdb.org/
RDKit documentation: https://www.rdkit.org/docs/
scikit-learn documentation: https://scikit-learn.org/stable/
PaDEL-Descriptor: https://github.com/dataprofessor/padel
Disclaimer
For educational and research purposes only. This repository does not provide medical advice and must not be used to make clinical decisions.
