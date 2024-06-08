Exploratory Data Analysis of McDonald's Menu Dataset
Overview
Welcome to the Exploratory Data Analysis (EDA) of the McDonald's Menu dataset. This project was conducted during my internship at Oasis Infobyte. The primary aim is to delve into the nutritional details of various McDonald's menu items, encompassing 24 features such as calories, fat, protein, and sugar. Through meticulous data cleaning, visualization, and statistical analysis, this EDA aims to uncover insights into the nutritional composition, aiding in informed dietary decisions and consumer awareness.

Table of Contents
Introduction
Getting Started
Data Cleaning
Exploratory Data Analysis
Outlier Detection
Nutritional Analysis by Category
Comparison of Nutritional Metrics
Identifying Healthier Options
Conclusions
Recommendations
Introduction
The McDonald's Menu dataset contains nutritional information for various items offered by McDonald's. This project aims to analyze these nutritional details to help consumers make better dietary choices. The dataset includes 260 items with features such as calories, total fat, protein, and more.

Getting Started
To replicate this analysis, you will need the following libraries:

numpy
pandas
matplotlib
seaborn
First, clone this repository and navigate to the project directory. Then, install the required libraries using:

bash
Copy code
pip install numpy pandas matplotlib seaborn
Load the dataset and display the first few rows:

python
Copy code
import pandas as pd

# Load the data
df = pd.read_csv('menu.csv')

# Display the first few rows of the dataset
print(df.head())
Data Cleaning
We performed the following data cleaning tasks:

Missing Values: Checked for and confirmed no missing values.
Data Types: Verified data types for each column to ensure they are appropriate for analysis.
Duplicates: Checked for and removed any duplicate rows.
Exploratory Data Analysis
Outlier Detection
Outliers were identified using the Interquartile Range (IQR) method. Here's a summary of the outliers found in each numerical column:

python
Copy code
def detect_outliers(df):
    outliers = {}
    for column in df.select_dtypes(include=['int64', 'float64']).columns:
        Q1 = df[column].quantile(0.25)
        Q3 = df[column].quantile(0.75)
        IQR = Q3 - Q1
        lower_bound = Q1 - 1.5 * IQR
        upper_bound = Q3 + 1.5 * IQR
        outlier_indices = df[(df[column] < lower_bound) | (df[column] > upper_bound)].index
        outliers[column] = len(outlier_indices)
    return outliers

# Detect outliers
outliers = detect_outliers(df)
print("Number of outliers in each numerical column:")
print(outliers)
Nutritional Analysis by Category
We grouped the data by category and calculated mean nutritional values. The analysis revealed significant differences in nutritional content across different categories, such as breakfast items generally having higher calorie counts compared to other categories.

Comparison of Nutritional Metrics
A pair plot was generated to visualize the relationships between different nutritional metrics, revealing patterns such as items with higher calories often having more fat.

Identifying Healthier Options
Healthier options were identified based on specific criteria (e.g., low calorie, low fat, high protein). Initially, no items met all three criteria simultaneously. Adjusting the criteria revealed several items that met at least two of the criteria:

python
Copy code
# Define percentiles for adjusted "healthier options"
calories_25th = df['Calories'].quantile(0.25)
total_fat_25th = df['Total Fat'].quantile(0.25)
protein_75th = df['Protein'].quantile(0.75)

# Filter menu items that meet at least two criteria for healthier options
healthier_options_adjusted = df[
    ((df['Calories'] < calories_25th) & (df['Total Fat'] < total_fat_25th)) |
    ((df['Calories'] < calories_25th) & (df['Protein'] > protein_75th)) |
    ((df['Total Fat'] < total_fat_25th) & (df['Protein'] > protein_75th))
]

# Display healthier options
print(healthier_options_adjusted)
Conclusions
This analysis provided valuable insights into the nutritional content of McDonald's menu items. Key findings include:

Breakfast items are generally higher in calories.
Burgers and chicken items are higher in total fat and cholesterol.
No single item met the strict criteria for the healthiest option, but several items met at least two of the criteria.
Recommendations
Based on the analysis, the following recommendations are made:

Consumers looking for lower-calorie options may consider salads and certain sides.
McDonald's could consider offering more menu items that meet the criteria for being low in calories, low in fat, and high in protein.
Further investigation into the nutritional composition of menu items with extreme values may help improve the overall menu offering.
