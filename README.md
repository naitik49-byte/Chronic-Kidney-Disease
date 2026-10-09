# Chronic-Kidney-Disease
Chronic Kidney Disease (CKD) Data Analysis
Cleaning and visualizing a kidney disease patient dataset with Python.
About the project
Chronic kidney disease (CKD) is often found late, and the patient records used to study it are messy. This project takes a raw dataset of 400 patients, cleans it, draws charts from it, and writes a short report on what the charts show.
The project covers:
Data cleaning (missing values, duplicates, data types, outliers)
7 analysis charts and 2 cleaning charts
A short insights report
Dataset
The file kidney_disease.csv has 400 patients (rows) and 26 columns. The last column, classification, tells whether the patient has CKD: 250 patients (62.5%) do and 150 (37.5%) do not.
Group
Columns
Basic details
age, bp (blood pressure)
Urine tests
sg (specific gravity), al (albumin), su (sugar), rbc (red blood cells), pc (pus cells), pcc (pus cell clumps), ba (bacteria)
Blood tests
bgr (blood glucose), bu (blood urea), sc (serum creatinine), sod (sodium), pot (potassium), hemo (hemoglobin), pcv (packed cell volume), wc (white cell count), rc (red cell count)
History and symptoms
htn (hypertension), dm (diabetes), cad (coronary artery disease), appet (appetite), pe (pedal edema), ane (anemia)
Target
classification (ckd or notckd)
Source: add the link where you downloaded the dataset. It appears to be the public Chronic Kidney Disease dataset (UCI Machine Learning Repository / Kaggle).
Data cleaning
Check
What I found
What I did
Missing values
About 1,000 empty cells (10% of the table). 242 of 400 rows have at least one gap.
Filled number columns with the median and text columns with the most common value. Dropping rows would leave only 158 patients.
Duplicates
None.
Nothing to remove.
Data types
pcv, wc and rc are numbers stored as text, and a few cells hold ?. Text labels have hidden tabs and spaces, so ckd and ckd\t looked like two groups.
Converted the three columns to numbers and stripped spaces and tabs from all text columns.
Outliers
The IQR rule flags 51 values in sc, 38 in bu, 36 in bp and 34 in bgr.
Kept them, because very high creatinine and urea are real in kidney failure. Three impossible values (potassium 39 and 47, sodium 4.5) were set to empty and filled with the median.
After cleaning, the table has 400 rows and 25 columns (the id column is dropped) and no missing values.
Charts
#
Question
File
1
How many patients have CKD?
1_class_distribution.png
2
How old are the patients?
2_age_distribution.png
3
Do key test results differ between the two groups?
3_boxplots.png
4
Which features are linked to CKD?
4_correlation_heatmap.png
5
Do health conditions matter?
5_risk_factors.png
6
Can two test results separate the groups?
6_hemo_vs_creatinine.png
7
Does CKD become more common with age?
7_ckd_by_age.png
Two more charts support the cleaning step: A_missing_values.png and B_outliers.png. All charts are in output/figures/.
�
�
�
Key findings
CKD patients have lower hemoglobin (middle value 11.3 against 15.0 g/dL), lower packed cell volume (36% against 45.5%) and lower specific gravity.
Their serum creatinine (2.2 against 0.9 mg/dL) and blood urea (51 against 33.5 mg/dL) are higher.
Hemoglobin has the strongest link with CKD (-0.73), then packed cell volume (-0.67), specific gravity (-0.66) and red cell count (-0.57). Albumin has the strongest positive link (+0.53).
Every patient with hypertension, diabetes, coronary artery disease, poor appetite, pedal edema or anemia is in the CKD group.
The CKD share rises with age: 31% for ages 21 to 40, 62% for 41 to 60 and 78% above 60.
Hemoglobin and serum creatinine together separate the two groups clearly, so a simple model should be able to predict CKD. That is a good next step.