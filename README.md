# Zomato-Restaurant-Analysis-Dashboard-
Zomato Restaurant Analysis Dashboard – November 2025

# 🍽️ Zomato Restaurant Analysis Dashboard – November 2025

This project demonstrates a complete data analysis workflow using Python (Google Colab) for data cleaning and Power BI for dashboard creation. It explores restaurant ratings, votes, online ordering behavior, and cost trends from Zomato’s dataset.

---

## 📌 Objective

To analyze customer engagement and restaurant performance across various categories using real-world data. The goal is to:
- Clean and transform raw data
- Visualize key metrics and trends
- Build an interactive dashboard for business insights

---

## 📦 Dataset Overview

- **Source**: Zomato restaurant dataset (uploaded manually)
- **Format**: CSV
- **Key Columns**:
  - `name`: Restaurant name
  - `online_order`: Whether online ordering is available
  - `book_table`: Whether table booking is available
  - `rate`: Customer rating (e.g., 4.1/5)
  - `votes`: Number of votes received
  - `approx_cost(for two people)`: Estimated cost
  - `listed_in(type)`: Restaurant type (e.g., Cafes, Dining, Buffet)

---

## 🧪 Step 1: Data Cleaning in Google Colab

### ✅ Tasks Performed:
- Removed `/5` from `rate` column and converted to float
- Converted cost column to numeric
- Dropped rows with missing critical values
- Exported cleaned dataset for Power BI

### 📄 Google Colab Code Used:

```python
# Import libraries
import pandas as pd
import numpy as np
from google.colab import files

# Upload CSV
uploaded = files.upload()

# Load dataset
df = pd.read_csv('Zomato-Dataset-EDA-New-Modified_18102035.csv')

# Clean 'rate' column
def handleRate(rate):
    if pd.isnull(rate):
        return None
    rate = str(rate).split('/')[0]
    try:
        return float(rate)
    except:
        return None

df['rate'] = df['rate'].apply(handleRate)

# Convert cost to numeric
df['approx_cost(for two people)'] = pd.to_numeric(df['approx_cost(for two people)'], errors='coerce')

# Drop rows with missing values in critical columns
df.dropna(subset=['rate', 'votes', 'approx_cost(for two people)'], inplace=True)

# Export cleaned data
df.to_csv("zomato_cleaned.csv", index=False)
files.download("zomato_cleaned.csv")

