# 🌍 Real-Time Seismic Analytics with Microsoft Fabric

![Fabric](https://img.shields.io/badge/Microsoft%20Fabric-Enabled-0078D4?style=for-the-badge&logo=microsoft)
![Status](https://img.shields.io/badge/Pipeline-Active-success?style=for-the-badge)

### 📋 Project Overview
This project implements an End-to-End Data Engineering pipeline that ingests real-time earthquake data from the **USGS API**. It demonstrates the "Medallion Architecture" (Bronze, Silver, Gold) using **Microsoft Fabric Notebooks** and **PySpark**.

---

### 🏗️ Architecture Flow
The pipeline follows industry best practices for data processing:

```mermaid
graph LR
    A[USGS API Source] -->|Ingestion| B(Bronze Layer - Raw JSON)
    B -->|Transformation| C(Silver Layer - Cleaned Delta)
    C -->|Aggregation| D(Gold Layer - Star Schema)
    D -->|DirectLake| E[Power BI Report]
