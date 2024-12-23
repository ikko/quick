# Azure Databricks Cheatsheet

## Overview

**Azure Databricks** is a robust, cloud-based analytics platform that delivers high-performance solutions for big data processing and artificial intelligence. Built on **Apache Spark**, it seamlessly integrates with Microsoft Azure's cloud ecosystem, offering scalability, advanced data analytics capabilities, and an environment tailored for collaboration across teams. Whether handling batch workloads, real-time streaming, or advanced machine learning pipelines, Azure Databricks simplifies data engineering and analytics at scale.

This cheatsheet is designed to help you quickly understand the key features, components, and best practices for efficiently using Azure Databricks. 

---

## Key Concepts

- **Apache Spark**: An open-source, distributed data processing engine that supports high-performance computing for large-scale data processing, machine learning, and streaming analytics.
- **Workspace**: A collaborative hub where data teams organize and manage projects, notebooks, jobs, clusters, and libraries.
- **Clusters**: Compute resources that execute Spark workloads. Clusters can scale dynamically to accommodate varying data loads and workloads.
- **Notebooks**: Interactive documents that allow users to write and execute code in multiple languages (Python, SQL, Scala, R) while visualizing and analyzing results.
- **Jobs**: Scheduled tasks for automating the execution of notebooks or standalone applications.
- **DBFS (Databricks File System)**: A layer on top of Azure Storage that acts as a distributed file system for reading and writing data within Databricks.
- **Libraries**: Code dependencies (e.g., Python packages, JAR files) that can be installed for clusters and notebooks.
- **Delta Lake**: A storage layer that brings ACID transactions, schema enforcement, and scalable metadata to big data workloads on Databricks.

---

## Architecture Overview

Azure Databricks operates using a two-plane architecture:

1. **Control Plane** (Managed by Azure Databricks):
   - Oversees the creation, configuration, and management of clusters.
   - Handles metadata, logging, orchestration, and monitoring.
   - Provides a user-friendly web-based interface for managing jobs and resources.

2. **Data Plane** (Within Your Azure Subscription):
   - Spark compute workloads execute on Azure VMs inside your subscription.
   - Securely interacts with Azure Storage (Blob or ADLS) for data access.

### Core Integrations
- **Azure Data Lake Storage (ADLS)** and **Blob Storage**: Storage backends for structured, semi-structured, and unstructured data.
- **Azure Key Vault**: Provides secure storage for credentials, keys, and secrets used in data processing workflows.
- **Azure Active Directory (AAD)**: Handles authentication, role-based access control (RBAC), and single sign-on (SSO) for enterprise-level security.
- **Azure Synapse Analytics**: Integration for querying large datasets in conjunction with Databricks for processing and analysis.
- **Azure Monitor**: Provides monitoring, diagnostics, and logging capabilities for analyzing job performance and cluster health.

---

## Setup and Configuration

### 1. Creating a Databricks Workspace

1. In **Azure Portal**:
   - Navigate to **Create Resource** and search for **Azure Databricks**.
2. Configure the Workspace:
   - **Workspace Name**: Enter a descriptive name.
   - **Region**: Select the appropriate Azure region for proximity and cost efficiency.
   - **Pricing Tier**: Choose between **Standard** (basic) or **Premium** (advanced features).
3. Click **Create** and wait for the deployment to complete.
4. Access the workspace via the Azure Databricks portal and begin configuring clusters, notebooks, and jobs.

### 2. Cluster Management

Clusters are the backbone of Spark workloads. A well-configured cluster ensures efficient resource usage and cost management.

**Steps to Create a Cluster**:
1. Go to the **Compute** tab within the Databricks workspace.
2. Click **Create Cluster** and configure:
   - **Cluster Name**: Define a meaningful name for the cluster.
   - **Cluster Mode**: Select from **Standard**, **High Concurrency**, or **Single Node**.
   - **Autoscaling**: Enable to allow dynamic adjustment of worker nodes based on workload demand.
   - **VM Configuration**: Choose appropriate Azure VM SKUs (e.g., Standard\_DS3\_v2) for drivers and workers.
   - **Libraries**: Add required libraries (Python, Maven, or Scala).

