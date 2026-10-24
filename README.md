# 🧬 Hypoxic vs. Normoxic Cancer Cell Classification Using Single-Cell RNA-seq and Deep Learning

A computational genomics and machine learning project that analyzes single-cell RNA sequencing (scRNA-seq) data to investigate gene expression differences between cancer cells grown under hypoxic (low oxygen) and normoxic (normal oxygen) conditions.

The project combines exploratory data analysis, gene expression preprocessing, statistical testing, feature selection, dimensionality reduction, and neural network classification to investigate whether gene expression profiles can distinguish hypoxic from normoxic cancer cells.

Using Smart-seq and Drop-seq datasets, the notebook explores gene expression variability, identifies potentially hypoxia-associated genes, and experiments with deep learning models for binary classification.

---

## ✨ Features

- 🧬 Single-cell RNA-seq data analysis
- 🔬 Smart-seq and Drop-seq data processing
- 📊 Exploratory data analysis of gene expression
- 🧹 Missing-value and duplicate-gene inspection
- 🔍 Detection of zero-expression cells
- 📉 Gene expression sparsity analysis
- 🧪 Cell quality filtering
- ⚖️ Library-size normalization
- 🧬 Differential gene expression analysis
- 📈 Statistical significance testing
- 🔢 Benjamini–Hochberg multiple-testing correction
- 🎯 Highly variable and significant gene selection
- 🧠 Principal Component Analysis (PCA)
- 📊 Interactive three-dimensional PCA visualization
- 🤖 Neural network-based binary classification
- ⚙️ Hyperparameter tuning with GridSearchCV
- 📉 Training and validation performance visualization

---

## 🎯 Project Objective

Cancer cells can adapt to low-oxygen environments by changing their gene expression. Studying these changes can help researchers investigate the biological mechanisms associated with hypoxia.

The main objective of this project is to explore whether single-cell gene expression profiles contain useful information for distinguishing cells grown under two oxygen conditions:

- **Hypoxia:** Reduced oxygen availability (1% O₂)
- **Normoxia:** Normal oxygen availability (21% O₂)

The project investigates the following questions:

- How does gene expression vary between individual cells?
- How sparse are single-cell RNA-seq expression matrices?
- Which genes show statistically significant expression differences between hypoxic and normoxic conditions?
- Can dimensionality reduction reveal patterns in gene expression?
- Can neural networks classify cells according to their oxygen treatment condition?
- Which genes may be biologically relevant to the cellular response to hypoxia?

---

## 🏗️ Project Architecture

```text
Single-Cell RNA-seq Data
          │
          ▼
    Data Loading
  Smart-seq / Drop-seq
          │
          ▼
 Exploratory Data Analysis
          │
          ▼
   Quality Filtering
          │
          ▼
 Gene Expression Normalization
          │
          ▼
 Differential Gene Expression
          │
          ▼
 Feature Selection
          │
          ├───────────────┐
          ▼               ▼
    PCA Analysis     Neural Networks
          │               │
          ▼               ▼
   Visualization    Binary Classification
                          │
                          ▼
               Hypoxic vs. Normoxic
                   Cell Prediction
```

---

## 📊 Dataset

The project uses single-cell gene expression count matrices and metadata containing information about individual cells and their experimental conditions.

Each **column** in the expression matrix represents a sequenced cell, while each **row** represents a gene. The matrix entries contain gene expression read counts.

### Experimental conditions

| Condition | Description |
|---|---|
| Hypoxia | Cells grown under reduced oxygen conditions |
| Normoxia | Cells grown under normal oxygen conditions |

### Sequencing approaches

**Smart-seq**

The notebook analyzes gene expression counts and cell metadata, including the experimental condition associated with each cell.

**Drop-seq**

The notebook processes a separate gene expression dataset and constructs binary labels from cell identifiers to distinguish hypoxic from normoxic samples.

### Dataset details

In one Smart-seq analysis section, the notebook reports the following dimensions after separating cells by condition:

- Genes: 23,342
- Hypoxic cells: 110
- Normoxic cells: 99

