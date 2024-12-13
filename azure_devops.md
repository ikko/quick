Here’s a **comprehensive Azure DevOps Handbook and Cheatsheet** with a focus on **Python** integration. This guide covers CI/CD pipelines, repository management, testing, deployment, and other Azure DevOps features.

---

# **Azure DevOps Handbook**

Azure DevOps is a suite of tools to manage software development lifecycles:

---

## Key Concepts

- **Azure DevOps Services**: A suite of services to manage software development, including Boards, Repos, Pipelines, Test Plans, and Artifacts.
- **Azure Repos**: A version control system supporting Git or TFVC repositories for tracking changes to code.
- **Azure Boards**: A tool for planning and tracking work items, sprints, and backlogs.
- **Azure Pipelines**: Automation pipelines for Continuous Integration (CI) and Continuous Deployment (CD).
- **Azure Artifacts**: A package management system for storing, sharing, and managing dependencies.
- **Azure Test Plans**: Tools for testing, tracking bugs, and ensuring application quality.
- **Work Items**: Trackable units of work like user stories, tasks, bugs, and issues.

### Core DevOps Principles
- **CI/CD (Continuous Integration and Deployment)**: Automate building, testing, and deploying code.
- **Version Control**: Manage and track changes to source code effectively.
- **Agile Project Management**: Use sprints, backlogs, and boards to manage tasks.
- **Shift-Left Testing**: Integrate testing earlier in the development lifecycle.
- **Infrastructure as Code (IaC)**: Manage infrastructure declaratively with tools like Bicep or Terraform.

---

## Architecture and Components

### Azure DevOps Services
Azure DevOps is divided into five key components:

1. **Azure Boards**
   - Plan, track, and discuss work.
   - Includes tools like Kanban boards, backlogs, and sprint planning.
2. **Azure Repos**
   - Supports Git repositories or Team Foundation Version Control (TFVC).
   - Built-in pull request reviews and branch policies.
3. **Azure Pipelines**
   - Build, test, and deploy applications to any cloud or on-premises system.
   - Supports YAML and classic pipeline formats.
4. **Azure Artifacts**
   - Manage and share packages (NuGet, npm, Maven, Python).
   - Enable caching for faster builds.
5. **Azure Test Plans**
   - Manual and exploratory testing.
   - Track bugs, user stories, and testing coverage.

---

## Setup and Configuration

