# CRM Analytics for Purchase Propensity Prediction in an Online Retail Dataset

![CRM Analytics Banner](crm_analytics.webp)

### Introduction

In this study, the Online Retail dataset has been utilized to perform CRM (Customer Relationship Management) analyses, which are frequently applied in the industry. The key analyses and their purposes are as follows:

- **Cohort Analysis**: Identifies customer retention patterns over time, helping businesses understand how customer engagement evolves.  
- **Customer Lifetime Value (CLTV) Prediction**: Using BG-NBD and Gamma-Gamma models, CLTV is estimated to evaluate the long-term value each customer brings to the business.  
- **RFM Analysis**: Segments customers based on their Recency, Frequency, and Monetary values to optimize targeted marketing strategies.  
- **Customer Purchase Propensity Prediction**: A logistic regression model is used to predict the likelihood of customer purchases, aiding in prioritizing marketing efforts.  

This comprehensive approach enables actionable insights to improve customer relationships and maximize business profitability.


**Dataset Information**

This is a transactional data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail.The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.

**Variables Table**

| **Variable Name** | **Role**       | **Type**       | **Description**                                                                         | **Units**  | **Missing Values** |
|--------------------|----------------|----------------|-----------------------------------------------------------------------------------------|------------|---------------------|
| InvoiceNo          | ID            | Categorical    | A 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'c', it indicates a cancellation |            | No                  |
| StockCode          | ID            | Categorical    | A 5-digit integral number uniquely assigned to each distinct product                   |            | No                  |
| Description        | Feature       | Categorical    | Product name                                                                            |            | Yes                  |
| Quantity           | Feature       | Integer        | The quantities of each product (item) per transaction                                  |            | No                  |
| InvoiceDate        | Feature       | Date           | The day and time when each transaction was generated                                   |            | No                  |
| UnitPrice          | Feature       | Continuous     | Product price per unit                                                                 | Sterling   | No                  |
| CustomerID         | Feature       | Categorical    | A 5-digit integral number uniquely assigned to each customer                           |            | Yes                  |
| Country            | Feature       | Categorical    | The name of the country where each customer resides                                    |            | No                  |




**Additional Variable Information**

`InvoiceNo`: Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'c', it indicates a cancellation.  

`StockCode`: Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.  

`Description`: Product (item) name. Nominal.  

`Quantity`: The quantities of each product (item) per transaction. Numeric.  

`InvoiceDate`: Invoice date and time. Numeric, the day and time when each transaction was generated.  

`UnitPrice`: Unit price. Numeric, product price per unit in sterling.  

`CustomerID`: Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer.  

`Country`: Country name. Nominal, the name of the country where each customer resides.  

**Index:**


- [1. Data Validation and Cleaning](#1-data-validation-and-cleaning)
  - [1.1. Check General Information of Data](#11-check-general-information-of-data)
  - [1.2. Handle Missing Values](#12-handle-missing-values)
  - [1.3. Handle Duplicated Values](#13-handle-duplicated-values)
  - [1.4. Clean Records with Negative Quantity, UnitPrice Issues, and Canceled Transactions](#14-clean-records-with-negative-quantity-unitprice-issues-and-canceled-transactions)

- [2. Exploratory Data Analysis and Preprocessing](#2-exploratory-data-analysis-and-preprocessing)
  - [2.1. Categoric Variable Analysis](#21-categoric-variable-analysis)
  - [2.2. Outlier Analysis](#22-outlier-analysis)
  - [2.3. Additional Inferences](#23-additional-inferences)

- [3. Cohort Analysis](#3-cohort-analysis)

- [4. Customer Lifetime Value (CLTV) Prediction with BG-NBD and Gamma-Gamma Submodel](#4-customer-lifetime-value-cltv-prediction-with-bg-nbd-and-gamma-gamma-submodel)
  - [4.1. Data Preparation](#41-data-preparation)
  - [4.2. Building the BG-NBD Model](#42-building-the-bg-nbd-model)
  - [4.3. Building the GAMMA-GAMMA Model](#43-building-the-gamma-gamma-model)
  - [4.4. CLTV Calculation with BG-NBD and GAMMA-GAMMA Models](#44-cltv-calculation-with-bg-nbd-and-gamma-gamma-models)
  - [4.5. Creation of CLTV Segments](#45-creation-of-cltv-segments)

- [5. RFM Analysis](#5-rfm-analysis)
  - [5.1. Calculating RFM Metrics](#51-calculating-rfm-metrics)
  - [5.2. Calculating RFM Scores](#52-calculating-rfm-scores)
  - [5.3. Customer Segmentation Based on RFM Scores](#53-customer-segmentation-based-on-rfm-scores)
  - [5.4. Advanced Segmentation with KMeans Clustering Algorithm](#54-advanced-segmentation-with-kmeans-clustering-algorithm)

- [6. Creating an ML Model for Customer Purchase Propensity Prediction](#6-creating-an-ml-model-for-customer-purchase-propensity-prediction)
  - [6.1. Feature Engineering](#61-feature-engineering)
  - [6.2. Correlation Analysis](#62-correlation-analysis)
  - [6.3. Purchase Propensity Prediction Using Logistic Regression](#63-purchase-propensity-prediction-using-logistic-regression)

- [7. Conclusion](#7-conclusion)

## Installation

To run this project locally, follow these steps:

   ```bash
   git clone https://github.com/kanitvural/CRM_analytics.git
   cd CRM_analytics
   python -m venv venv
   .\venv\Scripts\activate
   pip install -r requirements.txt