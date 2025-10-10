# 🧬 Bioinformatics – ML Challenge

## 🔍 Data Understanding

---

### 🧑‍⚕️ 1. Clinical Data
- **Patient Attributes:**  
  Include survival status, overall survival months, age at diagnosis, and therapy details.  
- **Sample Attributes:**  
  Provide mapping between patient IDs and biological samples (tumor/normal).  
- **Purpose:**  
  Enables correlation between **genomic profiles** and **clinical outcomes**, forming the foundation for survival and subtype analysis.

---

### 🧫 2. Genomic Alteration Data
- **Copy Number Alterations (CNA):**  
  Used to identify **gene amplifications or deletions** potentially driving tumorigenesis.  
- **Mutation Data (MAF):**  
  Contains **point mutations** and **small insertions/deletions** across key cancer-associated genes.  
- **Gene Panel Matrix:**  
  Acts as a **binary mask** indicating which genes were sequenced or profiled per sample.

---

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

---

## 🔹 Gene Expression Features

~20K gene columns reduced using hybrid techniques:  
1. Variance Threshold → remove low-variance genes  
2. ANOVA F-Test → select statistically significant genes  
3. PCA → capture main variance patterns  
4. RFE (Random Forest) → retain top-ranked features

---

## 🎯 Outcome

- Integrated clinical + gene features  
- Reduced features from 20,639 → 117 informative  
- Noise-free dataset ready for high-accuracy classification





