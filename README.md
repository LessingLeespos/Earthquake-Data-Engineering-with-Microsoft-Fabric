#  Worldwide Earthquake Data Pipeline & Analytics (Microsoft Fabric)
![Visualization](/captures/01Visual_Earthquake.PNG)

## Overview
A data engineering and analysis pipeline utilising Microsoft Fabric’s Data Factory, Data Engineering, and Power BI experiences. 

Ingesting Earthquake events data from [usgs](https://earthquake.usgs.gov/). 

Technologies Used: Python, PySpark, Fabric (Data Engineering, Data Factory, Power BI)

## Worldwide Earthquake Data Visualization

![Visualization](/captures/02Visual_Earthquake.PNG)

An interactive Power BI dashboard tracking global earthquake occurrences within a selected date range.

Feature a global map view that Displays spatial distribution and location of earthquake events filtered by severity class. A highlight of total recorded events and maximum significance. It allows dynamic filtering by date range and classification levels (Low, Moderate, High).

## Microsoft Fabric Workspace Architecture

![Visualization](/captures/Workspace_Earthquake.PNG)

[ USGS API ] ──► [ Data Factory Pipeline ] ──► [ Lakehouse: Bronze (Raw GeoJSON/JSON) ]
                                                            │
                                                     (PySpark / Fabric Notebook)
                                                            ▼
                                                [ Lakehouse: Silver (Cleaned Delta) ]
                                                            │
                                                     (Spark SQL / Fabric Notebook)
                                                            ▼
                                                [ Lakehouse: Gold (Star Schema) ]
                                                            │
                                                     (Direct Lake / Power BI)
                                                            ▼
                                                [ Power BI Dashboard ]

**Medallion Data Pipelines:**

01 Worldwide Earthquake Events API - Bro (Bronze layer: Raw API ingestion)

02 Worldwide Earthquake Events API - Silv (Silver layer: Data cleaning & transformation)

03 Worldwide Earthquake Events API - Gol (Gold layer: Business-ready aggregation)

**Orchestration & Storage:**

Earthquake_Pipeline: Automated data pipeline orchestrating execution flow.

lkh_Earthquake: Central Lakehouse holding Delta tables and its corresponding SQL analytics endpoint.

**Semantic Layer:**

sm_Earthquake: Semantic model delivering structured metrics and data to Power BI reporting.

## Lakehouse Storage

![Lakehouse Storage](/captures/Lakehouse_Earthquake.PNG)

Overview of the Delta Lake storage structure within `lkh_Earthquake`:
Gold Layer (`earthquake_events_gold`): High-level curated dataset optimized for Power BI reporting.
Aggregation & Transformation Details:
  Spatial Alignment: Standardizes latitude, longitude, and elevation metrics.
  Severity & Metric Calculation: Normalizes raw magnitude (`mag`) and significance (`sig`) parameters for fast reporting aggregation.
  Metadata Refinement: Enriches location text (`place_description`) and title formats for clean visual presentation.

