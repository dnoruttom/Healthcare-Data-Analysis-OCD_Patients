# Healthcare Data Analysis: OCD Patients
## Project Overview
This project conducts an analysis of the demographics and clinical data of individuals diagnosed with Obsessive-Compulsive Disorder (OCD). The primary objective is to uncover patterns and insights that can enhance our understanding of OCD. By addressing the identified problem statements, the report endeavors to offer valuable insights into the demographic and clinical profiles of OCD patients, pinpoint potential factors affecting OCD severity, and foster a deeper comprehension of the disorder.

## Problem Statements
### Monthly Patient Count Analysis:
Determine the month-over-month patient count trend to understand any patterns or fluctuations in the number of OCD patients over time.

### Impact of Marital Status on OCD Across Age Groups:
Is there an impact of marital status (Single, Divorced, Married) on OCD severity within different age groups (adult, middle-aged, older)?

### Distribution of Obsession Severity Levels:
Analyze the distribution of patients across various obsession severity levels (Subclinical, Mild, Moderate, Severe and Extreme) to gain insights into the prevalence and severity of OCD symptoms within the patient population.

### Distribution of Compulsion Severity Levels:
Examine the distribution of patients across different compulsion severity levels (Subclinical, Mild, Moderate, Severe, Extreme) to understand the severity and nature of compulsive behaviors among OCD patients.

### Impact of Previous Diagnoses on OCD:
Do previous diagnoses such as Major Depressive Disorder (MDD), Generalized Anxiety Disorder (GAD), Panic Disorder, and Post-Traumatic Stress Disorder (PTSD) impact OCD patients? How many, or what percentage, of patients had these previous diagnoses compared to those with no prior diagnosis?
## SQL Queries with Outcome
### Monthly Patient Count Analysis:
```sql
SELECT
 YEAR(`OCD Diagnosis Date`) AS Year, 
 MONTH(`OCD Diagnosis Date`) AS  Month, 
 count(*) AS patient_count 
FROM healthcare.ocd_patient_dataset_cleaned
GROUP BY Year, Month
ORDER BY Year, Month;
```
![image](https://github.com/dnoruttom/Healthcare-Data-Analysis-OCD_Patients/assets/98158310/9591bfaf-343c-4bd1-af12-9b31be73664d)

### Impact of Marital Status on OCD Across Age Groups:
```sql
SELECT 
 CASE 
  WHEN Age <= 35 THEN 'adult'
  WHEN age <= 55 THEN 'middle_aged'
  ELSE 'older' END AS age_group,
 `Marital Status`,
count(*) AS patient_count
FROM healthcare.ocd_patient_dataset_cleaned
GROUP BY age_group, `Marital Status`
ORDER BY patient_count DESC;
```
![image](https://github.com/dnoruttom/Healthcare-Data-Analysis-OCD_Patients/assets/98158310/0c71258c-e131-4c0d-bcd1-01d90798b448)

### Distribution of Obsession Severity Levels:
```sql
SELECT 
 CASE 
  WHEN `Y-BOCS Score (Obsessions)` <= 7 THEN 'subclinical'
  WHEN `Y-BOCS Score (Obsessions)` <= 15 THEN 'mild'
  WHEN `Y-BOCS Score (Obsessions)` <= 23 THEN 'moderate'
  WHEN `Y-BOCS Score (Obsessions)` <= 31 THEN 'severe'
  ELSE 'extreme' END AS obsession_severity_level,
 count(*) AS patient_count
FROM healthcare.ocd_patient_dataset_cleaned
GROUP BY obsession_severity_level
ORDER BY patient_count DESC;
```
![image](https://github.com/dnoruttom/Healthcare-Data-Analysis-OCD_Patients/assets/98158310/3750160b-a531-4b25-bb07-953d960e9438)

### Distribution of Compulsion Severity Levels:
```sql
SELECT
 CASE
  WHEN `Y-BOCS Score (Compulsions)` <= 7 THEN 'subclinical'
  WHEN `Y-BOCS Score (Compulsions)` <= 15 THEN 'mild'
  WHEN `Y-BOCS Score (Compulsions)` <= 23 THEN 'moderate'
  WHEN `Y-BOCS Score (Compulsions)` <= 31 THEN 'severe'
  ELSE 'extreme' END AS compulsion_severity_level,
 count(*) AS patient_count
FROM healthcare.ocd_patient_dataset_cleaned
GROUP BY compulsion_severity_level
ORDER BY patient_count DESC;
```
![image](https://github.com/dnoruttom/Healthcare-Data-Analysis-OCD_Patients/assets/98158310/34234840-25bb-451d-8c96-09ddd05ae957)

### Impact of Previous Diagnoses on OCD:
```sql
SELECT 
  (SUM(CASE WHEN `Previous Diagnoses` IN ('MDD', 'PTSD', 'Panic Disorder','GAD') THEN 1 ELSE 0 END)) AS Previously_diagnosed,
  (SUM(CASE WHEN `Previous Diagnoses` = 'None' THEN 1 ELSE 0 END)) AS No_Prior_Diagnosis,
  (SUM(CASE WHEN `Previous Diagnoses` IN ('MDD', 'PTSD', 'Panic Disorder','GAD') THEN 1 ELSE 0 END))/COUNT(*) AS Previously_diagnosed_Percentage,
  (SUM(CASE WHEN `Previous Diagnoses` = 'None' THEN 1 ELSE 0 END))/COUNT(*) No_Prior_Daignosis_Percentage
FROM healthcare.ocd_patient_dataset_cleaned;
```
![image](https://github.com/dnoruttom/Healthcare-Data-Analysis-OCD_Patients/assets/98158310/d04498b6-0d24-4f0d-aa94-88766ffe902c)

## Findings: 
Dashboard
![image](https://github.com/dnoruttom/Healthcare-Data-Analysis-OCD_Patients/assets/98158310/0f11b832-5df2-4225-8a75-d02c3468a1f8)

## Tools and Technologies
This project utilized the following tools and technologies:

- **Jupyter Notebook**: Data Cleaning.
- **Power Query**: Data transformation and analysis using Power Query Editor, DAX and Measures. 
- **MySQL**: Data Analysis.
- **Power BI**: For creating interactive visualizations and dashboards.
