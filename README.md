# DevOps Project

This is DevOps Project involving building an automated workflow cum DevOps pipeline for the Coffee Project.

This repository is owned and maintained by the team:

```
------------------------------
|    Name     |   Unity ID   |
|:-----------:|:------------:|
| Tilak Satra |   trsatra    |
| Tejas Prabhu|   tprabhu2   |
| ----------- | ------------ |
```

## Problem Statement

**Tagline:** Automating Success, Infusing Efficiency, Brewing Reliability, One Commit at a Time: The DevOps Way

The challenge in the context of the DevOps domain for the Coffee Project lies in the need for availability, reliability, scalability, and efficient management of the application infrastructure. Although it initially appears to be a small-scale app with the simple functionality of ordering coffee and reviewing orders, the challenge emerges as usage grows both in terms of the users, adding more functionality, and availability of the service. With more features getting added to the project, the focus of the developers would be more towards shipping these features with utmost ease and zero issues. Getting involved in laborious and manual tasks of performing different sanity checks, ensuring correct tests are in place, and finally deploying it to the server/host/cloud could potentially make developers' day-to-day activities more involved and result in inefficient usage of developer's time on managing infrastructure and deployment rather than on feature development. Moreover, scaling the application, ensuring it remains available and responsive, and efficiently managing server resources becomes increasingly complex and labor-intensive.

### Why It Matters

These problems are significant because they affect both the end-users and the development and operations teams. End-users expect a seamless experience when ordering coffee, and downtime or performance issues can lead to a loss of customers. For the development and operations teams, manually managing the infrastructure to accommodate growing user demands is time-consuming, error-prone, and can lead to operational fatigue and burnout.

### Solution - DevOps Pipeline

An automated workflow, or the DevOps pipeline, automates various aspects of the Coffee App's infrastructure management. While it primarily operates in response to events like code commits to different branches or performing a production release, it mainly performs the task of checking linting errors, building the application, running the tests, and ensuring a healthy test coverage is maintained, backing up the existing working version of the application, deploying the app to the target environment, and performing health checks. Moreover, the operation of rolling back to the stable version in cases of application failure could also be performed through this pipeline. This pipeline not only eliminates the need for manual intervention but also ensures that the Coffee App is always available and responsive, delivering a seamless experience to end-users. It can also have interactions with user input for rolling back or running a specific image to ensure none of the target environments are down anytime ensuring high availability.

## Use Case

### Table of Contents