**Cluster Autoscaling**:
- Reduces costs by dynamically adjusting the number of worker nodes based on demand.
- Ensures sufficient capacity for heavy workloads while scaling down during idle periods.

### 3. Connect to Data

Azure Databricks integrates seamlessly with Azure storage accounts for data processing.

#### Accessing ADLS or Blob Storage
```python
# Setting up access to Azure Data Lake Storage (ADLS)
spark.conf.set("fs.azure.account.key.<storage_account_name>.dfs.core.windows.net",
              "<storage_account_key>")

# Read data stored in Azure Blob Storage
df = spark.read.format("csv").option("header", "true").load("abfss://<container>@<storage_account>.dfs.core.windows.net/data")
df.show()
```

#### Mounting Storage to Databricks
```python
# Mount Azure Blob Storage
dbutils.fs.mount(
  source="wasbs://<container>@<storage_account>.blob.core.windows.net/",
  mount_point="/mnt/<mount-name>",
  extra_configs={"<conf-key>":"<conf-value>"}
)
```

---

## Working with Databricks Notebooks

### Key Features of Notebooks
- **Multi-language Support**: Use `%python`, `%sql`, `%scala`, or `%r` commands to switch between languages.
- **Magic Commands**: Simplify file management, display outputs, and run other notebooks.
- **Rich Visualizations**: Use built-in charts and graphs to analyze Spark results visually.
- **Collaborative Editing**: Share notebooks with teammates and perform real-time collaborative editing.

### Common Workflow Examples

**Read and Display Data**:
```python
# Load data into a DataFrame
df = spark.read.format("csv").option("header", "true").load("/mnt/data/sample.csv")
df.show(10)
```

**Running SQL Queries**:
```sql
%sql
SELECT column1, COUNT(*) AS count
FROM sample_table
GROUP BY column1;
```

**Writing Output Data**:
```python
# Save DataFrame as a Parquet file
df.write.mode("overwrite").parquet("/mnt/output/destination")
```

---

## Managing Jobs and Pipelines

Automating workflows using **Databricks Jobs** is essential for production deployments.

### Job Creation and Scheduling
1. In the workspace, navigate to the **Jobs** tab.
2. Create a new job and:
   - Assign a notebook or JAR file.
   - Attach a cluster for job execution.
   - Schedule the job (e.g., hourly, daily, weekly).

### Running Notebooks Programmatically
```python
# Run another notebook programmatically
dbutils.notebook.run("other_notebook", timeout_seconds=1800, arguments={})
```

---

## Best Practices for Azure Databricks

### Performance Optimization
- **Enable Cluster Autoscaling** to manage costs and performance efficiently.
- **Partition Large Datasets** to minimize query execution time.
- Use **Delta Lake** for ACID transactions and incremental updates.
- Optimize file formats: prefer **Parquet** or **Delta** over CSV.

### Cost Management
- Use **spot VMs** for non-critical workloads to save costs.
- Implement idle timeouts for clusters to reduce unused compute costs.
- Monitor cluster usage and right-size VM configurations.

### Security and Governance
- Use **Azure Key Vault** to securely manage secrets and credentials.
- Apply **RBAC** policies for fine-grained user permissions.
- Encrypt data **at rest** using Azure Storage encryption.
- Use **private endpoints** to secure network communication.

---

## Resources

- [Azure Databricks Documentation](https://docs.microsoft.com/en-us/azure/databricks)
- [Apache Spark Documentation](https://spark.apache.org/docs/latest)
- [Delta Lake Documentation](https://docs.delta.io)
- [MLflow Documentation](https://mlflow.org)

---

Azure Databricks simplifies the complex process of handling big data and advanced analytics, making it the go-to platform for modern data engineering and AI solutions. Whether you're building pipelines, running Spark jobs, or training ML models, it delivers unparalleled flexibility and performance in the Azure ecosystem.