### 1. Creating an Azure DevOps Organization
1. Go to [Azure DevOps Portal](https://dev.azure.com).
2. Sign in with your Microsoft account.
3. Click **Create New Organization**.
4. Create a project within the organization:
   - Choose **Public** (open) or **Private** (restricted access).
   - Select version control: **Git** or **TFVC**.
   - Configure the methodology: **Agile**, **Scrum**, or **CMMI**.

### 2. Configuring Azure Repos
Azure Repos provides source control for managing code:
- **Git Repos**: Distributed version control system supporting branching, merging, and pull requests.
- **TFVC**: Centralized version control system for managing changes.

**Steps to Initialize a Repo**:
```bash
# Clone an Azure Repo locally
git clone https://dev.azure.com/<organization>/<project>/_git/<repository>

# Commit and push changes
git add .
git commit -m "Initial commit"
git push origin main
```

**Branching Strategy**:
- Use **GitFlow** for feature development.
- Protect **main** and **release** branches using branch policies.
- Enforce pull requests for code reviews.

---

## Working with Azure Boards

Azure Boards helps teams manage projects with features like backlogs, Kanban boards, and sprint planning.

### Key Components
- **Epics**: High-level objectives that span across sprints.
- **Features**: Grouped user stories that deliver incremental functionality.
- **User Stories**: Work items that describe functionality from a user’s perspective.
- **Tasks**: Small units of work required to complete a user story.
- **Bugs**: Track and manage application defects.

**Basic Workflow**:
1. Define epics, features, and user stories in the backlog.
2. Use sprints to plan short, incremental cycles of work.
3. Track progress using **Boards** and **Dashboards**.

---

## **1. Azure Repos**

### **Clone a Repository**
Clone a repository locally:
```bash
git clone https://dev.azure.com/{organization}/{project}/_git/{repository}
```

### **Add and Commit Changes**
```bash
git add .                     # Stage all changes
git commit -m "Commit message"
git push origin main          # Push to Azure Repos
```

### **Branching**
```bash
# Create a new branch
git checkout -b feature/new-feature

# Push the branch
git push origin feature/new-feature
```

### **Pull Requests**
1. Go to Azure Repos → **Pull Requests**.
2. Select the source and target branches.
3. Add reviewers and submit.

---

## **2. Azure Pipelines**

Azure Pipelines automates builds, tests, and deployments using YAML files.

### **Setup Pipeline**

1. Create a `azure-pipelines.yml` in the root directory.
2. Define the CI/CD pipeline steps.

---

### **3.1 Python CI Pipeline Example**
```yaml
trigger:
- main  # Trigger pipeline on pushes to 'main'

pool:
  vmImage: 'ubuntu-latest'  # Use Ubuntu VM for pipeline

steps:
- task: UsePythonVersion@0  # Install Python
  inputs:
    versionSpec: '3.10'

- script: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
  displayName: 'Install Dependencies'

- script: |
    python -m unittest discover tests/
  displayName: 'Run Unit Tests'

- task: PublishTestResults@2
  inputs:
    testResultsFormat: 'JUnit'
    testResultsFiles: '**/test-results.xml'
  displayName: 'Publish Test Results'

- script: |
    python main.py
  displayName: 'Run Application'
```

---

### **3.2 Variables and Secrets**
Store sensitive information in Azure DevOps **Pipeline Variables**.

1. Go to **Pipeline Settings** → **Variables**.
2. Add secrets (e.g., `MY_SECRET`).

Access secrets in `azure-pipelines.yml`:
```yaml
- script: |
    echo "Secret: $(MY_SECRET)"
  displayName: 'Access Secrets'
```

---

### **3.3 Pipeline Templates**

Reuse pipeline logic with **Templates**.

#### **Template File (build-template.yml)**
```yaml
steps:
- script: |
    pip install -r requirements.txt
  displayName: 'Install Dependencies'
```

#### **Main Pipeline**
```yaml
trigger: [main]

pool: ubuntu-latest

extends:
  template: build-template.yml
```

---

## **4. Azure Artifacts**

Azure Artifacts hosts Python packages (or other artifacts).

### **1. Publish a Python Package**

1. Create a **feed** in Azure Artifacts.
2. Install **`twine`**:
   ```bash
   pip install twine
   ```

3. Configure `~/.pypirc` for Azure Artifacts:
   ```ini
   [distutils]
   index-servers = azure

   [azure]
   repository: https://pkgs.dev.azure.com/{organization}/_packaging/{feed}/pypi/upload/
   username: __token__
   password: {Azure_Artifacts_PAT}
   ```

4. Upload Package:
   ```bash
   python setup.py sdist
   twine upload -r azure dist/*
   ```

---

## **4. Azure Boards**

Azure Boards is for agile project management.

### **5. Key Terms**
- **Work Items**: Tasks, bugs, user stories.
- **Boards**: Kanban board to visualize tasks.
- **Backlog**: List of work items to be completed.
- **Sprint**: Iteration with a defined scope and timebox.

---

### **6. Integrate Azure Boards with Git Commits**
Add Work Item ID in commit messages:
```bash
git commit -m "Fix login issue. Resolves #12345"
```

---

## **7. Azure DevOps CLI**

Install the **Azure CLI** and **Azure DevOps extension**:
```bash
# Install CLI
pip install azure-cli

# Install Azure DevOps extension
az extension add --name azure-devops
```

### **Login to Azure DevOps**
```bash
az login
az devops configure --defaults organization=https://dev.azure.com/{organization} project={project}
```

### **Common Commands**
| **Command**                     | **Description**                         |
|---------------------------------|-----------------------------------------|
| `az repos list`                 | List all repositories                   |
| `az pipelines run`              | Trigger a pipeline                      |
| `az boards work-item list`      | List work items                         |
| `az artifacts universal publish`| Publish a universal package to a feed   |

---

## **8. Testing in Azure Pipelines**

### **Run Python Unit Tests**
Add unit tests using `unittest`:
```python
import unittest

class TestExample(unittest.TestCase):
    def test_addition(self):
        self.assertEqual(1 + 1, 2)

if __name__ == "__main__":
    unittest.main()
```

Run the tests in the pipeline:
```yaml
- script: |
    python -m unittest discover tests/
  displayName: 'Run Python Unit Tests'
```

---
## Key Concepts

- **Azure DevOps Services**: A suite of services to manage software development, including Boards, Repos, Pipelines, Test Plans, and Artifacts.
- **Azure Repos**: A version control system supporting Git or TFVC repositories for tracking changes to code.
- **Azure Boards**: A tool for planning and tracking work items, sprints, and backlogs.
- **Azure Pipelines**: Automation pipelines for Continuous Integration (CI) and Continuous Deployment (CD).
- **Azure Artifacts**: A package management system for storing, sharing, and managing dependencies.
- **Azure Test Plans**: Tools for testing, tracking bugs, and ensuring application quality.
- **Work Items**: Trackable units of work like user stories, tasks, bugs, and issues.

### Core DevOps Principles
- **CI/CD (Continuous Integration and Deployment)**: Automate building, testing, and deploying code.
- **Version Control**: Manage and track changes to source code effectively.
- **Agile Project Management**: Use sprints, backlogs, and boards to manage tasks.
- **Shift-Left Testing**: Integrate testing earlier in the development lifecycle.
- **Infrastructure as Code (IaC)**: Manage infrastructure declaratively with tools like Bicep or Terraform.

---

## Architecture and Components

### Azure DevOps Services
Azure DevOps is divided into five key components:

1. **Azure Boards**
   - Plan, track, and discuss work.
   - Includes tools like Kanban boards, backlogs, and sprint planning.
2. **Azure Repos**
   - Supports Git repositories or Team Foundation Version Control (TFVC).
   - Built-in pull request reviews and branch policies.
3. **Azure Pipelines**
   - Build, test, and deploy applications to any cloud or on-premises system.
   - Supports YAML and classic pipeline formats.
4. **Azure Artifacts**
   - Manage and share packages (NuGet, npm, Maven, Python).
   - Enable caching for faster builds.
5. **Azure Test Plans**
   - Manual and exploratory testing.
   - Track bugs, user stories, and testing coverage.

---

## Setup and Configuration

### 1. Creating an Azure DevOps Organization
1. Go to [Azure DevOps Portal](https://dev.azure.com).
2. Sign in with your Microsoft account.
3. Click **Create New Organization**.
4. Create a project within the organization:
   - Choose **Public** (open) or **Private** (restricted access).
   - Select version control: **Git** or **TFVC**.
   - Configure the methodology: **Agile**, **Scrum**, or **CMMI**.

### 2. Configuring Azure Repos
Azure Repos provides source control for managing code:
- **Git Repos**: Distributed version control system supporting branching, merging, and pull requests.
- **TFVC**: Centralized version control system for managing changes.

**Steps to Initialize a Repo**:
```bash
# Clone an Azure Repo locally
git clone https://dev.azure.com/<organization>/<project>/_git/<repository>

# Commit and push changes
git add .
git commit -m "Initial commit"
git push origin main
```

**Branching Strategy**:
- Use **GitFlow** for feature development.
- Protect **main** and **release** branches using branch policies.
- Enforce pull requests for code reviews.

---

## Working with Azure Boards

Azure Boards helps teams manage projects with features like backlogs, Kanban boards, and sprint planning.

### Key Components
- **Epics**: High-level objectives that span across sprints.
- **Features**: Grouped user stories that deliver incremental functionality.
- **User Stories**: Work items that describe functionality from a user’s perspective.
- **Tasks**: Small units of work required to complete a user story.
- **Bugs**: Track and manage application defects.

**Basic Workflow**:
1. Define epics, features, and user stories in the backlog.
2. Use sprints to plan short, incremental cycles of work.
3. Track progress using **Boards** and **Dashboards**.

---

## **Azure DevOps Cheatsheet**

| **Task**                        | **Command or Step**                      |
|---------------------------------|-----------------------------------------|
| Clone a Repo                    | `git clone <Azure Repo URL>`            |
| Run Pipeline Manually           | `az pipelines run`                      |
| Publish Python Package          | `twine upload -r azure dist/*`          |
| Cache Dependencies              | Use `Cache@2` in pipelines              |
| Deploy to App Service           | `AzureWebApp@1` task                    |
| Access Key Vault Secrets        | `AzureKeyVault@2` task                  |
| Test Python Code                | `python -m unittest`                    |

---

## **Summary**

This Azure DevOps handbook covers core concepts like CI/CD pipelines, Python project deployment, and integration of key services such as Azure Repos, Pipelines, Boards, and Key Vault. By automating workflows with Azure Pipelines and managing secrets effectively, you can streamline Python development and deployment.

---

## **1. Azure Repos**

### **Clone a Repository**
Clone a repository locally:
```bash
git clone https://dev.azure.com/{organization}/{project}/_git/{repository}
```

### **Add and Commit Changes**
```bash
git add .                     # Stage all changes
git commit -m "Commit message"
git push origin main          # Push to Azure Repos
```

### **Branching**
```bash
# Create a new branch
git checkout -b feature/new-feature

# Push the branch
git push origin feature/new-feature
```

### **Pull Requests**
1. Go to Azure Repos → **Pull Requests**.
2. Select the source and target branches.
3. Add reviewers and submit.

---

## **9. Azure Pipelines**

Azure Pipelines automates builds, tests, and deployments using YAML files.

### **Setup Pipeline**

1. Create a `azure-pipelines.yml` in the root directory.
2. Define the CI/CD pipeline steps.

---

### **9.1 Python CI Pipeline Example**
```yaml
trigger:
- main  # Trigger pipeline on pushes to 'main'

pool:
  vmImage: 'ubuntu-latest'  # Use Ubuntu VM for pipeline

steps:
- task: UsePythonVersion@0  # Install Python
  inputs:
    versionSpec: '3.10'

- script: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
  displayName: 'Install Dependencies'

- script: |
    python -m unittest discover tests/
  displayName: 'Run Unit Tests'

- task: PublishTestResults@2
  inputs:
    testResultsFormat: 'JUnit'
    testResultsFiles: '**/test-results.xml'
  displayName: 'Publish Test Results'

- script: |
    python main.py
  displayName: 'Run Application'
```

---

### **9.2 Variables and Secrets**
Store sensitive information in Azure DevOps **Pipeline Variables**.

1. Go to **Pipeline Settings** → **Variables**.
2. Add secrets (e.g., `MY_SECRET`).

Access secrets in `azure-pipelines.yml`:
```yaml
- script: |
    echo "Secret: $(MY_SECRET)"
  displayName: 'Access Secrets'
```

---

### **9.3 Pipeline Templates**

Reuse pipeline logic with **Templates**.

#### **Template File (build-template.yml)**
```yaml
steps:
- script: |
    pip install -r requirements.txt
  displayName: 'Install Dependencies'
```

#### **Main Pipeline**
```yaml
trigger: [main]

pool: ubuntu-latest

extends:
  template: build-template.yml
```

---

## **10. Azure Artifacts**

Azure Artifacts hosts Python packages (or other artifacts).

### Publish a Python Package**

1. Create a **feed** in Azure Artifacts.
2. Install **`twine`**:
   ```bash
   pip install twine
   ```

3. Configure `~/.pypirc` for Azure Artifacts:
   ```ini
   [distutils]
   index-servers = azure

   [azure]
   repository: https://pkgs.dev.azure.com/{organization}/_packaging/{feed}/pypi/upload/
   username: __token__
   password: {Azure_Artifacts_PAT}
   ```

4. Upload Package:
   ```bash
   python setup.py sdist
   twine upload -r azure dist/*
   ```

---

## **11. Azure Boards**

Azure Boards is for agile project management.

### **1. Key Terms**
- **Work Items**: Tasks, bugs, user stories.
- **Boards**: Kanban board to visualize tasks.
- **Backlog**: List of work items to be completed.
- **Sprint**: Iteration with a defined scope and timebox.

---

### **2. Integrate Azure Boards with Git Commits**
Add Work Item ID in commit messages:
```bash
git commit -m "Fix login issue. Resolves #12345"
```

---

## **12. Azure DevOps CLI**

Install the **Azure CLI** and **Azure DevOps extension**:
```bash
# Install CLI
pip install azure-cli

# Install Azure DevOps extension
az extension add --name azure-devops
```

### **Login to Azure DevOps**
```bash
az login
az devops configure --defaults organization=https://dev.azure.com/{organization} project={project}
```

### **Common Commands**
| **Command**                     | **Description**                         |
|---------------------------------|-----------------------------------------|
| `az repos list`                 | List all repositories                   |
| `az pipelines run`              | Trigger a pipeline                      |
| `az boards work-item list`      | List work items                         |
| `az artifacts universal publish`| Publish a universal package to a feed   |

---

## **13. Testing in Azure Pipelines**

### **Run Python Unit Tests**
Add unit tests using `unittest`:
```python
import unittest

class TestExample(unittest.TestCase):
    def test_addition(self):
        self.assertEqual(1 + 1, 2)

if __name__ == "__main__":
    unittest.main()
```

Run the tests in the pipeline:
```yaml
- script: |
    python -m unittest discover tests/
  displayName: 'Run Python Unit Tests'
```

---

## **14. Deployment with Azure Pipelines**

### **1. Deploy to Azure App Service**
**azure-pipelines.yml**:
```yaml
trigger: [main]

pool:
  vmImage: 'ubuntu-latest'

variables:
  azureSubscription: 'my-subscription'
  appName: 'my-flask-app'

steps:
- task: UsePythonVersion@0
  inputs:
    versionSpec: '3.10'

- script: |
    pip install -r requirements.txt
  displayName: 'Install Dependencies'

- task: ArchiveFiles@2
  inputs:
    rootFolderOrFile: '$(System.DefaultWorkingDirectory)'
    archiveFile: '$(Build.ArtifactStagingDirectory)/app.zip'

- task: AzureWebApp@1
  inputs:
    azureSubscription: '$(azureSubscription)'
    appName: '$(appName)'
    package: '$(Build.ArtifactStagingDirectory)/app.zip'
```

---

## **15. Pipeline Cache and Artifacts**

### **Cache Dependencies**
```yaml
steps:
- task: Cache@2
  inputs:
    key: 'python | "$(Agent.OS)" | requirements.txt'
    path: '~/.cache/pip'
- script: pip install -r requirements.txt
```

### **Publish Build Artifacts**
```yaml
- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'drop'
    publishLocation: 'Container'
```

---

## **16. Secrets Management**

Integrate Azure Key Vault to manage sensitive secrets:
```yaml
- task: AzureKeyVault@2
  inputs:
    azureSubscription: 'my-subscription'
    KeyVaultName: 'my-keyvault'
    SecretsFilter: '*'
```

Access secrets as variables:
```yaml
- script: echo "My secret is $(my-secret)"
```

---

## **Azure DevOps Cheatsheet**

| **Task**                        | **Command or Step**                      |
|---------------------------------|-----------------------------------------|
| Clone a Repo                    | `git clone <Azure Repo URL>`            |
| Run Pipeline Manually           | `az pipelines run`                      |
| Publish Python Package          | `twine upload -r azure dist/*`          |
| Cache Dependencies              | Use `Cache@2` in pipelines              |
| Deploy to App Service           | `AzureWebApp@1` task                    |
| Access Key Vault Secrets        | `AzureKeyVault@2` task                  |
| Test Python Code                | `python -m unittest`                    |

---

## **Summary**

This Azure DevOps handbook covers core concepts like CI/CD pipelines, Python project deployment, and integration of key services such as Azure Repos, Pipelines, Boards, and Key Vault. By automating workflows with Azure Pipelines and managing secrets effectively, you can streamline Python development and deployment.


