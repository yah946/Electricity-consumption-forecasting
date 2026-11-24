# Electricity Consumption Forecasting with Microsoft Azure

## Project Overview

This project aims to develop an end-to-end electricity consumption forecasting solution using Python, Machine Learning, and Microsoft Azure.

The objective is to analyze historical electricity consumption data, identify temporal patterns and trends, and build a predictive model capable of forecasting future electricity consumption.

The project also focuses on implementing a cloud-based data pipeline using Azure services to automate data ingestion, storage, preprocessing, model training, evaluation, and inference.

The solution is designed with data governance and GDPR compliance in mind.

## Objectives

- Explore and understand historical electricity consumption data.
- Clean and preprocess time-series data.
- Identify consumption trends, patterns, and seasonality.
- Perform temporal feature engineering.
- Develop and evaluate a Linear Regression forecasting model.
- Compare machine learning predictions against a baseline forecasting approach.
- Build an automated data ingestion pipeline using Azure Data Factory.
- Store and organize raw data using Azure Data Lake Storage Gen2.
- Train and evaluate machine learning models using Azure Machine Learning.
- Create an inference pipeline for future predictions.

## Technologies and Tools

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Data Analysis | Pandas, NumPy |
| Data Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Cloud Platform | Microsoft Azure |
| Data Ingestion | Azure Data Factory |
| Data Storage | Azure Data Lake Storage Gen2 |
| Model Development | Azure Machine Learning |
| Model Training | Azure ML Designer |
| Version Control | Git, GitHub |

## Project Architecture

The project follows a cloud-based architecture that separates data ingestion, storage, processing, and machine learning workflows.

**Main components:**

1. **Azure Data Factory:** Responsible for ingesting CSV files from the data source and orchestrating data movement.
2. **Azure Data Lake Storage Gen2:** Stores raw historical electricity consumption data.
3. **Azure Machine Learning:** Handles data preprocessing, feature engineering, model training, evaluation, and inference.
4. **Azure Compute:** Provides the computational resources required to execute machine learning workloads.

### Data Flow

```text
Historical Electricity Data (CSV)
              |
              v
     Azure Data Factory
              |
              v
   Azure Data Lake Storage
              |
              v
      Azure ML Datastore
              |
              v
       Data Preparation
              |
              v
     Feature Engineering
              |
              v
       Model Training
              |
              v
       Model Evaluation
              |
              v
       Model Registration
              |
              v
      Inference Pipeline
              |
              v
   Electricity Consumption
          Predictions
```

## Project Implementation

The project is divided into two main phases.

### Phase 1: Data Exploration and Modeling with Python

This phase focuses on understanding the dataset, preparing the data, and developing an initial forecasting model.

#### 1. Data Loading and Exploration
- Load the dataset using Pandas.
- Convert the `Datetime` column into a datetime format.
- Examine dataset structure, data types, and descriptive statistics.
- Identify missing values.
- Analyze the temporal distribution of observations.

#### 2. Data Cleaning
- Detect duplicate records and missing values.
- Identify potential anomalies in electricity consumption.
- Apply appropriate cleaning strategies and justify each decision.
- Sort observations chronologically.

#### 3. Exploratory Data Analysis (EDA)
- Visualize electricity consumption over time.
- Analyze consumption patterns by hour, day, and month.
- Identify trends, seasonality, and recurring variations.

#### 4. Feature Engineering

Create relevant temporal features:

- `Hour`
- `DayOfWeek`
- `Month`
- `Year`
- `IsWeekend`

Create lag features:
- `lag24`: Consumption 24 hours earlier.
- `lag168`: Consumption 168 hours earlier (one week).

Create rolling statistics:
- `roll_24`: Rolling average over 24 hours.

#### 5. Data Preparation
- Define the target variable and explanatory features.
- Prepare the dataset for machine learning.
- Split the data chronologically into:
  - 80% Training set.
  - 20% Testing set.

#### 6. Model Training and Evaluation

Train a Linear Regression model and compare it against a baseline approach based on the previous 24-hour consumption (`lag24`).

Evaluate performance using:

- MAE (Mean Absolute Error)
- RMSE (Root Mean Squared Error)
- R² (Coefficient of Determination)
- MAPE (Mean Absolute Percentage Error)

Additional analysis:
- Compare actual and predicted consumption.
- Visualize model predictions.
- Analyze residuals and forecasting errors.

### Phase 2: Cloud Pipeline Implementation with Microsoft Azure

This phase focuses on migrating the workflow to Azure and implementing a cloud-based machine learning pipeline.

#### 1. Data Ingestion with Azure Data Factory
- Create an Azure Data Factory pipeline.
- Configure a Copy Data activity.
- Import CSV files from the source.
- Validate file structure and format.
- Store the raw data in Azure Data Lake Storage Gen2.

#### 2. Data Lake Organization

Organize raw data using a date-based directory structure:

```text
/raw/
    └── YYYY/
        └── MM/
            └── DD/
                └── consumption.csv
```

Raw data is preserved without modification.

#### 3. Azure Machine Learning Configuration
- Create an Azure Machine Learning workspace.
- Configure a datastore connected to Azure Data Lake Storage Gen2.
- Create a compute cluster for machine learning workloads.

#### 4. Dataset Creation
- Register a data asset in Azure ML Studio.
- Connect it to the configured datastore.
- Select the CSV files stored in the `/raw/` directory.

#### 5. Pipeline Development with Azure ML Designer

Build a machine learning pipeline using Azure ML Designer.

The pipeline includes the following processing stages:

**Data Cleaning**
- Summarize Data
- Clean Missing Data
- Remove Duplicate Rows
- Edit Metadata

**Feature Engineering**
- Execute Python Script
- Extract temporal features such as Hour, DayOfWeek, Month, Quarter, Year, and DayOfYear.

**Data Preparation**
- Select Columns in Dataset
- Split Data (80% training / 20% testing)
- Preserve chronological ordering during the split.

**Model Training**
- Select an appropriate regression algorithm.
- Train Model
- Score Model

**Model Evaluation**
- Evaluate Model
- Analyze prediction performance and model limitations.

#### 6. Model Registration
Register the trained model in Azure Machine Learning.

<!-- Example model name:

`forecastingmodelv1` -->

#### 7. Inference Pipeline

Convert the training pipeline into a real-time inference pipeline.

The inference pipeline will contain the necessary steps to:
- Receive new input data.
- Apply the required preprocessing and feature engineering.
- Generate predictions using the registered model.

### 8: Azure Machine Learning SDK

Explore the Azure Machine Learning SDK to interact programmatically with Azure ML resources, datasets, models, and pipelines.

## Evaluation Metrics

The forecasting model will be evaluated using the following metrics:

| Metric | Description |
|---|---|
| MAE | Measures the average absolute prediction error. |
| RMSE | Penalizes larger prediction errors. |
| R² | Measures the proportion of variance explained by the model. |
| MAPE | Measures average prediction error as a percentage. |

## Data Governance and GDPR

Data management and processing will follow relevant GDPR principles:

- Data minimization.
- Secure storage and access control.
- Controlled data processing.
- Appropriate data retention.
- Protection of potentially sensitive information.

## Project Status

<sub>Initial project setup - implementation in progress.</sub>

The project will be developed progressively, starting with Python-based exploration and modeling before moving to the Azure cloud implementation.

---

**Domain:** Data Engineering | Machine Learning | Time-Series Forecasting

**Cloud Platform:** Microsoft Azure