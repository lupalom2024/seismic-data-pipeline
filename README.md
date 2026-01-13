# 🌍 Real-Time Seismic Analytics with Microsoft Fabric

![Fabric](https://img.shields.io/badge/Microsoft%20Fabric-Enabled-0078D4?style=for-the-badge&logo=microsoft)
![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python)
![Status](https://img.shields.io/badge/Pipeline-Active-success?style=for-the-badge)

### 📋 Project Overview
This project focuses on building a complete **Data Engineering and Analytics pipeline** to process and analyze earthquake event data using **Microsoft Fabric**.

The pipeline ingests real-time data from the **USGS API**, processes it through a Medallion Architecture (Bronze, Silver, Gold) using PySpark, and produces business-ready datasets for visualization in **Power BI**.

**Key Technologies:**
* **Computation:** Fabric Data Engineering (Spark/Python).
* **Orchestration:** Fabric Data Factory (Pipelines).
* **Visualization:** Power BI (DirectLake).

---

### 🏗️ Architecture Flow
The workflow moves data from raw ingestion to analytical readiness:

```mermaid
graph LR
    A[USGS API Source] -->|Ingestion| B(Bronze Layer - Raw JSON)
    B -->|Transformation| C(Silver Layer - Cleaned Delta)
    C -->|Enrichment| D(Gold Layer - Reporting)
    D -->|DirectLake| E[Power BI Dashboard]

```

---

### 🛠️ Technical Implementation Steps

#### 1. Bronze Layer (Ingestion)

* **Script:** `01_ingestion_bronze.ipynb`
* **Function:** Ingests raw earthquake data directly from the USGS API.
* **Strategy:** Minimal processing to store data in its original format (JSON) within the **OneLake**, serving as the immutable foundation.

#### 2. Silver Layer (Transformation)

* **Script:** `02_transform_silver.ipynb`
* **Function:** Enhances data from the Bronze layer.
* **Actions:** Cleans null values, handles timestamps, and consolidates schemas. Prepares data for analytical processing.

#### 3. Gold Layer (Business Logic)

* **Script:** `03_aggregation_gold.ipynb`
* **Function:** Refines data to create business-ready datasets.
* **💡 Technical Note:** A custom environment was created to include the **`reverse_geocoder`** library. This is required to enrich the dataset with precise location details (City/Country) based on coordinates.

---

### ⚙️ Pipeline Orchestration (Dynamic Variables)

To ensure the pipeline is fully automated, dynamic variables are configured in **Data Factory** to fetch data incrementally based on execution time:

| Variable | Expression Logic | Description |
| --- | --- | --- |
| **`start_date`** | `@formatDateTime(adddays(utcNow(),-1), 'yyyy-MM-dd')` | Captures the date **one day before** execution. |
| **`end_date`** | `@formatDateTime(utcNow(), 'yyyy-MM-dd')` | Captures the **current date** at runtime. |

---

### 📚 Data Dictionary

The following attributes are tracked for each seismic event:

| Attribute | Type | Description |
| --- | --- | --- |
| `id` | String | Unique identifier for each data record. |
| `latitude` | Double | Latitude of the event's location. |
| `longitude` | Double | Longitude of the event's location. |
| `elevation` | Double | Elevation/Depth at which the event occurred (meters). |
| `title` | String | Title or name of the earthquake event. |
| `place_description` | String | Text description of the location. |
| `sig` | BigInt | Significance score (importance) of the event. |
| `mag` | Double | Magnitude of the earthquake. |
| `magType` | String | Scale used to measure the event (e.g., Richter). |
| `time` | Timestamp | Exact time when the event occurred. |

---

### 📊 Dashboard Preview

*(Visualization of global seismic activity)*

*(Note: Ensure your image file is named correctly inside the img folder)*

```


```
