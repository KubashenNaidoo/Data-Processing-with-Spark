# Spark Squirrel Census Analysis

## Overview
This project leverages Apache Spark to analyze and visualize data from the NYC Squirrel Census dataset. It demonstrates Spark's powerful capabilities for large-scale data processing, SQL querying, and machine learning.

The project includes:
* Data cleaning, transformation, and filtering using PySpark.
* Advanced SQL queries for deriving insights.
* Visualizations of key metrics.
* Window functions for cumulative metrics.
* Machine learning for predictive analysis.

---

## Features
1. **Data Cleaning**: Handling null values and ensuring schema consistency.
2. **SQL Queries**: Using Spark SQL for complex analytics.
3. **Visualizations**: Insights presented using Matplotlib and Seaborn.
4. **Window Functions**: Advanced analytical queries.
5. **Machine Learning**: Predicting squirrel sightings based on park conditions and observer metrics.

---

## Technologies Used
* **Apache Spark**: Distributed data processing.
* **PySpark SQL**: Querying structured datasets.
* **MLlib**: Machine learning library in Spark.
* **Matplotlib & Seaborn**: Data visualization.
* **Jupyter Notebook**: Development environment.

---

## Project Structure

├── data/ # Dataset 
├── code/ # Jupyter notebooks 
├── README.md # Documentation 

## Machine Learning

### Objective
Predict the number of squirrels based on:
- Park conditions.
- Total observation time.
- Number of observers.

## Steps

## 1. Index Categorical Data
Converting `Park Conditions` into numerical format:
indexer = StringIndexer(inputCols=["Park Conditions"], outputCols=["ParkConditionsIndex"])
df_indexed = indexer.fit(df_cleaned).transform(df_cleaned)`` 

## 2\. Assemble Features

Combine predictors into a single feature vector:


assembler = VectorAssembler(
    inputCols=["ParkConditionsIndex", "Total Time (in minutes, if available)", "Number of Sighters"],
    outputCol="features"
)
df_features = assembler.transform(df_indexed).select("features", "Number of Squirrels")` 

## 3\. Train-Test Split

Split data into training and testing sets:

`train_data, test_data = df_features.randomSplit([0.8, 0.2])` 

## 4\. Train the Model

Fit a Linear Regression model:

`lr = LinearRegression(featuresCol="features", labelCol="Number of Squirrels")
model = lr.fit(train_data)` 

## 5\. Evaluate the Model

Predict and evaluate performance:


`predictions = model.transform(test_data)
predictions.select("features", "Number of Squirrels", "prediction").show()` 


### Results

*   **Top Parks**: Insights into parks with the most squirrel activity.
*   **Hourly Trends**: Squirrel sightings peak during late afternoons.
*   **ML Model**: Achieved a mean squared error of `X` on test data (replace `X` after evaluation).

* * *

### Next Steps

*   Add a time-series analysis for squirrel activity over multiple days.
*   Deploy the Spark pipeline using Apache Airflow.
*   Integrate with cloud storage for distributed data processing.
