# Hollywood's Most Profitable Stories — Data Analysis & Overview
## 📌 Table of Contents
- [Dataset Overview](#dataset-overview)
- [Data Structure & Schema](#data-structure--schema)
- [Key Summary Statistics](#key-summary-statistics)
- [Data Quality & Cleaning Notes](#data-quality--cleaning-notes)
- [Exploratory Analysis Highlights](#exploratory-analysis-highlights)
- [Getting Started / Python Usage](#getting-started--python-usage)
- [License & Citation](#license--citation)

---## capture
![portfolio overview](images/capture-1 .png)<img width="283" height="211" alt="image" src="https://github.com/user-attachments/assets/26d675fc-ecec-4f85-bd52-deaa83decaaa" />


## 📁 Dataset Overview

* **Filename:** `HollywoodsMostProfitableStories.csv`[cite: 1]
* **Total Rows (Records):** 74[cite: 1]
* **Total Columns:** 8[cite: 1]
* **Time Span:** 2007 – 2011[cite: 1]
* **Primary Focus:** Film profitability ratios, worldwide gross earnings ($ Millions), critical acclaim (Rotten Tomatoes), and audience reception scores[cite: 1].

---

## 📊 Data Structure & Schema

The dataset contains the following 8 attributes[cite: 1]:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Film` | String (Text) | Title of the movie (Unique Identifier)[cite: 1]. |
| `Genre` | Category (Text) | Genre of the film (e.g., *Comedy*, *Drama*, *Romance*, *Animation*, *Action*, *Fantasy*)[cite: 1]. |
| `Lead Studio` | Category (Text) | Major studio or distribution entity responsible for release (e.g., *Fox*, *Warner Bros.*, *Universal*, *Independent*)[cite: 1]. |
| `Audience score %` | Float / Int | Audience rating score percentage (0 – 100%)[cite: 1]. |
| `Profitability` | Float | Ratio of Worldwide Gross return relative to budget/cost[cite: 1]. |
| `Rotten Tomatoes %` | Float / Int | Critical score percentage from Rotten Tomatoes (0 – 100%)[cite: 1]. |
| `Worldwide Gross` | Float | Total worldwide box office gross revenue in **Millions of USD** ($M)[cite: 1]. |
| `Year` | Integer | Release year of the film (2007–2011)[cite: 1]. |

---

## 📈 Key Summary Statistics

Below is an analytical overview of the numeric columns across the **74 recorded movies**[cite: 1]:

| Metric | Audience Score % | Profitability Ratio | Rotten Tomatoes % | Worldwide Gross ($M) | Release Year |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Count** | 73 | 71 | 73 | 74 | 74 |
| **Mean** | 64.14% | 4.74x | 47.36% | $136.35M | 2009 |
| **Std Dev** | 13.65% | 8.29x | 26.24% | $157.07M | 1.35 yrs |
| **Min** | 35.00% | 0.005x | 3.00% | $0.025M | 2007 |
| **25th Percentile** | 52.00% | 1.79x | 27.00% | $32.45M | 2008 |
| **Median (50%)** | 64.00% | 2.64x | 45.00% | $73.20M | 2009 |
| **75th Percentile** | 76.00% | 4.85x | 65.00% | $190.19M | 2010 |
| **Max** | 89.00% | 66.93x | 96.00% | $709.82M | 2011 |

---

## 🛠 Data Quality & Missing Values

Before conducting full downstream modeling or visualization, note the following missing value counts (`NaN`)[cite: 1]:

* `Lead Studio`: 1 missing entry[cite: 1]
* `Audience score %`: 1 missing entry[cite: 1]
* `Rotten Tomatoes %`: 1 missing entry[cite: 1]
* `Profitability`: 3 missing entries[cite: 1]

### Recommended Handling:
* **Imputation / Removal:** Missing numerical fields can be imputed with median values grouped by `Genre` or removed if performing standard regression/correlation tasks.
* **Column Formatting:** Note the double space in `Audience  score %` when accessing via key in Python (`df['Audience  score %']`)[cite: 1]. Re-naming columns for standardization is recommended.

---

## 🔍 Exploratory Analysis Highlights

1. **Most Dominant Genre:** `Comedy` represents over 55% of all records in this dataset (41 out of 74 films)[cite: 1].
2. **Top Studio:** `Independent` studios account for the largest single studio group (19 titles), followed by major entities like *Fox*, *Warner Bros.*, and *Universal*[cite: 1].
3. **Profitability Outliers:** High variation exists in `Profitability`, ranging from nearly zero (0.005) up to extreme positive returns (66.93x), indicating strong right-skewness[cite: 1].
4. **Worldwide Gross:** Box office gross spans from small indie releases ($25K) to major blockbusters exceeding $700M[cite: 1].

---

## 💻 Getting Started / Python Usage

You can quick-start your analysis in Python using `pandas`:

```python
import pandas as pd

# Load the dataset
df = pd.read_csv("HollywoodsMostProfitableStories.csv")

# Clean column headers
df.columns = df.columns.str.strip().str.replace(r'\s+', ' ', regex=True)

# Inspect dataset
print(df.info())
print(df.head())

# Filter top 5 most profitable films
top_profitable = df.sort_values(by="Profitability", ascending=False).head(5)
print(top_profitable[['Film', 'Genre', 'Profitability', 'Worldwide Gross']])
