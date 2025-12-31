# NYC Public Schools: SAT Performance Analysis

## 📌 Project Overview
This project analyzes standardized test (SAT) data from New York City public schools to evaluate academic performance across the five boroughs. The analysis assists stakeholders, including policy professionals and parents, in identifying high-performing schools and understanding regional disparities in educational outcomes. The SAT consists of three sections (reading, math, and writing), each with a maximum score of 800 points.

## 🚀 Key Objectives
* **Identify High Achievers:** Isolate schools with exceptional math performance (scores $\ge$ 80% of the maximum possible score).
* **Rank Institutions:** Determine the top 10 schools in NYC based on total aggregated SAT scores.
* **Regional Analysis:** Quantify performance variability by borough to understand the distribution of scores across the city.

## 🛠️ Technical Stack
* **Language:** Python 3.x
* **Data Manipulation:** Pandas (Grouping, Aggregation, Lambda functions)
* **Input Data:** `schools.csv`

## 📊 Methodology & Insights
1.  **Math Excellence Filtering:**
    * The analysis filtered for schools achieving an average math score of at least 640 (80% of 800).
    * **Result:** Prestigious institutions like *Stuyvesant High School* and *Bronx High School of Science* appeared at the top of this subset.
2.  **Total Score Aggregation:**
    * A new metric, `total_SAT`, was calculated by summing the average math, reading, and writing scores for each school.
    * The top 10 schools were ranked by this cumulative metric.
3.  **Borough-Level Statistics:**
    * The data was grouped by borough to calculate the number of schools, average total SAT, and standard deviation.
    * **Key Finding:** **Manhattan** exhibited the highest standard deviation (230.29), indicating the widest gap between high-performing and low-performing schools within a single borough.
    * **Key Finding:** **Staten Island** had the highest average SAT score (1439.00) among the boroughs.

## 💻 Code Highlight: Complex Aggregation
The project utilized Pandas' `groupby` and `agg` functions to generate summary statistics in a single, efficient step.

```python
# Aggregating data by borough to find count, mean, and standard deviation
borough_stats = (
    schools.groupby('borough')
    .agg(
        num_schools = ('school_name', 'count'),
        average_SAT = ('total_SAT', lambda x: round(x.mean(), 2)),
        std_SAT = ('total_SAT', lambda x: round(x.std(), 2))
    )
    .reset_index()
)
