# Azure DevOps Handbook and Cheatsheet

## Overview

**Azure DevOps** is a cloud-based platform that provides tools and services to streamline software development and delivery processes. It supports teams with planning, collaboration, automation, version control, testing, and deployment, making it an end-to-end DevOps solution. Whether you're working with agile methodologies, CI/CD pipelines, or infrastructure as code (IaC), Azure DevOps accelerates software delivery while maintaining quality.

This guide provides an organized overview of Azure DevOps components, workflows, and best practices to help you maximize productivity.

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

## Automating CI/CD with Azure Pipelines

Azure Pipelines automate building, testing, and deploying applications. Pipelines can be created using the classic editor or YAML.

### YAML Pipeline Example
Here is a basic YAML pipeline for a .NET application:

```yaml
trigger:
- main

pool:
  vmImage: 'windows-latest'

steps:
- task: UseDotNet@2
  inputs:
    version: '6.x'
    packageType: 'sdk'

- script: dotnet build --configuration Release
  displayName: 'Build Solution'

- script: dotnet test --configuration Release
  displayName: 'Run Unit Tests'

- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: '$(Build.ArtifactStagingDirectory)'
    artifactName: 'drop'
```

### Key CI/CD Concepts
- **Triggers**: Automatically start pipelines on changes to specific branches.
- **Jobs and Stages**: Organize pipelines into sequential tasks.
- **Tasks**: Individual actions such as building, testing, or deploying.
- **Deployment Environments**: Use approvals and checks for controlled deployments.

---

## Managing Artifacts

Azure Artifacts is a package management service that hosts and shares libraries and dependencies.

### Supported Package Types
- **NuGet**: For .NET projects.
- **npm**: Node.js packages.
- **Maven**: Java dependencies.
- **Python**: Python packages.

**Publish a Package**:
```bash
# Authenticate Azure Artifacts feed
npm login --registry https://pkgs.dev.azure.com/<organization>/_packaging/<feed>/npm/registry/

# Publish npm package
npm publish
```

---

## Testing with Azure Test Plans

Azure Test Plans provide manual, exploratory, and automated testing tools to ensure application quality.

### Key Features
- **Test Cases**: Define test steps and expected outcomes.
- **Test Suites**: Group test cases for easier management.
- **Exploratory Testing**: Perform ad-hoc testing to find unexpected issues.
- **Bug Tracking**: Report bugs and link them to test cases.

**Steps to Create a Test Plan**:
1. Navigate to **Test Plans** in your Azure DevOps project.
2. Create a new test plan and add test suites.
3. Define test cases and steps.
4. Execute tests and log results.

---

## Best Practices for Azure DevOps

### General
- Use **YAML pipelines** for versioned, reusable CI/CD configurations.
- Organize projects with clear naming conventions for repos, branches, and pipelines.
- Implement **branch policies** to enforce code quality.

### Security and Compliance
- Use **Azure Active Directory (AAD)** for identity and access management.
- Protect secrets and credentials using **Azure Key Vault**.
- Implement approval gates in pipelines for secure deployments.
- Enable **multi-factor authentication** (MFA) for enhanced security.

### Cost Management
- Optimize pipeline runtimes to reduce compute costs.
- Use **self-hosted agents** for resource-intensive workloads.
- Monitor Azure DevOps usage and configure usage alerts.

### Performance Optimization
- Use **caching** in pipelines for faster builds.
- Implement parallel jobs to reduce pipeline duration.
- Use **Azure Monitor** to track pipeline performance.

---

## Resources

- [Azure DevOps Documentation](https://docs.microsoft.com/en-us/azure/devops)
- [Azure Pipelines YAML Syntax](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema)
- [Azure Repos Git Documentation](https://docs.microsoft.com/en-us/azure/devops/repos)
- [Azure Boards Overview](https://docs.microsoft.com/en-us/azure/devops/boards)
- [Azure Test Plans Documentation](https://docs.microsoft.com/en-us/azure/devops/test-plans)

---

Azure DevOps provides a comprehensive platform for planning, developing, testing, and deploying software, empowering teams to deliver high-quality solutions faster and more efficiently.

