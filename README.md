# 💰 BalanceIQ: Data Architecture for Bank Reconciliation and Liquidity Forecasting

## 🚀 Project Status
![Development Badge](https://img.shields.io/badge/STATUS-IN%20DEVELOPMENT%20(Phase%20Roadmap)-blue)

Currently in **Phase 1: Ingestion and Load (E → L)**.  
The data structure has been defined, and work is ongoing on modularizing the business logic.

---

## 🎯 Core Business Problem (Business Context)

In transactional environments with **Legacy Systems** and fragmented financial data, bank reconciliation becomes a major operational bottleneck.

- **Challenge:** Daily reconciliation of bank statements against multiple source systems:
  - Card settlement reports  
  - Sales reports  
  - SAP Accounts Receivable (FBL5N)
- **Operational Cost:** Manual reconciliation requires approximately **5 hours per day** of human effort and is highly prone to data entry errors and delays in the accounting close.
- **Impact Objective:**  
  - Reduce manual intervention to **< 30 minutes per day**  
  - Eliminate **100% of data entry errors**  
  - Enable a **Cash Flow Forecasting** module based on reconciled and structured data

---

## 🏗️ Solution Architecture (ELT Pipeline)

BalanceIQ is built on a modular **ELT (Extract–Load–Transform)** architecture designed to handle heterogeneous data sources and act as an intelligence layer between source systems and the ERP (SAP).

### BalanceIQ Flowchart

A[📥 INGESTION
Data Loaders (Python)
8 Sources: SAP, Banks, POS, Cards]
--> B[🗄️ RAW Layer
SQL Database]

B --> C[🔄 TRANSFORMATION
Reconciliation Engine
Staging & Core]

C --> C1[🧹 Cleansing & Unification
Format Standardization]
C --> C2[🔗 Accounting Matching]

C1 --> D[📤 OUTPUT / ML]
C2 --> D

D --> D1[✅ Reconciled Report
(JSON / TXT)]
D --> D2[⚠️ Exception Report
(Unmatched Records)]
D --> D3[📈 Liquidity Forecast
Time Series]

D1 --> E[🤖 AUTOMATION
RPA + Dashboard]
E --> E1[🧾 Automatic SAP Posting
Transaction F-28]
E --> E2[📊 Treasury Dashboard
Liquidity Analysis]

D2 --> F[🔍 AUDIT
Treasury Assistant]
F --> F1[🧠 Complex Case Management
POS Errors / References]



---

## 🛠️ Technology Stack

- **Language:** Python (Pandas, OpenPyXL, SQLAlchemy)
- **Database:** MySQL / PostgreSQL (RAW and Transformed layers)
- **Data Modeling:** ELT Pattern  
  *(Data Loader → Staging → Core → Final)*
- **Machine Learning (Planned):**  
  Time Series Models (Prophet / ARIMA) for liquidity forecasting
- **Output:** Structured reports designed for direct consumption by **RPA robots**

---

## 🗺️ Project Roadmap

| Phase | Description | Status | Key Files |
| :--- | :--- | :--- | :--- |
| **I** | **Data Ingest & Load (E → L):** Load data from Excel (SAP, Banks, Portals) and `.msg` files into the SQL RAW layer. | **IN PROGRESS** | `data_loaders/`, `main.py` |
| **II** | **Data Transformation & Logic (T):** Data cleansing, standardization, and reconciliation matching logic. | PENDING | `data_models/staging/`, `data_models/core/logic/` |
| **III** | **Forecasting Model:** Development and implementation of Time Series models for short- and mid-term liquidity prediction. | PENDING | `src/models/` |
| **IV** | **Final Output & Automation:** Generation of the final reconciliation report and Business Intelligence dashboard. | PENDING | `data_models/final/` |

---

## 📂 Repository Structure

The project follows a clean, modular structure to ensure scalability and ease of testing.

```text
BalanceIQ/
├── data_loaders/        # PHASE 1: Ingestion Scripts (E)
├── data_models/         # PHASES 2–4: Transformation Logic (T)
│   ├── staging/         # Data cleansing and source unification
│   ├── core/            # Reconciliation and matching logic
│   └── final/           # Reports and output models
├── docs/                # Architecture and flow diagrams
├── utils/               # DB configuration and logging
├── requirements.txt     # Python dependencies
└── pipeline_master.py   # Main pipeline orchestrator

