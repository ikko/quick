Here is a **Handbook for Azure DevOps** that targets Python developers looking to integrate, automate, and streamline their workflows with Azure DevOps.

---

# **Azure DevOps for Python Users**

---

## **1. Overview**

Azure DevOps provides a platform for Continuous Integration/Continuous Deployment (CI/CD), project management, and artifact handling. Advanced Python users can automate and integrate Azure DevOps features into their workflows via:

1. **Azure CLI** and **Azure DevOps CLI** for scripting.
2. **Azure Pipelines** for automation (YAML-based CI/CD).
3. **Azure Artifacts** for dependency/package management.
4. **REST APIs** for programmatic control.

---

# **2. Azure DevOps CLI for Python Scripting**

### **Setup Azure DevOps CLI**

1. **Install Azure CLI** and the DevOps extension:
   ```bash
   pip install azure-cli
   az extension add --name azure-devops
   ```

2. **Authenticate to Azure DevOps**:
   ```bash
   az login
   az devops configure --defaults organization=https://dev.azure.com/{org} project={project}
   ```

### **Common Azure CLI Commands**

| **Task**                             | **Command**                                            |
|--------------------------------------|-------------------------------------------------------|
| List repositories                    | `az repos list`                                       |
| Clone a repository                   | `git clone <AzureRepoURL>`                            |
| List pipelines                       | `az pipelines list`                                   |
| Trigger a pipeline                   | `az pipelines run --name {PipelineName}`              |
| Publish an artifact                  | `az artifacts universal publish`                     |
| List work items                      | `az boards work-item list`                            |

---

### **Python Automation with Azure CLI**

Run Azure CLI commands programmatically using Python:
```python
import subprocess

# Run a CLI command to list Azure repositories
command = "az repos list --output json"
result = subprocess.run(command, shell=True, capture_output=True, text=True)

if result.returncode == 0:
    print("Repositories:", result.stdout)
else:
    print("Error:", result.stderr)
```

---

# **3. CI/CD Pipelines for Advanced Python Projects**

### **Key Pipeline Concepts**
- **Pipeline Triggers**: Automate pipeline execution based on commits/tags.
- **Multi-stage Pipelines**: Break pipelines into stages for builds, tests, and deployments.
- **Caching**: Optimize builds by caching dependencies.
- **Environments**: Define approvals and gates for deployment environments.
- **Secrets Management**: Securely use sensitive information like keys and credentials.

---

### **Advanced Python Pipeline (YAML)**

This pipeline:
1. Installs dependencies (cached for efficiency).
2. Runs tests and generates coverage reports.
3. Deploys the app to Azure App Service.

#### **azure-pipelines.yml**
```yaml
trigger:
- main  # Trigger on changes to 'main' branch

variables:
  pythonVersion: '3.10'

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Build
  displayName: "Build and Test"
  jobs:
  - job: BuildJob
    displayName: "Build and Test Python App"
    steps:
    - task: UsePythonVersion@0
      inputs:
        versionSpec: '$(pythonVersion)'
      displayName: "Use Python $(pythonVersion)"

    - task: Cache@2  # Cache dependencies for faster builds
      inputs:
        key: 'pip | "$(Agent.OS)" | requirements.txt'
        restoreKeys: 'pip | "$(Agent.OS)"'
        path: '~/.cache/pip'

    - script: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
      displayName: "Install Dependencies"

    - script: |
        pytest --junitxml=test-results.xml --cov=my_app
      displayName: "Run Tests"

    - task: PublishTestResults@2
      inputs:
        testResultsFormat: 'JUnit'
        testResultsFiles: 'test-results.xml'
      displayName: "Publish Test Results"

    - task: PublishCodeCoverageResults@1
      inputs:
        codeCoverageTool: 'Cobertura'
        summaryFileLocation: 'coverage.xml'
      displayName: "Publish Code Coverage"

- stage: Deploy
  displayName: "Deploy to Azure App Service"
  jobs:
  - job: DeployJob
    displayName: "Deploy Application"
    steps:
    - task: ArchiveFiles@2
      inputs:
        rootFolderOrFile: '$(System.DefaultWorkingDirectory)'
        archiveFile: '$(Build.ArtifactStagingDirectory)/app.zip'
      displayName: "Archive Application"

    - task: AzureWebApp@1
      inputs:
        azureSubscription: '<ServiceConnection>'
        appName: 'my-python-app'
        package: '$(Build.ArtifactStagingDirectory)/app.zip'
      displayName: "Deploy to Azure Web App"
```

