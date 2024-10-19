# GitHub Actions Workflow for Uptime Kuma

![github_action](https://github.com/user-attachments/assets/f33d0203-0234-49b2-a2d2-8603cf170a49)

This repository contains a GitHub Actions workflow to automate the build and deployment of the Uptime Kuma project.

## Table of Contents

- [GitHub Actions Workflow for Uptime Kuma](#github-actions-workflow-for-uptime-kuma)
  - [Table of Contents](#table-of-contents)
  - [Workflow Overview](#workflow-overview)
    - [Triggers](#triggers)
    - [Jobs](#jobs)
      - [Build Job](#build-job)
      - [Deploy Job](#deploy-job)
  - [Secrets](#secrets)
  - [Usage](#usage)
  - [License](#license)
    - [Actions of repo](#actions-of-repo)

## Workflow Overview

The workflow is defined in the [deploy.yml](.github/workflows/deploy.yml) file and consists of two main jobs: `build` and `deploy`.

### Triggers

The workflow is triggered by:
- Push events to the `main` branch.
- Manual dispatch via the GitHub Actions interface.

### Jobs

#### Build Job

- **Runs on**: `ubuntu-latest`
- **Steps**:
  1. **Checkout code**: Uses the `actions/checkout@v2` action to checkout the repository code.
  2. **Build the project**: Installs dependencies and builds the project using npm.

#### Deploy Job

- **Runs on**: `ubuntu-latest`
- **Needs**: `build` (depends on the successful completion of the build job)
- **Steps**:
  1. **Checkout code**: Uses the `actions/checkout@v2` action to checkout the repository code again for the deploy job.
  2. **Debug SSH Connection**: Prepares the SSH private key and tests the SSH connection to the EC2 instance.
  3. **Install Docker (if not installed)**: Installs Docker on the EC2 instance if it's not already installed.
  4. **Stop current Uptime Kuma container**: Stops and removes the current Uptime Kuma container if it exists.
  5. **Deploy new Uptime Kuma container**: Deploys a new Uptime Kuma container.

## Secrets

The workflow requires the following:
- `EC2_SSH_KEY`: SSH private key for connecting to the EC2 instance.

## Usage

To manually trigger the workflow, go to the "Actions" tab in your GitHub repository, select the "Uptime Kuma" workflow, and click "Run workflow".

## License

This project is licensed under the MIT License - see the [LICENSE](../LICENSE) file for details.

### Actions of repo
![Screenshot_20241019_140732](https://github.com/user-attachments/assets/67e6df33-8b8c-496b-92d9-33d1d01b34a2)
