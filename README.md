# ADF Orders Pipeline

This repository contains an **Azure Data Factory (ADF) project** for processing and transforming order data using a **Bronze-Silver-Gold architecture**. The project demonstrates end-to-end data ingestion, transformation, and loading into **Azure SQL Database** for downstream consumption.

---

## Architecture Overview

The pipeline follows a **modern data engineering approach**:

1. **Landing (Bronze)**  
   - Raw files of various formats are ingested into an **Azure Blob Storage** container (`landing`).  
   - Acts as the initial staging area for all incoming data.

2. **Raw (Bronze → Raw)**  
   - Data is copied from landing to the **raw container** in **ADLS Gen2** using a simple **Copy Activity**.  
   - Preserves the original data for auditing and traceability.

3. **Cleansed (Silver)**  
   - **Mapping Data Flows** transform and clean the raw data.  
   - Includes typecasting, normalization, and validation.  
   - Data is stored in the **cleansed container** in ADLS Gen2.

4. **Structured (Gold)**  
   - Further transformations, joins, and aggregations are applied.  
   - The final curated data is stored in the **structured container** (ADLS Gen2) and **Azure SQL Database**.  
   - Supports **upsert and overwrite operations** to maintain data consistency for applications.

---

## Pipelines

- **Landing → Raw**: Simple ingestion pipeline using Copy Activity.  
- **Raw → Cleansed**: Data Flow pipeline to clean and standardize the data.  
- **Cleansed → Structured**: Data Flow pipeline for business-ready transformations and loading into **Azure SQL Database**.

---

## Features

- Bronze-Silver-Gold layered architecture  
- Support for multiple input file formats (CSV, JSON, etc.)  
- Data cleansing and transformation using **ADF Mapping Data Flows**  
- Sink to **Azure SQL Database** with **upsert and overwrite support**  
- Modular and scalable design for future enhancements  

---

## Requirements

- Azure subscription with **Data Factory**, **Blob Storage**, and **ADLS Gen2**  
- Azure SQL Database instance  
- Azure Data Factory configured with Integration Runtime  

---

## Usage

1. Clone the repository.  
2. Import the ADF pipelines into your **Azure Data Factory** instance.  
3. Configure your **linked services** for Blob Storage, ADLS Gen2, and SQL Database.  
4. Trigger the pipelines in sequence:
   - Landing → Raw  
   - Raw → Cleansed  
   - Cleansed → Structured  

---
