# 🧬 Bioinformatics – ML Challenge

---

## 🔍 Data Understanding


### 🧑‍⚕️ 1. Clinical Data
- **Patient Attributes:**  
  Include survival status, overall survival months, age at diagnosis, and therapy details.  
- **Sample Attributes:**  
  Provide mapping between patient IDs and biological samples (tumor/normal).  
- **Purpose:**  
  Enables correlation between **genomic profiles** and **clinical outcomes**, forming the foundation for survival and subtype analysis.



### 🧫 2. Genomic Alteration Data
- **Copy Number Alterations (CNA):**  
  Used to identify **gene amplifications or deletions** potentially driving tumorigenesis.  
- **Mutation Data (MAF):**  
  Contains **point mutations** and **small insertions/deletions** across key cancer-associated genes.  
- **Gene Panel Matrix:**  
  Acts as a **binary mask** indicating which genes were sequenced or profiled per sample.



### 🧬 3. Transcriptomic & Epigenetic Data
- **mRNA Expression (Raw + Z-Score):**  
  Quantifies **gene expression variation**, valuable for **subtype classification** and **clustering analysis**.  
- **Methylation (Promoters):**  
  Captures **epigenetic regulation** by measuring promoter methylation levels — reflecting **gene silencing** or **activation patterns** in tumor versus normal tissues.

---

### 🔹 Relation between Age of patient and Type of Cancer

![Age vs. Cancer Type](Age_vs_CancerType.png)

---

### 🔹 Cancer Type Distribution

![Cancer Type Distribution](Cancer_Distribution.png)

---

### 🔹 Tumor Size vs Grade

![Grade vs Tumor Size](Grade_vs_Tumor_Size.png)

---

# 🧬 Data Preprocessing Pipeline

To build a robust breast cancer subtype prediction model, the dataset was split into **clinical** and **gene expression** features and processed to ensure quality and reduce dimensionality.

---

## 🔹 Clinical Features

### Numerical Variables  
Examples: AGE, NPI, LYMPH_NODES_EXAMINED_POSITIVE  
- Imputation: Missing values filled using median.  
- Scaling: StandardScaler applied for normalized input.

### Categorical Variables  
Examples: CELLULARITY, CHEMOTHERAPY, HORMONE_THERAPY  
- Encoding: One-Hot for nominal, Ordinal for ordered categories.


## 🔹 Gene Expression Features

~20K gene columns reduced using hybrid techniques:  
1. Variance Threshold → remove low-variance genes  
2. ANOVA F-Test → select statistically significant genes  
3. PCA → capture main variance patterns  
4. RFE (Random Forest) → retain top-ranked features



## 🎯 Outcome

- Integrated clinical + gene features  
- Reduced features from 20,639 → 8363 informative  
- Noise-free dataset ready for high-accuracy classification

---

## 🤖 Model Building and Optimization

### 🌲 Random Forest Classifier  
We chose the **Random Forest** algorithm as our baseline model for classification due to its robustness, interpretability, and high performance on tabular biomedical datasets.  
It is an **ensemble learning** method that constructs multiple decision trees during training and combines their predictions to improve generalization.

#### 🔹 Why Random Forest?
- Handles both **numerical and categorical** data effectively  
- Automatically performs **feature importance ranking**  
- Reduces risk of **overfitting** compared to individual decision trees  
- Works well even with **imbalanced** and **high-dimensional** genomic datasets  
- Provides strong **baseline accuracy** without extensive tuning  

### ⚙️ Hyperparameter Tuning with Grid Search CV  
To further enhance model performance, we applied **Grid Search Cross-Validation (GridSearchCV)** with **5-fold CV** to systematically explore hyperparameter combinations such as:  
- Number of estimators (`100`)  
- Maximum depth of trees (`max_depth`)  
- Minimum samples per split (`min_samples_split`)  
- Criterion (`gini` or `entropy`)  

This process ensures an optimal balance between **bias and variance**, improving model generalization.

### 📈 Model Performance  
After tuning, the optimized Random Forest achieved:  
- **Accuracy:** ~92% on the validation dataset  
- **Precision and Recall:** Both remained consistently high, indicating balanced predictions  
- **Feature Insights:** Top contributing features included key clinical indicators and selected gene expression markers

---

## ⚠️ Challenges Faced

During the project, several challenges were encountered that required careful consideration:

### 1️⃣ Data Segregation and Collection
- The dataset included **clinical, genomic, and transcriptomic features** with different formats and identifiers.  
- Mapping patients to samples and integrating multiple data types required extensive preprocessing and cleaning.  

### 2️⃣ High Dimensionality and Feature Selection
- Gene expression data contained **~20,000 features**, which can lead to **noise and computational overhead**.  
- We applied hybrid dimensionality reduction techniques (Variance Threshold, ANOVA F-Test, PCA, RFE) to retain biologically relevant features.  

### 3️⃣ Model Selection and Overfitting
- Choosing an appropriate model that balances **accuracy and generalization** was critical.  
- Random Forest helped mitigate overfitting, but **hyperparameter tuning** with Grid Search CV was required to achieve optimal performance.  

### 4️⃣ Imbalanced and Missing Data
- Some categorical and numeric clinical variables had **missing values**, while cancer subtypes were **unevenly represented**.  
- Strategies like median imputation, encoding, and careful cross-validation were employed to handle these issues.  

### 5️⃣ Computational Constraints
- Handling high-dimensional omics data required **efficient preprocessing** and **feature reduction** to make model training feasible on standard hardware.  

> 💡 *Overall, addressing these challenges ensured a robust, interpretable, and high-performing breast cancer subtype prediction model.*