---

## **4. Advanced Testing and Reporting**

### **Running Tests with `pytest`**
1. Install `pytest` and coverage tools:
   ```bash
   pip install pytest pytest-cov
   ```

2. Run tests and generate coverage reports:
   ```bash
   pytest --cov=my_app --junitxml=test-results.xml
   ```

### **Publish Test and Coverage Reports in Pipeline**
```yaml
- task: PublishTestResults@2
  inputs:
    testResultsFormat: 'JUnit'
    testResultsFiles: '**/test-results.xml'
  displayName: "Publish Test Results"

- task: PublishCodeCoverageResults@1
  inputs:
    codeCoverageTool: 'Cobertura'
    summaryFileLocation: 'coverage.xml'
  displayName: "Publish Code Coverage"
```

---

## **5. Secrets Management**

Integrate **Azure Key Vault** for secrets management.

### **Store and Retrieve Secrets**

1. **Add Key Vault Task in Pipeline**:
   ```yaml
   - task: AzureKeyVault@2
     inputs:
       azureSubscription: '<ServiceConnection>'
       KeyVaultName: '<KeyVaultName>'
       SecretsFilter: '*'
     displayName: "Fetch Secrets from Key Vault"
   ```

2. **Access Secrets**:
   ```yaml
   - script: |
       echo "Secret: $(my-secret)"
     displayName: "Use Secrets in Pipeline"
   ```

---

## **6. REST APIs for Azure DevOps**

Leverage the **Azure DevOps REST API** for advanced automation.

### **1. List Pipelines**
```python
import requests
from requests.auth import HTTPBasicAuth

organization = "<organization>"
project = "<project>"
personal_access_token = "PAT"  # Azure DevOps Personal Access Token

url = f"https://dev.azure.com/{organization}/{project}/_apis/pipelines?api-version=6.0"
response = requests.get(url, auth=HTTPBasicAuth("", personal_access_token))

if response.status_code == 200:
    pipelines = response.json()
    for pipeline in pipelines['value']:
        print(f"Pipeline ID: {pipeline['id']}, Name: {pipeline['name']}")
else:
    print("Error:", response.status_code, response.text)
```

### **2. Trigger a Pipeline**
```python
url = f"https://dev.azure.com/{organization}/{project}/_apis/pipelines/{pipeline_id}/runs?api-version=6.0"
response = requests.post(url, auth=HTTPBasicAuth("", personal_access_token), json={})

print("Pipeline Triggered:", response.status_code)
```

---

## **7. Cheatsheet**

### **Azure CLI Commands**
| **Task**                    | **Command**                                        |
|-----------------------------|---------------------------------------------------|
| Login to Azure DevOps       | `az login`                                        |
| Set Defaults                | `az devops configure --defaults organization=...` |
| Trigger a Pipeline          | `az pipelines run --name {PipelineName}`          |
| List Artifacts              | `az artifacts universal list`                     |
| Fetch Work Items            | `az boards work-item list`                        |

---

### **Pipeline Best Practices**
1. Use **caching** to speed up dependency installation.
2. Integrate **Azure Key Vault** for secrets.
3. Use **multi-stage pipelines** for build-test-deploy workflows.
4. Publish **test results** and **code coverage** for visibility.
5. Automate pipeline creation and triggers with **REST API** and **CLI**.

---

## **Summary**

This advanced handbook demonstrates how Python developers can fully integrate Azure DevOps into their workflows. By leveraging CI/CD pipelines, CLI automation, REST APIs, and Key Vault secrets, Python projects can achieve robust automation, testing, and deployment pipelines.
