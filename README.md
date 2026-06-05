# Identity Security Machine Learning Platform

<div align="center">

![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00ADD4?style=for-the-badge&logo=delta&logoColor=white)
![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=for-the-badge&logo=mlflow&logoColor=white)

**End-to-End IAM Security Analytics & Threat Detection Platform**

</div>
<img width="1342" height="761" alt="image" src="https://github.com/user-attachments/assets/6dbe4e8d-4eb5-4ef4-9091-6befa68f2c38" />
<img width="1350" height="664" alt="image" src="https://github.com/user-attachments/assets/444d8113-4d0e-48b6-952d-83bf0e71f51d" />
<img width="1139" height="738" alt="image" src="https://github.com/user-attachments/assets/57ddb06f-07c6-4de2-b933-bb877bcc38ad" />


---

## Overview

A comprehensive Databricks-based platform for Identity and Access Management (IAM) security analytics and threat detection using machine learning. This platform provides end-to-end IAM security monitoring, from data ingestion through advanced anomaly detection. It combines real-time analytics dashboards with machine learning models to identify suspicious login patterns and potential security threats.

## Components

### 1. Data Pipeline
**File:** `Identity & Access Management (IAM) Analytics Platform.ipynb`

End-to-end ETL pipeline that:
- Ingests raw IAM login data from Unity Catalog
- Transforms and enriches security events
- Creates bronze, silver, and gold layer tables
- Prepares data for both analytics and ML workflows

**Key Features:**
- Bronze layer: Raw IAM log ingestion
- Silver layer: Data cleansing, deduplication, enrichment
- Gold layer: Aggregated metrics and analytics-ready datasets

### 2. Security Analytics Dashboard
**File:** `IAM Security Analytics Dashboard.lvdash.json`

Interactive dashboard providing real-time IAM security insights:
- **Login Activity Monitoring**: Track authentication patterns across time
- **Device Type Analysis**: Identify login trends by device (desktop, mobile, tablet)
- **Login Activity by Hour**: Detect unusual access patterns by time of day
- **Failed Login Tracking**: Monitor authentication failures and potential brute force attempts
- **User Activity Metrics**: Track unique users, total logins, and success rates

**Data Source:** `identity.default.silver_iam_logs`

### 3. ML-Based Threat Detection
**File:** `IAM Suspicious Login Detection ML.ipynb`

Machine learning pipeline for anomaly detection:
- **Algorithm**: Isolation Forest (unsupervised learning)
- **Features**:
  - Risk score aggregation
  - Failed login counts per user
  - Device type patterns
  - Login time analysis (hourly patterns)
- **Model Output**: Anomaly scores identifying suspicious login behavior
- **Performance**: Detects ~5% anomalies with configurable contamination threshold

**Model Pipeline:**
1. Feature engineering from IAM logs
2. One-hot encoding for categorical variables
3. Feature scaling and normalization
4. Isolation Forest training
5. Anomaly scoring and ranking
6. Feature importance analysis

## Data Architecture

```
Unity Catalog Structure:
├── identity (catalog)
    └── default (schema)
        ├── bronze_iam_logs (raw ingestion)
        ├── silver_iam_logs (cleaned, enriched)
        └── iam_metrics (metric view for dashboard)
```

## Getting Started

### Prerequisites
- Databricks workspace with Unity Catalog enabled
- Serverless compute or cluster with Python support
- IAM log data in Unity Catalog

### Setup

1. **Run the Data Pipeline**
   ```
   Open: Identity & Access Management (IAM) Analytics Platform.ipynb
   Execute all cells to create tables and metric views
   ```

2. **Deploy the Dashboard**
   ```
   Import: IAM Security Analytics Dashboard.lvdash.json
   Publish the dashboard to your workspace
   ```

3. **Train the ML Model**
   ```
   Open: IAM Suspicious Login Detection ML.ipynb
   Run all cells to train the anomaly detection model
   Note: MLflow tracking requires classic cluster compute
   ```

## Key Metrics

The platform tracks and analyzes:
- **Total logins**: Overall authentication volume
- **Unique users**: Distinct user activity
- **Failed logins**: Authentication failure counts
- **Success rate**: Login success percentage
- **Device distribution**: Login patterns by device type
- **Temporal patterns**: Hour-of-day and date-based trends
- **Anomaly scores**: ML-detected suspicious behavior

## Machine Learning Model

**Isolation Forest Configuration:**
- Contamination: 5% (adjustable based on your security posture)
- Estimators: 100 trees
- Features: 4 dimensions (risk_score, failed_login_count, login_hour, device_type)
- Training samples: 100,000 IAM events

**Detected Anomalies:**
The model identifies users with:
- Unusual login time patterns
- Excessive failed login attempts
- Abnormal device type usage
- High-risk behavior scores

## Technology Stack

- **Platform**: Databricks (Serverless Compute)
- **Data Layer**: Unity Catalog (Delta Lake)
- **Languages**: Python, SQL
- **ML Libraries**: scikit-learn, pandas, numpy
- **Visualization**: Lakeview Dashboards
- **Tracking**: MLflow (requires classic cluster)

## Future Enhancements

Potential additions:
- Real-time streaming anomaly detection
- Multi-factor authentication (MFA) analysis
- Geographic location-based risk scoring
- User behavior analytics (UBA)
- Automated alerting and incident response
- Model retraining pipeline with MLflow
- Integration with SIEM systems

## Security Considerations

- All data stored in Unity Catalog with governance controls
- Dashboard access controlled via workspace permissions
- Model predictions should be reviewed by security analysts
- Anomaly scores are risk indicators, not definitive threats
- Regular model retraining recommended for evolving threat patterns

