<div align="center">

# 🏦 Modern Data Stack — Banking Analytics Platform

<img src="https://img.shields.io/badge/Status-Production%20Ready-success?style=for-the-badge" alt="Status"/>
<img src="https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
<img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="License"/>

**A fully containerized, end-to-end real-time data pipeline for banking analytics**

_From PostgreSQL → Kafka (CDC) → MinIO → Snowflake → dbt → Power BI_

<br/>

[🚀 Quick Start](#-quick-start) •
[📐 Architecture](#-architecture) •
[🛠️ Tech Stack](#%EF%B8%8F-tech-stack) •
[📁 Project Structure](#-project-structure) •
[⚙️ Setup](#%EF%B8%8F-setup-guide)

</div>

---

## ✨ Highlights

| Feature                       | Description                                         |
| ----------------------------- | --------------------------------------------------- |
| 🔄 **Real-time CDC**          | Capture data changes instantly via Debezium + Kafka |
| 🏗️ **Medallion Architecture** | Bronze → Silver → Gold data layers in Snowflake     |
| 📸 **SCD Type 2**             | Track historical changes with dbt snapshots         |
| 🎯 **Orchestration**          | Apache Airflow manages all workflows                |
| 🚀 **CI/CD**                  | Automated testing & deployment with GitHub Actions  |
| 🐳 **Fully Containerized**    | One command to spin up the entire stack             |

---

## 📐 Architecture

<div align="center">
  <img src="./Screenshot 2025-11-30 104348.png" alt="Modern Data Stack Architecture" width="100%"/>
</div>

### 📊 Data Flow

```
1️⃣ PostgreSQL        →  Source banking transactions (customers, accounts, transactions)
2️⃣ Debezium + Kafka  →  Real-time Change Data Capture (CDC)
3️⃣ Kafka Consumer    →  Converts events to Parquet & stores in MinIO
4️⃣ Airflow DAG       →  Loads Parquet files to Snowflake RAW tables
5️⃣ dbt Staging       →  Cleans & deduplicates data (Silver layer)
6️⃣ dbt Snapshots     →  Tracks SCD Type 2 history
7️⃣ dbt Marts         →  Business-ready dimensions & facts (Gold layer)
8️⃣ Power BI          →  Interactive dashboards & reports
```

---

## 🛠️ Tech Stack

<table>
<tr>
<td align="center" width="96">
  <a href="https://www.docker.com/">
    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" width="48" height="48" alt="Docker" />
  </a>
  <br><strong>Docker</strong>
</td>
<td align="center" width="96">
  <a href="https://www.postgresql.org/">
    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg" width="48" height="48" alt="PostgreSQL" />
  </a>
  <br><strong>PostgreSQL</strong>
</td>
<td align="center" width="96">
  <a href="https://kafka.apache.org/">
    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/apachekafka/apachekafka-original.svg" width="48" height="48" alt="Kafka" />
  </a>
  <br><strong>Kafka</strong>
</td>
<td align="center" width="96">
  <a href="https://debezium.io/">
    <img src="https://debezium.io/assets/images/color_white_debezium_type_600px.svg" width="48" height="48" alt="Debezium" />
  </a>
  <br><strong>Debezium</strong>
</td>
<td align="center" width="96">
  <a href="https://min.io/">
    <img src="https://raw.githubusercontent.com/minio/minio/master/.github/logo.svg" width="48" height="48" alt="MinIO" />
  </a>
  <br><strong>MinIO</strong>
</td>
</tr>
<tr>
<td align="center" width="96">
  <a href="https://www.snowflake.com/">
    <img src="https://www.vectorlogo.zone/logos/snowflake/snowflake-icon.svg" width="48" height="48" alt="Snowflake" />
  </a>
  <br><strong>Snowflake</strong>
</td>
<td align="center" width="96">
  <a href="https://www.getdbt.com/">
    <img src="https://seeklogo.com/images/D/dbt-logo-500AB0BAA7-seeklogo.com.png" width="48" height="48" alt="dbt" />
  </a>
  <br><strong>dbt</strong>
</td>
<td align="center" width="96">
  <a href="https://airflow.apache.org/">
    <img src="https://www.vectorlogo.zone/logos/apache_airflow/apache_airflow-icon.svg" width="48" height="48" alt="Airflow" />
  </a>
  <br><strong>Airflow</strong>
</td>
<td align="center" width="96">
  <a href="https://powerbi.microsoft.com/">
    <img src="https://upload.wikimedia.org/wikipedia/commons/c/cf/New_Power_BI_Logo.svg" width="48" height="48" alt="Power BI" />
  </a>
  <br><strong>Power BI</strong>
</td>
<td align="center" width="96">
  <a href="https://github.com/features/actions">
    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" width="48" height="48" alt="GitHub Actions" />
  </a>
  <br><strong>Actions</strong>
</td>
</tr>
</table>

### 📦 Python Dependencies

| Package                      | Purpose                              |
| ---------------------------- | ------------------------------------ |
| `faker`                      | Generate realistic banking test data |
| `psycopg2-binary`            | PostgreSQL adapter                   |
| `kafka-python`               | Kafka consumer for CDC events        |
| `boto3`                      | S3-compatible storage (MinIO)        |
| `pandas` & `fastparquet`     | Data processing & Parquet I/O        |
| `dbt-snowflake`              | Data modeling & transformations      |
| `snowflake-connector-python` | Snowflake connectivity               |

---

## 📁 Project Structure

```
📦 ModernDataStack
├── 📂 .github
│   └── 📂 workflows
│       ├── 📄 ci.yml                 # Lint, test, dbt compile
│       └── 📄 cd.yml                 # Deploy dbt models to prod
│
├── 📂 banking_dbt                    # 🔶 dbt Project
│   ├── 📄 dbt_project.yml
│   ├── 📂 models
│   │   ├── 📄 sources.yml            # Raw layer source definitions
│   │   ├── 📂 staging                # 🥈 Silver Layer
│   │   │   ├── 📄 stg_customers.sql
│   │   │   ├── 📄 stg_accounts.sql
│   │   │   └── 📄 stg_transactions.sql
│   │   └── 📂 marts                  # 🥇 Gold Layer
│   │       ├── 📂 dimensions
│   │       │   ├── 📄 dim_customers.sql
│   │       │   └── 📄 dim_accounts.sql
│   │       └── 📂 facts
│   │           └── 📄 fact_transactions.sql
│   └── 📂 snapshots                  # 📸 SCD Type 2
│       ├── 📄 customers_snapshot.sql
│       └── 📄 accounts_snapshot.sql
│
├── 📂 consumer
│   └── 📄 kafka-to-minio.py          # Kafka → Parquet → MinIO
│
├── 📂 data-generator
│   └── 📄 faker_generator.py         # Fake banking data generator
│
├── 📂 docker
│   ├── 📂 dags                       # Airflow DAGs
│   │   ├── 📄 minio_to_snowflake.py  # Load raw data to Snowflake
│   │   └── 📄 scd_snapshots.py       # Run dbt snapshots & marts
│   ├── 📂 logs                       # Airflow logs
│   ├── 📂 minio/data                 # MinIO object storage
│   ├── 📂 plugins                    # Airflow plugins
│   └── 📂 postgres/data              # PostgreSQL data volume
│
├── 📂 kafka-debezium
│   └── 📄 generate_and_post_connector.py  # Register Debezium connector
│
├── 📂 postgres
│   └── 📄 schema.sql                 # Banking OLTP schema
│
├── 📄 docker-compose.yml             # 🐳 All services orchestration
├── 📄 dockerfile-airflow.dockerfile  # Custom Airflow with dbt
├── 📄 requirements.txt               # Python dependencies
└── 📄 README.md                      # You are here!
```

---

## ⚙️ Setup Guide

### 📋 Prerequisites

- 🐳 **Docker** & **Docker Compose**
- ❄️ **Snowflake Account** (with database `BANKING` and schema `RAW`, `ANALYTICS`)
- 🐍 **Python 3.11+** (for local development)

### 1️⃣ Clone & Configure

```bash
# Clone the repository
git clone https://github.com/yourusername/ModernDataStack.git
cd ModernDataStack

# Create environment file
cp .env.example .env
```

<details>
<summary>📝 <strong>Required Environment Variables</strong></summary>

```env
# PostgreSQL (Source)
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_USER=banking_user
POSTGRES_PASSWORD=your_password
POSTGRES_DB=banking

# Kafka
KAFKA_BOOTSTRAP=localhost:29092
KAFKA_GROUP=banking-consumer

# MinIO
MINIO_ROOT_USER=minioadmin
MINIO_ROOT_PASSWORD=minioadmin
MINIO_ENDPOINT=http://localhost:9000
MINIO_ACCESS_KEY=minioadmin
MINIO_SECRET_KEY=minioadmin
MINIO_BUCKET=raw

# Airflow
AIRFLOW_DB_USER=airflow
AIRFLOW_DB_PASSWORD=airflow
AIRFLOW_DB_NAME=airflow

# Snowflake
SNOWFLAKE_ACCOUNT=your_account
SNOWFLAKE_USER=your_user
SNOWFLAKE_PASSWORD=your_password
SNOWFLAKE_WAREHOUSE=COMPUTE_WH
SNOWFLAKE_DB=BANKING
SNOWFLAKE_SCHEMA=RAW
```

</details>

### 2️⃣ Start the Stack

```bash
# Start all services
docker-compose up -d

# Verify services are running
docker-compose ps
```

| Service              | URL                   | Description               |
| -------------------- | --------------------- | ------------------------- |
| 🌐 **Airflow**       | http://localhost:8080 | Workflow UI (admin/admin) |
| 📦 **MinIO**         | http://localhost:9001 | Object Storage Console    |
| 🔌 **Kafka Connect** | http://localhost:8083 | Debezium REST API         |
| 🐘 **PostgreSQL**    | localhost:5432        | Source Database           |

### 3️⃣ Initialize the Pipeline

```bash
# 1. Create the source database schema
psql -h localhost -U banking_user -d banking -f postgres/schema.sql

# 2. Register Debezium connector
python kafka-debezium/generate_and_post_connector.py

# 3. Start the Kafka consumer (in background)
python consumer/kafka-to-minio.py &

# 4. Generate fake banking data
python data-generator/faker_generator.py --once  # or without --once for continuous
```

### 4️⃣ Configure dbt

```bash
# Create dbt profile
mkdir -p ~/.dbt
cat > ~/.dbt/profiles.yml <<EOF
banking_dbt:
  target: dev
  outputs:
    dev:
      type: snowflake
      account: {{ env_var('SNOWFLAKE_ACCOUNT') }}
      user: {{ env_var('SNOWFLAKE_USER') }}
      password: {{ env_var('SNOWFLAKE_PASSWORD') }}
      role: ACCOUNTADMIN
      database: BANKING
      warehouse: COMPUTE_WH
      schema: ANALYTICS
EOF

# Test connection
cd banking_dbt
dbt debug
dbt run
```

---

## 🔄 Airflow DAGs

| DAG                          | Schedule     | Description                  |
| ---------------------------- | ------------ | ---------------------------- |
| `minio_to_snowflake_banking` | Every minute | Load Parquet → Snowflake RAW |
| `SCD2_snapshots`             | Daily        | Run dbt snapshots + marts    |

---

## 🧪 CI/CD Pipeline

### Continuous Integration (`ci.yml`)

```yaml
✓ Code checkout
✓ Python 3.11 setup
✓ Install dependencies
✓ Ruff linting
✓ Pytest unit tests
✓ dbt compile (validation)
```

### Continuous Deployment (`cd.yml`)

```yaml
✓ Code checkout
✓ Setup dbt profile (prod)
✓ dbt deps
✓ dbt run (production)
✓ dbt test (data quality)
```

---

## 🥉🥈🥇 Medallion Architecture

| Layer         | Location          | Description                       |
| ------------- | ----------------- | --------------------------------- |
| 🥉 **Bronze** | `BANKING.RAW`     | Raw Parquet data loaded as-is     |
| 🥈 **Silver** | `stg_*` views     | Cleaned, typed, deduplicated      |
| 🥇 **Gold**   | `dim_*`, `fact_*` | Business-ready dimensions & facts |

### dbt Model Lineage

```
sources/raw.*
    │
    ▼
┌─────────────────────────────────────┐
│           Staging (Silver)          │
├─────────────────────────────────────┤
│ stg_customers  │ stg_accounts  │ stg_transactions
└───────┬────────┴───────┬───────┴────────┬───────┘
        │                │                │
        ▼                ▼                │
┌───────────────┐ ┌──────────────┐        │
│  customers_   │ │  accounts_   │        │
│  snapshot     │ │  snapshot    │        │
└───────┬───────┘ └──────┬───────┘        │
        │                │                │
        ▼                ▼                ▼
┌─────────────────────────────────────────────────┐
│                  Marts (Gold)                    │
├─────────────────────────────────────────────────┤
│  dim_customers  │  dim_accounts  │  fact_transactions
└─────────────────┴────────────────┴──────────────┘
```

---

## 📸 SCD Type 2 Tracking

Both `customers` and `accounts` are tracked with **Slowly Changing Dimensions Type 2**:

```sql
-- Columns added by dbt snapshot
dbt_valid_from   -- When this version became active
dbt_valid_to     -- When this version was superseded (NULL = current)
is_current       -- Convenience flag for current record
```

---

## 🧹 Useful Commands

```bash
# Docker
docker-compose up -d          # Start all services
docker-compose down           # Stop all services
docker-compose logs -f kafka  # Follow Kafka logs

# dbt
cd banking_dbt
dbt deps                      # Install packages
dbt compile                   # Validate SQL
dbt run                       # Build models
dbt snapshot                  # Run SCD2 snapshots
dbt test                      # Run tests
dbt docs generate && dbt docs serve  # Documentation

# Data Generator
python data-generator/faker_generator.py --once  # Single batch
python data-generator/faker_generator.py         # Continuous loop
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with ❤️ using the Modern Data Stack**

<sub>PostgreSQL • Kafka • Debezium • MinIO • Snowflake • dbt • Airflow • Docker • GitHub Actions</sub>

</div>
