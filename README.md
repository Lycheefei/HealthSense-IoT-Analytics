# HealthSense-IoT-Analytics: End-to-End Health Data Platform

**HealthSense-IoT-Analytics** is a production-grade data engineering and analytics platform designed to process high-frequency telemetry data from ergonomic IoT devices. The platform automates the entire lifecycle of data: from multi-modal ingestion (JSON & SQLite) to PostgreSQL partitioned storage, culminating in behavioral modeling and LLM-driven insight generation.

---

### System Architecture

The platform follows a robust 4-tier data architecture:
1.  **Ingestion Tier**: A stability-aware orchestrator monitors device folders, handling concurrent ingestion of multi-stream JSON and SQLite databases.
2.  **Storage Tier**: PostgreSQL with **Table Partitioning** (by time range) and idempotent logic (`ON CONFLICT DO NOTHING`) ensures high performance and data integrity.
3.  **Analytics Tier**: A behavioral engine that calculates user "Gold Patterns" using rolling averages and lifecycle curves.
4.  **AI Insight Tier**: Integrated LLM pipeline (via Ollama/Qwen) for automated sentiment analysis and technical feedback clustering.

---

### Key Features

* **Smart Orchestration**: Automatically detects, validates, and processes incoming device data using a file-stability polling mechanism.
* **Multi-Modal Ingestion**: 
    * **JSON Stream**: Processes achievements, evaluations, exercises, and hints.
    * **SQLite Adapter**: Extracts granular telemetry from local device databases.
* **Scalable Storage**: Implements PostgreSQL range partitioning to handle millions of rows efficiently, optimized for time-series analysis.
* **Behavioral Modeling**: Includes a "Gold User" analysis framework to visualize posture improvements, sit-stand ratios, and hydration habits over time.
* **Automated Data Logging**: Comprehensive lineage tracking—logs every file's ingestion status, row counts, and error rates.

---

### Tech Stack

* **Language**: Python 3.9+ (Pandas, SQLAlchemy, Psycopg)
* **Database**: PostgreSQL 13+ (Time-based Partitioning)
* **AI/LLM**: Ollama (Qwen-3 8B), `json-repair` for deterministic output.
* **Analysis**: Jupyter Notebook, Matplotlib (Seaborn), NumPy.

---

### Repository Structure

```text
.
├── adapters/           # Data ingestion adapters (JSON/SQLite)
├── db/                 # Database schema (PostgreSQL) and logging logic
├── config.py           # System configurations and stream definitions
├── orchestrator.py     # Main polling service and folder watcher
├── analysis/           # Behavioral modeling and gold user notebooks
└── report_gen/         # LLM-powered feedback analyzer (Qwen/Ollama)
