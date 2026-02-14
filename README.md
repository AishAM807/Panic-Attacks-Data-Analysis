# 📊Panic Attack Data Analysis

### Dashboard Link : 
### Data Source: Snowflake

## Report Snapshot (Power BI DESKTOP)
<img width="875" height="490" alt="Image" src="https://github.com/user-attachments/assets/3dcb8998-3e25-4570-a388-543bcec11361" />

## Problem Statement:

The objective of this project is to analyze panic attack–related patient data and transform complex health records into an interactive Power BI dashboard that:

- Identifies patterns and correlations between lifestyle factors and panic attack occurrence

- Detects high-risk individuals based on behavioral and physiological indicators

- Evaluates the impact of factors such as sleep, stress, caffeine, and activity levels

- Provides actionable insights to support early intervention and preventive care

This dashboard enables healthcare professionals, counselors, and researchers to make data-driven decisions, recognize triggers earlier, and design better preventive strategies for mental health management.


### 🛠️ Project Methodology

1. Data Extraction (Snowflake Data Warehouse)
The dataset was stored in the Snowflake cloud data warehouse. SQL queries were used to fetch relevant patient records related to panic attack occurrences, physiological indicators, and lifestyle factors.

2. Data Understanding using SQL
Initial data exploration was performed in Snowflake using SQL to understand the structure, schema relationships, and distribution of variables such as heart rate, sleep hours, stress levels, physical activity, and caffeine intake. This step helped identify missing values, inconsistent entries, and potential outliers.

3. Data Connection to Power BI
Snowflake was connected to Power BI Desktop using the native Snowflake connector. The required tables and views were imported into Power BI for further analysis and dashboard development.

4. Data Cleaning and Transformation (Power Query Editor)
The dataset was prepared using Power Query Editor. The following preprocessing steps were performed:

- Handling missing and null values

- Standardizing categorical variables

- Correcting data types (numeric, date/time, categorical)

- Removing duplicate records

- Creating derived columns for analysis

### Step followed:

- Step 1 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 2 : Certain symptom-related fields such as Shortness of Breath and Sweating were originally stored as categorical text values (“Yes”, “No”). These variables were converted into   binary numerical indicators (1 = Yes, 0 = No) using the Conditional Column feature in Power Query Editor.
- Step 3 : A new derived column “HML Panic Score” was created to categorize patients into High, Medium, and Low risk groups based on their Panic Score values. Threshold ranges were   defined to segment individuals according to severity levels.
		
		= Table.AddColumn(#"Changed Type2", "HML_PANIC_SCORE", each if [PANIC_SCORE] <= 4 then "LOW" else if [PANIC_SCORE] >= 8 then "HIGH" else "MEDIUM")

- Step 4 : The first report page was designed using a dedicated “Panic Attack” theme. The canvas background and visual styling were customized to create a healthcare-	   oriented interface and improve visual readability
- Step 5 : A second report page was developed to analyze the number of patients experiencing different panic attack symptoms. Bar chart visualizations were used to  compare the frequency of symptoms such as dizziness, chest pain, sweating, and shortness of breath.
- Step 6 : A new calculated column “Age Group” was created using a DAX IF function to categorize patients into age brackets (for example: Youth, Adult, Senior) based  on the existing AGE column.
- Step 7 : for creating a new column following DAX expression was written;

		age_group = IF('PANIC_ATTACK_DATA '[AGE] <= 17, "Child",
                     IF('PANIC_ATTACK_DATA '[AGE] <= 24, "Adolescent",
                        IF('PANIC_ATTACK_DATA '[AGE] <= 44,"Adult", "Senior")))


       
- Step 8 : A third report page was created to examine lifestyle factors associated with panic attacks. Area chart visualizations were used to analyze:

  - Number of patients by sleep duration (hours)

  - Distribution of panic attack duration (in minutes)

  - Number of patients by weekly drink consumption


- Step 9 : Interactive slicers were implemented to allow dynamic exploration of the data. Users can filter the dashboard by HML Panic Score (risk level), Gender, 	   Trigger Reason, and Medical History.
- Step 10 : The final report page presents key summary metrics including Average Sleep Hours, Average Panic Score, and Panic Attack Frequency. Bar chart visualizations were used to compare these measures across different trigger reasons, such as Caffeine, PTSD, Social Anxiety, and Stress.
- Step 11 : A DAX measure was created to calculate the percentage of patients experiencing dizziness out of the total patient population.
	    The total number of patients was computed using the COUNTROWS function, and a filter condition was applied to isolate records where the Dizziness symptom was present.
	    
  - Following DAX expression was written for the same,
		
		    % patients_dizziness = DIVIDE(COUNTROWS(FILTER('PANIC_ATTACK_DATA ','PANIC_ATTACK_DATA '[DIZZINESS] = TRUE())), COUNTROWS('PANIC_ATTACK_DATA '))
		
		
- Step 12 : A card visual was used to represent Percentage of patients dizziness:
<img width="196" height="94" alt="Image" src="https://github.com/user-attachments/assets/b5aafb0d-1ba5-44b3-bac0-bf2aa8365a0d" />

- Step 13 : The report was then published to Power BI Service.

## Report Snapshot (Power BI DESKTOP)


# Insights
Following inferences can be drawn from the dashboard;

### [1] Total Number of patients = 1200
	
- Number of patients having Dizziness = 620

- Number of patients having Chest Pain = 713

- Number of patients having Sweating = 836

- Number of patients having Shortness Of Breathing = 746



### [2] Caffeine Trigger

- Adolescent: Sleep ≈ 6.7 hrs, Panic Score ≈ 6.44, Attack Frequency ≈ 4.74

- Adult: Sleep ≈ 6.5 hrs, Panic Score ≈ 4.87, Frequency ≈ 4.14

- Senior: Sleep ≈ 6.6 hrs, Panic Score ≈ 5.58, Frequency ≈ 4.82

- Caffeine causes frequent but moderate severity panic attacks. Adolescents show higher panic scores than adults.



### [3] Phobia Trigger

- Adolescent: Sleep ≈ 6.5 hrs, Panic Score ≈ 6.19, Frequency ≈ 4.44

- Adult: Sleep ≈ 6.3 hrs, Panic Score ≈ 5.38, Frequency ≈ 3.79

- Senior: Sleep ≈ 6.5 hrs, Panic Score ≈ 5.48, Frequency ≈ 4.24

- Phobia attacks are situational — moderate panic score but relatively lower frequency.

### [4] PTSD Trigger

- Adolescent: Sleep ≈ 6.4 hrs, Panic Score ≈ 5.50, Frequency ≈ 4.40

- Adult: Sleep ≈ 6.6 hrs, Panic Score ≈ 5.82, Frequency ≈ 5.12 ← Highest

- Senior: Sleep ≈ 6.7 hrs, Panic Score ≈ 5.80, Frequency ≈ 4.35

- PTSD shows the highest panic attack frequency, especially among adults.

### [5] Social Anxiety Trigger

- Adolescent: Sleep ≈ 6.5 hrs, Panic Score ≈ 5.12, Frequency ≈ 4.46

- Adult: Sleep ≈ 6.5 hrs, Panic Score ≈ 5.76, Frequency ≈ 4.67

- Senior: Sleep ≈ 6.6 hrs, Panic Score ≈ 5.98, Frequency ≈ 4.12

- Social anxiety produces consistent panic severity across all ages.

