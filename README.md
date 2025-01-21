# Logistics_ETL_Automation
# Logistics_ETL_Automation_Management

This project automates the process of managing logistics data by leveraging Apache Airflow to load and partition data into a Hive data warehouse on Google Cloud Dataproc. The workflow ensures efficient data ingestion, organization, and archival of raw files.

---

## Features

- **Automated Workflow**: Uses Apache Airflow to automate the entire ETL process.
- **Dynamic Partitioning**: Partitions data by date for improved query performance.
- **Error Handling**: Includes sensors to monitor the presence of input files before processing.
- **File Archival**: Moves processed files to an archive bucket to ensure the raw bucket stays organized.

---

## Workflow Steps

1. **Monitor GCS Bucket**:
   - Detects new logistics data files in the input bucket (`gs://logistics-raw-gds/input_data`).

2. **Create Hive Database and Tables**:
   - Creates a database (`logistics_db`) if it doesn’t already exist.
   - Creates an external Hive table (`logistics_data`) for raw data.
   - Creates a partitioned Hive table (`logistics_data_partitioned`) for optimized querying.

3. **Load and Partition Data**:
   - Loads data from the external table into the partitioned table dynamically using the `date` field.

4. **Archive Raw Files**:
   - Moves processed files from the raw bucket to an archive bucket (`gs://logistics-archive-gds`).

---

## Prerequisites

- **Google Cloud Platform**:
  - A Dataproc cluster named `compute-cluster` in the `us-central1` region.
  - Google Cloud Storage buckets for raw data and archives.
  - A GCP project ID (`project_id`).
  
- **Airflow Configuration**:
  - Airflow set up with the required providers:
    - `apache-airflow-providers-google`
  - Environment variables or connections for GCP authentication.

---

## File Structure

```plaintext
├── dags/
│   └── hive_load_airflow_dag.py  # Airflow DAG definition
├── README.md                    # Project documentation