- [Preconditions](#preconditions)
- [Main Flow](#main-flow)
- [Alternative Flows](#alternative-flows)

---

### Preconditions

Before initiating the automated CI/CD pipeline, the following preconditions must be met:

- DEV VCL Host is provisioned.
- Self-Hosted GitHub Actions system is provisioned.
- Both feature and develop branches exist.
- Branch Protection Rules are applied on develop, main, and release branches.

---

### Main Flow

The main flow of this automated CI/CD pipeline use case is as follows:

1. A developer commits code to the feature branch, triggering a Linting Check for every commit.
2. After successful feature testing, the developer initiates the Continuous Integration (CI) pipeline by creating a Pull Request (PR) to the develop branch.
3. The PR includes necessary changes/improvements, a change message, and reviewers.
4. In the background, GitHub Actions invokes checks involving building the package, running tests (unit + integration tests), and ensuring the specified code coverage percentage is achieved.
5. The PR Reviewer approves the PR only when all checks pass.
6. Upon successful merge, GitHub Actions triggers the Continuous Deployment (CD) pipeline, which includes:
   - Installing Docker, Node, Kubernetes on the target host.
   - Building a Docker image and uploading it to the Docker Registry.
   - Invoking an Ansible Playbook to run the built image as a container on the target host.
   - Performing a health check.
7. If the Health Check is OK, the CI/CD pipeline concludes.

---

### Alternative Flows

This use case accounts for various alternative flows to handle issues or errors during the CI/CD pipeline:

- [E1] Linting Fails: Linting checks fail, indicating code quality issues.
- [E2] Tests Fail: Automated tests fail to pass, signaling potential issues or regressions.
- [E3] Docker Image Building Fails: Issues arise during Docker image building.
- [E4] Health Check – Not OK: The health check indicates a problem, leading to actions such as Rollback (manual trigger of pipeline with user input of specific image name & version).

---

This use case outlines the process of automated CI/CD pipeline execution triggered by a Pull Request to a develop branch. It ensures that code changes are thoroughly tested and deployed with reliability. The CI/CD pipeline encompasses a sequence of steps, as described in the main flow, and handles potential issues or errors through the alternative flows, with logs generated by GitHub Actions to facilitate debugging.

# Project Structure

# Project Structure Overview

This project is organized into several key directories, each serving a specific function in the application lifecycle, from Continuous Integration and Deployment to the NodeJS application codebase and Kubernetes configurations.

## Directory Structure

### Tree structure

```plaintext
.
├── .github
│   └── workflows
│       ├── cd-develop-main.yaml         # Handles CD for the develop/main branch
│       ├── cd-prod-promotion.yaml       # Manages Canary deployment promotions in prod
│       ├── cd-prod-rollback.yaml        # Facilitates rollbacks to stable versions
│       ├── cd-release.yaml              # Manages CD for the release branch
│       └── pipeline.yaml                # CI pipeline for linting, tests, and security
├── coffee_project                       # NodeJS application directory
│   ├── app.js                           # Main application file
│   ├── data.js                          # Data handling module
│   ├── Dockerfile                       # Docker container specification
│   ├── jest.config.js                   # Jest testing framework configuration
│   ├── package.json                     # NPM package and dependency declarations
│   ├── package-lock.json                # Auto-generated dependency tree
│   └── README.md                        # Project documentation and instructions
└── k8s                                  # Kubernetes deployment configurations
    ├── deployment-develop-main.yaml     # Staging/QA and dev environment deployment
    ├── deployment-release-canary.yaml   # Canary deployment for the release cluster
    ├── deployment-release-stable.yaml   # Stable release deployment
    ├── service-prod.yaml                # Production service with HTTPS support
    └── service.yaml                     # Load balancing service configuration
```

### Workflow Trigger Chart

```plaintext
Workflow File              | Trigger Event               | Branch                  | Actions
---------------------------|-----------------------------|-------------------------|-------------------------------------------------
pipeline.yaml              | Push, Pull Request          | All                     | - Linting checks
                           |                             |                         | - Test coverage
                           |                             |                         | - Vulnerability checks
---------------------------|-----------------------------|-------------------------|-------------------------------------------------
cd-develop-main.yaml       | Push                        | develop, main           | - Docker build and deploy to develop/main
                           |                             |                         | - AWS EKS staging/QA environment update
---------------------------|-----------------------------|-------------------------|-------------------------------------------------
cd-release.yaml            | Push                        | release                 | - Docker build and deploy to Docker Repo
                           |                             |                         | - AWS EKS production environment update
---------------------------|-----------------------------|-------------------------|-------------------------------------------------
cd-prod-rollback.yaml      | Push + Manual Dispatch      | -                       | - Revert to stable release in prod environment
---------------------------|-----------------------------|-------------------------|-------------------------------------------------
cd-prod-promotion.yaml     | Push + Manual Dispatch      | -                       | - Promote canary release in prod environment
                           |                             |                         |
---------------------------|-----------------------------|-------------------------|-------------------------------------------------
```

Additional Details:

Continuous Integration: pipeline.yaml is triggered on every push or pull request to any branch, ensuring code quality and security before any merge.

Continuous Deployment: cd-develop-main.yaml and cd-release.yaml are activated on pushes to their respective branches, deploying the latest version of the application automatically.

Manual Workflows: cd-prod-rollback.yaml and cd-prod-promotion.yaml require manual dispatch, providing controlled mechanisms for managing production releases.

## .github/workflows Folder

### pipeline.yaml

This file contains the code for Continuous Integration (CI). It defines branch action policies, linting checks, test coverage, and vulnerability checks. CI tasks are executed on a self-hosted GitHub Runner, which is a VCL Unix Host.

### cd-develop-main.yaml, cd-release.yaml

These files handle Continuous Deployment (CD). They involve installing Docker on a self-hosted runner, building and deploying the image to the Docker Repository within respective develop/main/release repo folders. Using GitHub action variables, these workflows identify branch-related metadata to deploy the application through AWS EKS.

### cd-prod-rollback.yaml, cd-prod-promotion.yaml

Responsible for additional functionalities like Rollback and Canary deployments. 'cd-prod-rollback.yaml' facilitates reverting canary release to a stable version, while 'cd-prod-promotion.yaml' enables canary release by implementing changes in one of the four pods.

## coffee_project Folder

This folder encompasses the entire NodeJS application.

## k8s Folder

The k8s directory hosts Kubernetes configurations essential for application deployment across different environments. It includes deployment-develop-main.yaml for staging and development setups, service.yaml for load balancing, deployment-release-canary.yaml for canary testing in production, and deployment-release-stable.yaml for stable releases. The service-prod.yaml facilitates secure HTTPS traffic in production with AWS-managed certificates. These files collectively ensure a seamless deployment pipeline from development to production.

## Pipeline Design

![DevOps Pipeline](https://github.ncsu.edu/trsatra/Devops_Project/blob/main/assets/devops.drawio.png)

# Continuous Integration and Deployment Pipeline

## Code Commit Stage

- **Tools**: Git, GitHub, Integrated Development Environments (IDEs)
- **Description**: Development begins on feature branches, branched off from the main development branch. Developers commit code changes after local validation. Each commit on a feature branch triggers the Continuous Integration (CI) process as defined in pipeline.yaml. This CI process includes automated tests and lint checks, ensuring that the new code adheres to quality standards and does not introduce regressions.

## Pull Request (PR) to Development Branch Stage

- **Tools**: GitHub Actions
- **Description**: When a feature is ready for integration, a PR is raised to merge the code into the development branch. This action triggers the CI pipeline which performs several checks including linting, dependency installation, execution of tests, and code coverage analysis. The PR requires at least one peer review for approval. Branch protection rules are in place, mandating successful CI checks and peer review approvals prior to merging. Direct deletions of the development branch are also prohibited to maintain integrity.

## Development Environment Build Stage

- **Tools**: GitHub Actions, Docker, Kubernetes, Amazon EKS
- **Description**: Post-merge into the development branch, the combined CI/CD pipeline kicks in. The pipeline configures Docker on the self-hosted runner, builds the Docker image from the code repository with a tag referencing the specific GitHub SHA, and pushes it to a public Docker repository dedicated for development builds. Subsequently, it installs and configures kubectl and the AWS CLI. Separate from the pipeline, EKS clusters are pre-configured using eksctl. The pipeline sets the context to the development cluster and deploys the latest Docker image and associated load balancing services, provisioning two replicas of the application for the development environment.

## Pull Request (PR) to Main Branch Stage

- **Tools**: GitHub Actions
- **Description**: Following extensive testing in the development environment, a PR is created to merge changes into the main branch. This PR triggers the CI pipeline, which mirrors the checks conducted during the development stage to ensure the code is ready for staging.

## Staging/Pre-Release Environment Build Stage

- **Tools**: GitHub Actions, Docker, Kubernetes, Amazon EKS
- **Description**: This stage mirrors the development environment build but with configurations tailored for the staging environment. This includes the use of dedicated image repositories and Kubernetes clusters, along with a specific load balancer setup tailored for staging.

## Pull Request (PR) to Release Branch Stage

- **Tools**: GitHub Actions
- **Description**: After the QA team completes testing in the staging environment, a PR is raised from the main to the release branch. This PR triggers the same CI pipeline that runs against PRs to the main branch, ensuring all changes are vetted before reaching production.

## Release Environment Build Stage

- **Tools**: GitHub Actions, Docker, Kubernetes, Amazon EKS
- **Description**: The release environment build stage starts with the same initial configuration and build process as the staging environment. However, it employs a distinct deployment strategy with canary releases. In this setup, the newest build handles a predefined percentage of the load, initially set at 25%, while the existing stable version manages the remaining 75%. The stable version tag is manually set in GitHub secrets, with future scope for automation. The trigger for this process is a new push to the release branch, which initiates three workflows: cd-develop-main.yaml for the usual deployment process, cd-prod-promotion.yaml, and cd-prod-rollback.yaml. The former proceeds with a canary deployment, while the latter two await gatekeeper approval. The goal is to gradually increase the canary's load-handling capacity, but within the project scope, it transitions directly from 25% to 100%. The gatekeeper's role is crucial, determining the stability of the canary release. They can promote the canary to the stable version by approving the promotion workflow and rejecting the rollback workflow, or vice versa if the canary is deemed unstable.

This CI/CD pipeline represents a robust, automated pathway from code commit to production deployment, incorporating rigorous testing, quality checks, and a structured approval process for managing deployments in a multi-environment architecture. The pipeline's design facilitates not only seamless integration and deployment but also provides mechanisms for safe and controlled updates to the production environment, minimizing risks associated with new releases.

## Security Measures

### Node Package Vulnerability Scanning

- **Phase**: Continuous Integration (CI)
- **Description**: In the Continuous Integration (CI) phase, the pipeline employs npm audit to scrutinize the project's Node.js packages for known vulnerabilities. This tool cross-references dependencies against the npm registry's database of security issues. Findings from the audit provide immediate feedback on potential vulnerabilities, allowing developers to address issues before merging code into the main branch.

### Docker Image Security Scanning

- **Phase**: Continuous Deployment (CD)
- **Description**: During the Continuous Deployment (CD) process, the pipeline leverages the Trivy tool to perform a thorough vulnerability scan of the Docker images. Trivy is an open-source security scanner that detects vulnerabilities within container images, file systems, and even configuration issues, offering a broad security assessment. The results from Trivy scans are then captured and preserved as artifacts within the GitHub Actions workflow. This ensures that any security concerns are documented and can be reviewed as part of the build history.

## Steps to create EKS clusters

```bash
eksctl create cluster --name devops-release --region us-east-1 --nodegroup-name release-nodes --node-type t2.micro --nodes 4 --zones us-east-1a,us-east-1b

eksctl create cluster --name devops-main --region us-east-1 --nodegroup-name main-nodes --node-type t2.micro --nodes 3 --zones us-east-1a,us-east-1b

eksctl create cluster --name devops-develop --region us-east-1 --nodegroup-name develop-nodes --node-type t2.micro --nodes 3 --zones us-east-1a,us-east-1b
```