These dimensions apply to that particular analysis stage and should not be interpreted as the total size of every dataset used in the notebook.

**Data-source note:** The notebook's introductory text mentions HCC1086 and MCF7, while several file paths and model sections refer to HCC1806. The exact cell-line and dataset mapping should be verified before publishing definitive dataset descriptions.

---

## 🔬 Methodology

### 1. Exploratory Data Analysis

The notebook examines the structure and characteristics of the expression matrices.

Key analyses include:

- Dataset dimensions and data types
- Missing-value inspection
- Duplicate gene expression profiles
- Cell-to-cell correlation analysis
- Gene expression distributions
- Zero-count patterns and sparsity
- Mean and variance relationships
- Skewness and kurtosis of gene expression

These analyses help characterize the challenges of working with high-dimensional, sparse single-cell data.

### 2. Cell Quality Control and Filtering

The notebook investigates potential low-quality cells using:

- Total read counts per cell
- Number of genes expressed per cell
- Expression distribution patterns
- Mitochondrial RNA proportion

Cells identified as potentially problematic are filtered according to the notebook's selected thresholds.

### 3. Gene Expression Normalization

The project explores library-size normalization to account for differences in sequencing depth between cells.

It also applies logarithmic transformation using \(\log(x+1)\) in the gene-selection workflow and discusses how normalization can influence expression variability and downstream comparisons.

### 4. Differential Gene Expression Analysis

The notebook compares gene expression between hypoxic and normoxic cells.

It implements two statistical approaches:

- **Welch's/t-test-based analysis:** Used in the normalized expression workflow to calculate p-values.
- **Mann–Whitney U test:** Used in the nonparametric analysis of unnormalized expression data.

The notebook also implements Benjamini–Hochberg correction to adjust for multiple hypothesis testing and reduce false-positive findings.

### 5. Feature Selection

Genes are selected based on their statistical significance and expression characteristics.

The notebook explores count-per-million (CPM) filtering and adjusted p-values to identify genes that may be informative for distinguishing the two experimental conditions.

It also discusses hypoxia-associated genes, including:

- **NDRG1**
- **PGK1**

These genes are highlighted in the notebook's discussion as potentially relevant to the cellular response to hypoxia. Their selection in this exploratory analysis does not independently establish a biological association in the studied samples.

### 6. Dimensionality Reduction and Visualization

Principal Component Analysis (PCA) is used to explore patterns in gene expression.

The notebook includes an interactive three-dimensional PCA visualization based on the first three principal components, with points colored according to experimental labels.

### 7. Neural Network Classification

The final sections experiment with feed-forward neural networks for binary classification.

The notebook includes:

- Dense neural network architectures
- ReLU hidden-layer activations
- Sigmoid output layers
- Binary classification labels
- Stochastic Gradient Descent and RMSprop optimizers
- Training and validation curves
- Model evaluation
- Dropout and L2 regularization experiments
- Weight-initialization hyperparameter search using GridSearchCV

The goal is to investigate whether gene expression profiles can predict the oxygen condition under which each cell was grown.

---

## 📈 Experimental Results

The notebook contains neural network evaluation outputs for its HCC1806-labelled Smart-seq and Drop-seq sections.

| Experiment | Reported evaluation accuracy |
|---|---:|
| Smart-seq neural network | 94.89% |
| Drop-seq neural network | 80.29% |

These values are the accuracies printed by the notebook's `model.evaluate()` calls.

**Important:** They should be treated as preliminary experimental results, not as proof of reliable classification performance. The notebook requires further verification of data splits, label alignment, preprocessing consistency, and model configuration before these scores can be interpreted as comparable or generalizable results.

---

## 🛠️ Tech Stack

### Programming and Data Analysis

- Python
- Pandas
- NumPy
- SciPy
- Statsmodels

### Statistical Analysis

- Student's and Welch's t-tests
- Mann–Whitney U test
- Benjamini–Hochberg correction
- Correlation analysis
- Descriptive statistics

### Machine Learning and Deep Learning

