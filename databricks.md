# Databricks on Azure Cheatsheet

## Overview

**Azure Databricks** is a cloud-based data analytics platform optimized for big data analytics and AI. It combines Apache Spark with Azure's cloud capabilities for scalable and collaborative data solutions.

### Key Concepts

- **Apache Spark**: Distributed data processing framework that enables data transformations, machine learning, and streaming.
- **Workspace**: An environment for managing data, notebooks, jobs, and clusters.
- **Clusters**: Scalable compute resources for running Spark workloads.
- **Notebooks**: Interactive documents to run code (Python, Scala, SQL, R) and visualize results.
- **Jobs**: Automated tasks for running notebooks or applications.
- **DBFS**: Databricks File System, a distributed file system layer on top of Azure storage.

---

## Architecture

1. **Azure Databricks** runs on:
   - **Azure Storage** for data input/output (ADLS, Blob Storage).
   - **Azure VMs** for Spark clusters.
   - **Azure Key Vault** for secrets management.
2. **Components**:
   - **Control Plane** (managed by Azure Databricks): Manages cluster creation, jobs, security, and logging.
   - **Data Plane**: Executes Spark workloads within your Azure subscription.



---

## Setup and Configuration

### 1. Create an Azure Databricks Workspace

- Go to Azure Portal > **Create Resource** > Search **Databricks** > **Create**.
- Configure:
  - Workspace name
  - Region
  - Pricing tier (Standard/Premium)
- Deploy and access the workspace.

### 2. Manage Clusters

- Go to **Compute** in the workspace.
- **Create Cluster**:
  - Name: User-defined
  - Mode: Standard, High Concurrency, Single Node
  - Autoscaling: Enabled/Disabled
  - Workers: Min/Max workers
  - VM Type: Standard\_DS3\_v2, etc.

### 3. Connect Data

- **ADLS Gen2/Blob Storage**:
  ```python
  spark.conf.set("fs.azure.account.key.<storage_account_name>.dfs.core.windows.net",
                "<storage_account_key>")
  df = spark.read.csv("abfss://<container>@<storage_account_name>.dfs.core.windows.net/path/to/data")
  ```
- **Mount Storage**:
  ```python
  dbutils.fs.mount(
    source="wasbs://<container>@<storage_account_name>.blob.core.windows.net/",
    mount_point="/mnt/<mount-name>",
    extra_configs={"<conf-key>":"<conf-value>"})
  ```
- **Databases & Tables**:
  ```sql
  CREATE DATABASE IF NOT EXISTS my_db;
  USE my_db;
  CREATE TABLE my_table (id INT, name STRING);
  ```

### 4. Security

- **Azure AD** for authentication.
- **Access Control Lists** (ACLs) for workspace resources.
- Use **Azure Key Vault** to manage credentials securely:
  ```python
  dbutils.secrets.get(scope="<scope-name>", key="<key-name>")
  ```

---

## Databricks Notebooks

### Basics

- **Languages**: Python, Scala, SQL, R.
- Switch languages using **magic commands**:
  - `%python`, `%sql`, `%scala`, `%r`
- Comments:
  ```python
  # This is a comment in Python
  -- This is a comment in SQL
  ```

### Example Code

#### Load Data

```python
# Read CSV file
df = spark.read.format("csv").option("header", "true").load("path/to/file.csv")
df.show()
```

#### Run SQL

```sql
%sql
SELECT * FROM my_table LIMIT 10;
```

#### Write Data

```python
df.write.mode("overwrite").parquet("/mnt/output/path")
```

---

## Managing Jobs

- **Create Jobs**:
  - Go to **Jobs** in workspace.
  - Add a new job, specify the notebook/script and cluster.
- **Job Scheduling**:
  - Define periodic runs (e.g., hourly, daily).
- **Run Command**:
  ```python
  dbutils.notebook.run("notebook-name", timeout_seconds=3600, arguments={})
  ```

---

## Advanced Topics

### Delta Lake

- A storage layer that brings ACID transactions and schema enforcement to big data.

**Create Delta Table**:

```python
df.write.format("delta").save("/mnt/delta-table-path")
```

**Query Delta Table**:

```python
df = spark.read.format("delta").load("/mnt/delta-table-path")
df.show()
```

**SQL**:

```sql
CREATE TABLE delta_table USING DELTA LOCATION '/mnt/delta-table-path';
SELECT * FROM delta_table;
```

### MLflow

- Manage Machine Learning workflows (tracking, versioning, and deployment).

**Example**:

```python
import mlflow
mlflow.start_run()
mlflow.log_param("param1", 5)
mlflow.log_metric("rmse", 0.89)
mlflow.end_run()
```

---

## Best Practices

1. **Enable Cluster Autoscaling**: Use cluster autoscaling to automatically adjust compute resources, reducing costs during idle times.
2. **Mount Azure Storage**: Use mounted Azure Storage (Blob or ADLS Gen2) for optimized and efficient data access.
3. **Leverage Delta Lake**: Use **Databricks Delta Lake** for faster queries, versioned data, and ACID transactions on big data.
4. **Secure Secrets with Azure Key Vault**: Use Azure Key Vault to securely manage and access secrets, credentials, and configurations.
5. **Automate Pipelines**: Schedule jobs using Databricks jobs scheduler to automate data ingestion, transformation, and analysis pipelines.
6. **Optimize Cluster Configurations**:
   - Choose appropriate VM sizes.
   - Enable spot instances for non-critical workloads to reduce costs.
   - Monitor cluster metrics to adjust worker node counts.
7. **Version Control Notebooks**: Integrate Databricks notebooks with version control tools like Git to track changes and collaborate effectively.
8. **Optimize Data Storage**:
   - Use Parquet format for efficient storage and querying.
   - Partition large datasets to improve query performance.
9. **Monitor and Log Performance**:
   - Use **Spark UI** and Databricks performance monitoring tools.
   - Track job execution times, resource usage, and optimize bottlenecks.
10. **Follow Security Best Practices**:
    - Implement role-based access controls (RBAC).
    - Use private endpoints to limit access to Databricks resources.
    - Enable encryption for data at rest and in transit.

---

## Pricing

- Azure Databricks pricing depends on:
  - **VM Instance type** (compute)
  - **DBU (Databricks Unit)** consumption
  - **Cluster uptime**

**Pricing tiers**:

- Standard: Basic capabilities.
- Premium: Enhanced features (ACLs, advanced security, Delta Lake).

---

## Useful Commands Reference

### File System

```python
dbutils.fs.ls("/mnt")            # List files
dbutils.fs.cp("source", "dest")   # Copy files
dbutils.fs.rm("/path", True)     # Delete files
```

### Spark SQL

```sql
%sql
SHOW TABLES;
DESCRIBE my_table;
SELECT COUNT(*) FROM my_table;
```

### Cluster Utilities

```python
spark.catalog.listTables()   # List all tables
spark.conf.get("spark.app.id") # Get Spark app ID
```

---

## Resources

- [Azure Databricks Documentation](https://docs.microsoft.com/en-us/azure/databricks)
- [Apache Spark Documentation](https://spark.apache.org/docs/latest)
- [Delta Lake Documentation](https://docs.delta.io)

