# Subscription Churn Analysis

An end-to-end **Big Data Analytics pipeline for subscription customer churn analysis and prediction**, integrating **Hadoop HDFS, MapReduce, Apache Spark, PySpark, Spark MLlib, and Python-based visualization**.

The project focuses on identifying customer churn patterns, preparing large-scale customer data for analysis, and building a scalable machine learning model to predict customers at risk of churning.

---

## 📌 Overview

Customer churn is a major challenge for subscription-based businesses such as telecom providers, streaming platforms, SaaS products, and other digital services.

This project implements a Big Data workflow to process customer subscription data through multiple stages:

Raw Customer Data

       ↓

   Hadoop HDFS

       ↓

    MapReduce

       ↓

    Spark ETL

       ↓

Feature Engineering

       ↓

   Spark MLlib

       ↓

Churn Prediction

       ↓

Visualization & Insights

The pipeline combines distributed storage, batch processing, scalable ETL, machine learning, and exploratory analysis to understand customer behavior and support data-driven retention strategies.

## 🎯 Objectives

\- Store raw customer churn data using Hadoop HDFS

\- Perform distributed churn aggregation using Hadoop MapReduce

\- Build a scalable PySpark ETL pipeline

\- Clean, transform, and prepare customer data for machine learning

\- Engineer features such as customer tenure and churn labels

\- Store processed data in Parquet format

\- Train a Gradient Boosted Tree classifier using Spark MLlib

\- Analyze churn patterns through visualizations

\- Identify factors associated with higher churn risk

\- Generate insights that can support customer retention strategies

## 🛠️ Technologies Used

| Category | Technologies |
|---|---|
| Distributed Storage | Hadoop HDFS |
| Distributed Processing | Hadoop MapReduce |
| Data Processing | Apache Spark, PySpark |
| Machine Learning | Spark MLlib, Gradient Boosted Tree |
| Programming | Python |
| Data Formats | CSV, Parquet |
| Visualization | Jupyter Notebook, Matplotlib, Seaborn |
| Environment | Ubuntu / WSL2 |
| Development | Jupyter Notebook |

## 🏗️ Architecture

The project follows the architecture:

                    ┌──────────────────┐

                    │  Raw Customer    │

                    │      Data        │

                    └────────┬─────────┘

                             │

                             ▼

                    ┌──────────────────┐

                    │   Hadoop HDFS    │

                    │ Distributed      │

                    │ Storage          │

                    └────────┬─────────┘

                             │

                             ▼

                    ┌──────────────────┐

                    │ Hadoop           │

                    │ MapReduce        │

                    │ Churn Aggregation│

                    └────────┬─────────┘

                             │

                             ▼

                    ┌──────────────────┐

                    │   Spark ETL      │

                    │ Cleaning &       │

                    │ Transformation   │

                    └────────┬─────────┘

                             │

                             ▼

                    ┌──────────────────┐

                    │ Feature          │

                    │ Engineering      │

                    └────────┬─────────┘

                             │

                             ▼

                    ┌──────────────────┐

                    │ Spark MLlib      │

                    │ GBT Classifier   │

                    └────────┬─────────┘

                             │

                             ▼

                    ┌──────────────────┐

                    │ Predictions &    │

                    │ Model Evaluation │

                    └────────┬─────────┘

                             │

                             ▼

                    ┌──────────────────┐

                    │ Visualization &  │

                    │ Business Insights│

                    └──────────────────┘

## 📂 Data

The dataset contains customer-level subscription information including:

\- Customer ID

\- Age

\- Gender

\- Tenure

\- Usage Frequency

\- Support Calls

\- Payment Delay

\- Subscription Type

\- Contract Length

\- Total Spend

\- Last Interaction

\- Churn

The data is processed through the Hadoop and Spark ecosystem before being used for machine learning.
### 🔹 1. Hadoop HDFS
Hadoop HDFS is used as the distributed storage layer for the raw customer datasets.

The project organizes the data into raw and processed directories:

hdfs dfs -mkdir -p /data/churn/raw

hdfs dfs -mkdir -p /data/churn/processed

The raw dataset is uploaded to HDFS:

```bash
hdfs dfs -put training.csv /data/churn/raw/
```

The HDFS contents can then be verified using:

```bash
hdfs dfs -ls /data/churn/raw
```
### 🔹 2. Hadoop MapReduce
Hadoop MapReduce is used for batch aggregation of churn statistics across subscription types.

The mapper produces key-value pairs in the form:

(SubscriptionType, ChurnStatus)

The reducer aggregates:

- Total customers per subscription type
- Number of churned customers per subscription type
- Churn distribution across plans
Example output:

Basic     143026    83210

Premium   146878    83173

Standard  149128    83616

This stage provides an initial distributed analysis of churn behavior before the Spark processing stage.
### 🔹 3. Spark ETL
Apache Spark is used for data cleaning, transformation, and feature engineering.

ETL operations include:

- Handling missing values
- Converting numerical fields to appropriate types
- Standardizing data formats
- Encoding categorical features
- Creating a binary churn label
- Calculating derived features such as tenure_months
- Writing processed data in Parquet format
Processed data can then be loaded from HDFS using Spark:

spark.read.parquet(

    "hdfs:///data/churn/processed/training_parquet"

)