- Scikit-learn
- TensorFlow
- Keras
- Artificial Neural Networks
- Principal Component Analysis
- GridSearchCV

### Visualization

- Matplotlib
- Seaborn
- Plotly
- JupyterDash

### Environment

- Google Colab
- Jupyter Notebook
- Google Drive for dataset access

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/humairyousaf6/Hypoxic-vs-Normoxic-Cancer-Cell-Classification.git
cd Hypoxic-vs-Normoxic-Cancer-Cell-Classification
```

### 2. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn tensorflow plotly jupyter
```

Some notebook cells use Google Colab-specific commands and JupyterDash. Depending on the environment, additional compatibility adjustments may be necessary.

### 3. Prepare the Dataset

The notebook references files stored in Google Drive, including expression matrices and metadata files such as:

```text
HCC1806_SmartS_Unfiltered_Data (1).txt
HCC1806_SmartS_MetaData.tsv
HCC1806_SmartS_Filtered_Normalised_3000_Data_train.txt
HCC1806_Filtered_Normalised_3000_Data_train.txt
```

Place the required datasets in an accessible location and update the file paths in the notebook.

The example filenames above reflect paths referenced in the notebook; they are not necessarily included in the repository.

### 4. Run the Notebook

Open the notebook in Google Colab or Jupyter and execute the cells sequentially.

The workflow proceeds from exploratory data analysis and filtering to differential expression, PCA visualization, and neural network experiments.

---

## 📁 Project Structure

```text
Hypoxic-vs-Normoxic-Cancer-Cell-Classification/
│
├── Hypoxic_vs_Normoxic_Cancer_Cell_Classification_Using_Single_Cell_RNA_Sequencing_and_Machine_Learning.ipynb
├── README.md
├── data/
│   ├── expression_matrices/
│   └── metadata/
└── requirements.txt
```

This is a suggested repository structure. The data directories and dependency file should be added if you choose to organize the repository this way.

Do not upload sensitive or restricted research data without confirming that you have permission to share it.

---

## 🔮 Future Improvements

- [ ] Resolve cell-line and dataset naming inconsistencies.
- [ ] Make dataset loading independent of personal Google Drive paths.
- [ ] Validate cell labels against the metadata using explicit cell identifiers.
- [ ] Use stratified train, validation, and test splits.
- [ ] Prevent data leakage during feature selection and normalization.
- [ ] Correctly configure binary cross-entropy loss for sigmoid outputs.
- [ ] Compare neural networks with logistic regression, Random Forest, and gradient boosting.
- [ ] Evaluate precision, recall, F1-score, ROC-AUC, and confusion matrices.
- [ ] Validate performance using independent samples or appropriate grouped splits.
- [ ] Investigate differential expression with established single-cell analysis workflows.
- [ ] Add reproducible configurations and random seeds.
- [ ] Improve visualization of selected genes and biological pathways.
- [ ] Package the analysis into a reproducible pipeline.

---

## ⚠️ Limitations

This project is an exploratory computational genomics and machine learning study, not a clinically validated cancer diagnostic system.

The notebook's reported evaluation accuracies require further validation. In particular, the data preparation, label mapping, train/validation/test partitioning, and neural network loss configuration should be reviewed before drawing conclusions about model reliability.

The differential expression findings are exploratory and should not be interpreted as definitive biological discoveries without independent validation.

---

## 👨‍💻 Author

**Muhammad Humair**

AI/ML & Automation Engineer

- Python
- Machine Learning
- Deep Learning
- Computational Genomics
- Bioinformatics
- Single-Cell RNA Sequencing
- Statistical Analysis
- Data Visualization

---

## ⭐ Project Highlights

- 🧬 Single-cell RNA-seq analysis
- 🔬 Smart-seq and Drop-seq workflows
- 🧹 Cell quality control and normalization
- 📊 Differential gene expression
- 🎯 Statistical feature selection
- 🧪 Multiple-testing correction
- 📉 PCA-based visualization
- 🧠 Neural network classification
- ⚖️ Hypoxic vs. normoxic condition analysis
- 🔍 Exploratory investigation of hypoxia-associated genes
