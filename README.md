# ADF Orders Pipeline

This repository contains an **Azure Data Factory (ADF) project** for processing and transforming order data using a **Bronze-Silver-Gold architecture**. The goal is to take raw data files, clean and transform them, and make them ready for applications and reporting in **Azure SQL Database**.

---

## How it works

1. **Landing**  
   - All raw files (CSV, JSON, etc.) are uploaded to a **landing container** in Azure Blob Storage.  
   - This is just a temporary staging area for incoming data.

2. **Raw (Bronze)**  
   - The data is copied into the **raw container** in ADLS Gen2 using a Copy Activity.  
   - This keeps the original files safe and unmodified.

3. **Cleansed (Silver)**  
   - Using **Mapping Data Flows**, the raw data is cleaned and standardized.  
   - This includes typecasting, removing duplicates, and fixing formats.  
   - The cleaned data is stored in the **cleansed container**.

4. **Structured (Gold)**  
   - The cleansed data is further transformed: joins, aggregations, and business logic are applied.  
   - The final data is stored in the **structured container** and also written to **Azure SQL Database**.  
   - Supports **upsert and overwrite**, so the SQL table stays consistent.

---

## Security & Authentication

- Secrets are stored in **Azure Key Vault**.  
- You can choose how the pipelines authenticate:
  - **Service Principal**  
  - **User Assigned Managed Identity**  
- The project follows **least-privileged role principles**, so users only have the permissions they need.

---

## Scheduling

- The pipelines run automatically using a **tumbling window trigger** every **15 minutes**.  
- This makes sure new data is processed regularly without manual intervention.

---

## Pipelines

- **Landing → Raw**: Simple copy of files from landing to raw.  
- **Raw → Cleansed**: Cleans and standardizes the data.  
- **Cleansed → Structured**: Applies business transformations and loads the final data into SQL.

---

## Features

- Bronze-Silver-Gold architecture  
- Handles multiple file formats  
- Cleans and transforms data using Mapping Data Flows  
- Writes to Azure SQL Database with upsert/overwrite support  
- Flexible authentication via Key Vault, Service Principal, or Managed Identity  
- Automated pipelines with tumbling window triggers  
- Modular and scalable design  

---

## Requirements

- Azure subscription with Data Factory, Blob Storage, ADLS Gen2, and Key Vault  
- Azure SQL Database  
- Configured Integration Runtime  

---

## How to use

1. Clone the repo.  
2. Import the pipelines into your **Azure Data Factory** instance.  
3. Configure linked services (Blob Storage, ADLS Gen2, SQL Database, Key Vault).  
4. Choose your preferred authentication method.  
5. Run the pipelines manually or let the **15-minute trigger** run them automatically.
