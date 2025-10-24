# Cognifyz_DA_Task1_TopCuisines
Task 1 of Cognifyz Data Analysis Internship — Top Cuisines Analysis using Python

# 🍽️ Cognifyz Technologies Internship – Task 1 (Top Cuisines Analysis)

This repository contains my **Task 1 submission** for the **Data Analysis Internship** at "Cognifyz Technologies".


## 🎯 Objective
To identify the **Top 3 most common cuisines** and calculate the **percentage of restaurants** serving each cuisine using the given dataset.


## 🧠 Insights
- **North Indian** cuisine is the most popular across restaurants.
- **Chinese** cuisine ranks second, showing wide acceptance.
- **Fast Food** ranks third, reflecting the growth of urban lifestyle and quick service trends.

## 🧩 Dataset Information
- **Total records:** 9,551  
- **Columns used:** `Restaurant ID`, `Restaurant Name`, `Cuisines`  
- **Missing Cuisines:** 9 rows (filled as blank)
- **No duplicate entries found**


## 🧹 Data Cleaning Steps
1. Filled missing cuisines with blank (`fillna('')`)
2. Converted text to lowercase (`.str.lower()`)
3. Removed extra spaces (`.str.strip()`)
4. Unified all separators like `/ | ;` into commas
5. Split multi-cuisine rows into separate entries using `explode()`


## 💻 Technologies Used
- **Python**  
- **pandas** (data manipulation)  
- **matplotlib** (visualization)  
- **Jupyter Notebook / Google Colab**


## 📊 Code Summary
```python
# Load data
df = pd.read_csv("Dataset.csv")

# Clean text
df['Cuisines'] = df['Cuisines'].fillna('').str.lower().str.strip()

# Split and explode
df['Cuisines'] = df['Cuisines'].str.split(',')
df_exp = df.explode('Cuisines')

# Count cuisines
result = (
    df_exp.groupby('Cuisines')['Restaurant ID']
    .nunique()
    .reset_index(name='Restaurant_Count')
    .sort_values('Restaurant_Count', ascending=False)
)

# Top 3 cuisines
top3 = result.head(3)
print(top3)

---
*Created by Komal for the Data Analyst Internship Program.*
