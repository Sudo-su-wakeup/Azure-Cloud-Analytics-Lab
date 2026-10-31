# ☁️ Azure Cloud Analytics Lab — Proof of Work (Semester 3)

[![Microsoft Azure](https://img.shields.io/badge/Microsoft_Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Azure Data Factory](https://img.shields.io/badge/Azure_Data_Factory-008AD7?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/en-us/products/data-factory/)
[![Azure Synapse Analytics](https://img.shields.io/badge/Azure_Synapse-005BA1?style=for-the-badge&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/en-us/products/synapse-analytics/)
[![Jain University](https://img.shields.io/badge/Jain_University-Cloud_Analytics_Lab-blue?style=for-the-badge)](https://www.jainuniversity.ac.in/)

---

## 👤 Student & Lab Information

| Attribute | Details |
| :--- | :--- |
| **Student Name** | **Yadav Manish Chandrajeet** |
| **User Principal / Login** | `cal166@redalis.net` |
| **GitHub Profile** | [`sudo-su-wakeup`](https://github.com/sudo-su-wakeup) |
| **Academic Program** | Semester 3 — Cloud Analytics Lab Exercises |
| **Institution** | Jain University |
| **Azure Subscription** | `JAIN-CloudAnalytics-Lab` (`c2135661-f8fb-457d-abac-225af670f33e`) |
| **Resource Group** | `RG-CA-core` |
| **Primary Region** | `South India` |

---

## 📚 Executive Summary & Table of Contents

This repository represents the comprehensive **Proof-of-Work (PoW)** portfolio for the Microsoft Azure Cloud Analytics laboratory curriculum. It documents cloud resource provisioning, data integration pipelines, linked service configurations, serverless Transact-SQL analytics, and cloud security / RBAC troubleshooting.

| Experiment | Title | Key Cloud Services | Documentation File | Verification Status |
| :---: | :--- | :--- | :---: | :---: |
| **Exp 01** | **ADF Pipeline: On-Prem SQL / Ingestion to Blob Storage** | Azure Data Factory V2, ADLS Gen2, Resource Groups | [📄 EXPERIMENT-01.md](./EXPERIMENT-01.md) | `Completed` ✅ |
| **Exp 02** | **Linked Service Configuration to ADLS Gen2** | Integration Runtime, Linked Services, Storage Keys | [📄 EXPERIMENT-02.md](./EXPERIMENT-02.md) | `Completed` ✅ |
| **Exp 03** | **Serverless SQL Analytics & Synapse RBAC Diagnostics** | Azure Synapse Analytics, Serverless SQL (`OPENROWSET`), RBAC | [📄 EXPERIMENT-03.md](./EXPERIMENT-03.md) | `Completed` ✅ |
| **Exp 04** | **Hybrid Ingestion Pipeline (`PL_Onprem_adls_ingest_Manish_166`)** | Azure Data Factory, Azure Key Vault, ADLS Gen2 (`Ott-adls-011`) | [📄 EXPERIMENT-04.md](./EXPERIMENT-04.md) | `Completed` ✅ |

---

## 🏗️ End-to-End Enterprise Architecture

```mermaid
flowchart TD
    subgraph Client ["Client & Auth Layer"]
        User["Yadav Manish Chandrajeet\n(cal166@redalis.net)"] --> Entra["Microsoft Entra ID\n(Tenant Auth)"]
    end

    subgraph AzureResourceGroup ["Azure Resource Group: RG-CA-core (South India)"]
        subgraph SecurityLayer ["Key Management Security"]
            AKV["Azure Key Vault\n(CA-KeyVault)"]
            LS_KV["Linked Service:\nLS_Keyvault_Manish_166"]
            AKV --- LS_KV
        end

        subgraph IngestionLayer ["Data Ingestion & Orchestration"]
            ADF["Azure Data Factory\n(adf-jain-cloudanalytics)"]
            Pipeline["Pipeline:\nPL_Onprem_adls_ingest_Manish_166"]
            LS_Src["LS_Onprem_File_Manish_166"]
            LS_Dst["LS_adls_ingest_Manish_166"]
            ADF --- Pipeline
            Pipeline --> LS_Src
            Pipeline --> LS_Dst
        end

        subgraph StorageLayer ["Data Lake Storage Layer (ADLS Gen2)"]
            Storage["Ott-adls-011\n(ADLS Gen2 Account)"]
            Container[("Container: raw")]
            Folder["Folder: ingest/"]
            Storage --> Container --> Folder
        end

        subgraph AnalyticsLayer ["Analytics & Compute Layer"]
            Synapse["Azure Synapse Studio\n(syn-jain-cloudanalytics)"]
            ServerlessSQL["Serverless SQL Pool\n(Built-in Engine)"]
            Query["OPENROWSET T-SQL\nQuery Engine"]
            Synapse --> ServerlessSQL --> Query
        end
    end

    Entra --> AzureResourceGroup
    LS_KV -.->|Managed Identity Credentials| LS_Dst
    LS_Dst --> Folder
    Query -.->|Read Stream| Folder

    style AzureResourceGroup fill:#f4f9ff,stroke:#0078D4,stroke-width:2px;
    style StorageLayer fill:#e8f4fc,stroke:#008AD7,stroke-width:1.5px;
    style AnalyticsLayer fill:#ebf3fa,stroke:#005BA1,stroke-width:1.5px;
    style IngestionLayer fill:#edf5fd,stroke:#0078D4,stroke-width:1.5px;
    style SecurityLayer fill:#fff3cd,stroke:#ffc107,stroke-width:1.5px;
```

---

## 📁 Repository Directory Structure

```
.
├── .gitignore                                 # Git ignore configuration
├── README.md                                  # Master Proof-of-Work Portfolio (This File)
├── EXPERIMENT-01.md                           # Experiment 1: Ingestion & ADF Provisioning
├── EXPERIMENT-02.md                           # Experiment 2: Linked Service to ADLS Gen2
├── EXPERIMENT-03.md                           # Experiment 3: Serverless SQL & RBAC Analysis
├── EXPERIMENT-04.md                           # Experiment 4: Hybrid Ingestion Pipeline (PL_Onprem_adls_ingest)
├── deploy_pipeline.ps1                        # Automated PowerShell Deployment Script
├── adf_artifacts/                             # ADF Arm/JSON Resource Definitions
│   ├── linkedService/                         # Linked Services (LS_Keyvault, LS_Onprem_File, LS_adls_ingest)
│   ├── dataset/                               # Datasets (DS_Onprem_File, DS_adls_ingest)
│   └── pipeline/                              # Pipelines (PL_Onprem_adls_ingest)
├── Experiment 1.pdf                           # Original Lab Manual / Exercise Reference
└── Screenshots/                               # Master Proof-of-Work Screenshot Evidence
    ├── Experiment-01/
    ├── Experiment-02/
    ├── Experiment-03/
    └── Experiment-04/                          # Key Vault & Pipeline Configuration Evidence
```

---

## 🧪 Experiments Summary

### [Experiment 01: ADF Pipeline & Ingestion to Azure Blob Storage](./EXPERIMENT-01.md)
- **Focus**: Enterprise cloud tenant authentication, resource group deployment (`RG-CA-core`), Azure Data Factory instance (`adf-jain-cloudanalytics`), and raw CSV data ingestion (`Manish_Yadav.csv`) into ADLS Gen2 storage container (`raw`).
- **Highlights**:
  - Verification of Microsoft Entra identity (`Yadav Manish Chandrajeet`).
  - Architecture overview across South India deployment region.
  - Ingested dataset validation in `caljainstorage1`.

### [Experiment 02: Linked Service Configuration to ADLS Gen2](./EXPERIMENT-02.md)
- **Focus**: Establishing secure connection protocols between Azure Data Factory / Synapse compute and Azure Data Lake Storage Gen2.
- **Highlights**:
  - Configured Linked Service `LS_Manish_Yadav`.
  - Connected via `AutoResolveIntegrationRuntime` with Account Key authentication.
  - Successfully verified end-to-end network and security handshake.

### [Experiment 03: Serverless SQL Analytics & Security Diagnostics in Azure Synapse](./EXPERIMENT-03.md)
- **Focus**: Querying data lake datasets using the Synapse `Built-in` Serverless SQL pool via `OPENROWSET` Transact-SQL, coupled with an in-depth security diagnostic.
- **Highlights**:
  - Auto-generated and configured `OPENROWSET` query targeting `raw/Manish_Yadav.csv`.
  - Root Cause Analysis (RCA) on HTTP Error 403 (Forbidden) and Built-in SQL pool role delegation.
  - Complete enterprise remediation protocol outlining Synapse RBAC and Azure Storage IAM role assignments.

### [Experiment 04: Hybrid Data Ingestion Pipeline (`PL_Onprem_adls_ingest_Manish_166`)](./EXPERIMENT-04.md)
- **Focus**: Implementing a complete hybrid cloud ingestion pipeline (`PL_Onprem_adls_ingest_Manish_166`) transferring data from On-Premises File Storage to ADLS Gen2 (`Ott-adls-011`) container `raw` folder `ingest`.
- **Highlights**:
  - Configured Azure Key Vault (`LS_Keyvault_Manish_166`) via System-Assigned Managed Identity.
  - Defined Linked Services (`LS_Onprem_File_Manish_166`, `LS_adls_ingest_Manish_166`) and Datasets (`DS_Onprem_File_Manish_166`, `DS_adls_ingest_Manish_166`).
  - Created automated deployment script `deploy_pipeline.ps1` for Azure PowerShell provisioning.

---

## 🚀 Connecting and Pushing this Repository to GitHub

To publish this repository to your GitHub account:

### Step 1: Create a New Repository on GitHub
1. Open your browser and navigate to [github.com/new](https://github.com/new).
2. Repository Name: `Azure-Cloud-Analytics-Lab` (or your preferred name).
3. Set Visibility: **Public** or **Private**.
4. Leave *"Initialize this repository with a README"* **unchecked** (since we already have a full repository built).
5. Click **Create repository**.

### Step 2: Push Local Repository to GitHub
Open PowerShell or your terminal in this project folder and run:

```powershell
# 1. Add your GitHub repository as the remote origin
git remote add origin https://github.com/sudo-su-wakeup/<YOUR_REPOSITORY_NAME>.git

# 2. Rename branch to main (if not already main)
git branch -M main

# 3. Push code and documentation to GitHub
git push -u origin main
```

---

## 📜 Academic Integrity & License
This laboratory repository is authored by **Yadav Manish Chandrajeet** for the **Sem-3 Cloud Analytics Course** at **Jain University**. All work and visual proofs represent genuine hands-on lab exercises executed on the Microsoft Azure cloud platform.