Using Parquet provides an optimized format for downstream distributed processing.
### 🔹 4. Machine Learning
A Gradient Boosted Tree (GBT) Classifier is trained using Spark MLlib.

The machine learning pipeline consists of:

Selected Features

       ↓

VectorAssembler

       ↓

GBT Classifier

       ↓

Prediction

       ↓

Model Evaluation

## Features
The model uses customer attributes such as:

- Usage Frequency
- Support Calls
- Payment Delay
- Total Spend
- Tenure
- Contract Length
Other engineered features

The model generates:

Churn probability

Binary churn prediction

## 📈 Model Performance
The model achieved the following validation results:

| Metric | Score |
|---|---:|
| Accuracy | 99.38% |
| Precision | 99.99% |
| Recall | 98.92% |
| F1-Score | 99.45% |
| ROC-AUC | 99.99% |

The project also evaluates the model using a confusion matrix and ROC curve.

## 📊 Exploratory Data Analysis
Python-based exploratory analysis was performed to understand customer churn behavior.

Visualizations include:

- Churn vs. Non-Churn Distribution
- Correlation Heatmap
- Churn by Gender
- Churn by Subscription Type
- Churn by Contract Length
- Age Distribution
- Tenure Distribution
- Usage Frequency Distribution
- Confusion Matrix
- ROC Curve
These visualizations help identify customer segments and behavioral patterns associated with churn.

## 💡 Key Insights
The analysis highlights several important churn patterns:
### Monthly Contracts
Customers with monthly contracts show substantially higher churn compared with customers on annual and quarterly contracts.
### Subscription Type
Basic-tier customers exhibit the highest churn count, while premium customers show comparatively lower churn.
### Support Interactions
Frequent support calls are associated with increased churn risk and may indicate customer dissatisfaction or unresolved issues.
### Payment Delays
Payment behavior is an important factor in understanding customer churn.
### Customer Engagement
Usage frequency and customer activity provide useful signals for identifying customers who may be at higher risk of churn.

## 💼 Business Recommendations
The analysis can support retention strategies such as:

Encouraging customers to move from monthly to longer-term contracts

Identifying high-risk customers using churn probabilities

- Proactively engaging customers with declining usage
- Investigating customers with frequent support interactions
- Addressing payment-related issues
- Designing targeted retention campaigns for high-risk customer segments

## 📁 Project Structure

```text
subscription-churn-analysis/
│
├── data/
│   ├── customer_churn_dataset-training-master.csv
│   └── customer_churn_dataset-testing-master.csv
│
├── notebooks/
│   └── BDA.ipynb
│
├── results/
│   └── visualizations/
│       ├── Average Churn Rate by Contract Length.png
│       ├── Average Churn Rate by Gender.png
│       ├── Average Churn Rate by Subscription Type.png
│       ├── Confusion Matrix.png
│       ├── Distribution of Age.png
│       ├── Distribution of Tenure.png
│       ├── Distribution of Usage Frequency.png
│       ├── Numeric Feature Correlation HeatMap.png
│       ├── ROC Curve.png
│       ├── Target Distribution.png
│       └── Top Feature Importances.png
│
├── BDA Report.pdf
├── requirements.txt
└── README.md
```


The repository structure contains the available project artifacts. The Hadoop MapReduce implementation was executed as part of the project workflow, but the mapper/reducer source files are not included in this repository.

## ⚙️ Requirements
Python 3.x

Java 8 or 11

Hadoop 3.x

Apache Spark 3.x

PySpark

Jupyter Notebook

Ubuntu / WSL2

## Python Dependencies
pip install pandas numpy matplotlib seaborn pyspark jupyter

## 🚀 Hadoop Setup
Start the Hadoop services:

start-dfs.sh

start-yarn.sh

Verify the Hadoop daemons:

```bash
jps
```

Upload the raw dataset:

hdfs dfs -mkdir -p /data/churn/raw

```bash
hdfs dfs -put training.csv /data/churn/raw/
```

Verify the uploaded data:

```bash
hdfs dfs -ls /data/churn/raw
```

## 🔮 Future Enhancements
The project can be extended with:

Real-time churn prediction using Apache Kafka and Spark Streaming

Advanced behavioral feature engineering

Customer segmentation using clustering algorithms

Automated retention recommendations

Model deployment through an API

Model explainability using SHAP

CRM integration

Real-time customer risk monitoring

## 📚 Key Learning Outcomes
Through this project, I gained practical experience with:

- Distributed data storage using HDFS
- Hadoop MapReduce
- PySpark ETL pipelines
- Feature engineering
- Parquet-based data processing
- Spark MLlib
- Gradient Boosted Tree classification
- Exploratory Data Analysis
- Model evaluation
- Data visualization
- Translating analytical results into business insights

## 👩‍💻 Author
Chetana Muddulur

Computer Science & Engineering

GitHub: Chetana2502

## ⭐ Highlights
✓ End-to-end Big Data Analytics workflow

✓ Hadoop HDFS distributed storage

✓ Hadoop MapReduce batch processing

✓ PySpark ETL

✓ Feature Engineering

✓ Parquet data processing

✓ Spark MLlib

✓ Gradient Boosted Tree

✓ Customer Churn Prediction

✓ Exploratory Data Analysis

✓ Business-oriented insights