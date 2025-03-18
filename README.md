## Project Overview
This project demonstrates my Python skills by analyzing job postings data to uncover key insights and trends. The project follows the Ask, Prepare, Process, Analyze methodology to ensure a structured approach to data analysis.

## Ask

### Business Problem:
- What are the locations in the US that have the highest demand for Data Analysts?
- What are the most in demand skills for a Data Analyst in the US?
- What are the most optimal skills based on both demand and salary?
- What is the average salary expectation by skills for Data Analysts in the US?

## Prepare

### Dataset Information:
- **Source:** Job postings database
- **Description:** Contains job postings with company details, salary information, job locations, and schedules.

### Data Cleaning Considerations:
- Filtering for relevant job titles and locations
- Removing records with missing salary data or filling in NAN values with Median/Mean data
- Standardizing job location formats

## Process

```python
#import libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt

#load data and basic cleaning
dataset = load_dataset('lukebarousse/data_jobs')
df= dataset['train'].to_pandas()

df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x:ast.literal_eval(x) if pd.notna(x) else x)

#filter data and plot
df_DA_US = df[(df['job_country']=='United States') & (df['job_title_short']=='Data Analyst')] 
df_plot = df_DA_US['job_location'].value_counts().head(10).to_frame()

sns.set_theme(style="ticks")
sns.barplot(data=df_plot, x='count', y='job_location', hue='count', palette='dark:b_r')
sns.despine()
plt.title('Top 10 Locations for Data Analyst Jobs in the US')
plt.xlabel('Number of Jobs')
plt.ylabel('Location')
plt.show()

df_DA_US = df[(df['job_country']=='United States') & (df['job_title_short']=='Data Analyst')] 
df_plot = df_DA_US['company_name'].value_counts().head(10).to_frame()

sns.set_theme(style="ticks")
sns.barplot(data=df_plot, x='count', y='company_name', hue='count', palette='dark:b_r')
sns.despine()
plt.title('Counts of Companies with Data Analyst Jobs in the US')
plt.xlabel('Number of Jobs')
plt.ylabel('Location')
plt.show()

```

![Graph 1](images/graph1.png)
![Graph 2](images/graph2.png)