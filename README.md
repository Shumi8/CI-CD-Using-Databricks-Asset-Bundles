# CI/CD using Databricks Asset Bundles

This repository contains the configuration for a **CI/CD pipeline** implemented for Denmark's largest retail organization using **Azure DevOps** and **Databricks Asset Bundles**. The pipeline automates the deployment of Databricks jobs to a development environment, ensuring that updates to key configuration files trigger an efficient deployment workflow.

## Features

- **Branch-Specific Triggers**: The pipeline only triggers when specific branches (e.g., `CustomerSuccess`) or configuration files (e.g., `JobConfiguration.yml`) are modified.
- **Python Environment Setup**: The pipeline ensures a Python 3.8 environment is used for all deployments, along with installing the required Python dependencies.
- **Databricks CLI Integration**: Uses the Databricks CLI to validate and deploy asset bundles directly to a Databricks workspace.
- **Scheduled Databricks Jobs**: The pipeline includes job scheduling using cron expressions to ensure tasks are executed at predefined intervals.

## Technologies Used

### 1. **Azure Pipelines**
- The pipeline is defined using the `azure-pipelines.yml` file, automating deployment for Databricks Asset Bundles. Key stages include:
  - **Deploy to Development**: Executes the deployment of Databricks bundles to the development environment when triggered.

### 2. **Databricks Asset Bundles**
- **Databricks CLI**: The pipeline installs the Databricks CLI for automating interactions with the Databricks workspace, including bundle validation and deployment.
- **Bundle Configuration**: The `databricks.yml` file defines the asset bundle configuration, specifying which files to include in the bundle and setting up environment-specific targets.

### 3. **Python**
- Python 3.8 is used for running various scripts, including the installation of dependencies and Databricks CLI setup.

### 4. **Job Scheduling**
- **JobConfiguration.yml**: Defines the Databricks jobs and their respective tasks, including:
  - **Job Scheduling**: Schedules job execution using a Quartz cron expression.
  - **Email Notifications**: Configures email notifications to notify on job failures.
  - **Task Execution**: Specifies multiple tasks (e.g., `FunctionApp1.py`, `FunctionApp2.py`) that are executed as part of the job.

## Pipeline Workflow

### 1. **Trigger Configuration**
- The pipeline is configured to trigger only when changes are made to the `CustomerSuccess` branch or specific files like `JobConfiguration.yml` under the `CustomerService/Resources` directory.

### 2. **Stage: Deploy to Development**
- **Environment Setup**: The pipeline sets up the Python environment (Python 3.8), installs dependencies, and checks out the source code.
- **Databricks CLI Installation**: The pipeline installs the latest version of the Databricks CLI for managing the deployment process.
- **Bundle Validation**: Before deploying, the Databricks bundle is validated to ensure all configurations are correct.
- **Bundle Deployment**: Upon successful validation, the Databricks bundle is deployed to the development environment.

### 3. **Job Configuration**
- The `JobConfiguration.yml` file specifies the details of the jobs to be executed in Databricks:
  - **Tasks**: Defines tasks that run notebooks located in the `FunctionApp` directory.
  - **Clusters**: Configures auto-scaling clusters that are used to run the jobs.
  - **Notifications**: Sends email alerts in case of job failures.

### 4. **Databricks YAML Configuration**
- The `databricks.yml` file defines the Databricks asset bundle and the target environment (development). It includes:
  - **Bundle Name**: Specifies the name of the bundle (e.g., `CustomerSuccess`).
  - **Include Directives**: Specifies which files to include in the bundle.
  - **Target Configuration**: Defines the development environment configuration, including the Databricks instance and workspace root path.

## Configuration Files

### 1. **azure-pipelines.yml**
This file defines the CI/CD pipeline for automating deployments to Databricks using Databricks Asset Bundles.

### 2. **JobConfiguration.yml**
This file defines the job schedule, tasks, and clusters for Databricks jobs, including email notifications on job failures.

### 3. **databricks.yml**
This file defines the Databricks bundle and specifies which files to include in the bundle and the environment targets for deployment.

## Usage

1. **Triggering the Pipeline**
   - The pipeline will automatically trigger when changes are made to the `CustomerSuccess` branch or the `JobConfiguration.yml` file under `CustomerService/Resources`.

2. **Validating and Deploying Bundles**
   - Upon triggering, the pipeline will validate and deploy the Databricks Asset Bundle to the development environment using the Databricks CLI.

3. **Managing Job Configurations**
   - Update the `JobConfiguration.yml` file to adjust task scheduling, add new tasks, or configure job clusters.

## Key Components

- **Azure Pipelines**: Automates the CI/CD workflow.
- **Databricks CLI**: Facilitates bundle validation and deployment.
- **Databricks Asset Bundles**: Manages the deployment of Databricks jobs and resources.
- **Python**: Used for environment setup and running deployment scripts.
