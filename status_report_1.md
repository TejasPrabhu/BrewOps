# Status Report 1

## Team Accomplishments

### Tilak Satra | Unity_Id: trsatra

- Accomplishment 1: Branch Protection Rule Enabled
  - Description: Main, Develop, Release Branches are protected from direct push, require PR(s) and approval
  - Link: https://github.ncsu.edu/trsatra/Devops_Project/settings/branches
- Accomplishment 2: Continuous Integration Enabled
  - Description: CI Pipeline enabling successful compilation, linting and test case execution
  - Link: https://github.ncsu.edu/trsatra/Devops_Project/commit/646af64fba32302e77200083812daab290bc2d0d#diff-a9fcf81f55b16d4db9d62258b46a56b196b1e20741c9f5fc61728a3578064b98

### Tejas Prabhu | Unity_Id: tprabhu2

- Accomplishment 1: Continuous Delivery Enabled through github actions

  - Description: This achievement encompasses the development of a Dockerfile and the automation of Docker image building and pushing processes to the Docker Hub registry.
  - Link: https://github.ncsu.edu/trsatra/Devops_Project/commit/42c469fa52ec8876b4c44f5005fdee28e8cca882

- Accomplishment 2: Continuous Deployment Enabled through ansible playbook
  - Description: This accomplishment highlights the deployment of an automated process using Ansible Playbook for the configuration and setup of the development environment. It includes the deployment of the Docker container on the environment
  - Link: https://github.ncsu.edu/trsatra/Devops_Project/commit/6a631e0cf864a2cbf7e193abf5e2fe5b79ce9db6

## Next Steps

### Tilak Satra

- Goal 1: Integrate Code Coverage to the CI Pipeline
  - Since the basic template for CI pipeline is ready and executes fine, the next step in to integrate code coverage ensuring code changes are well tested and meet the set coverage requirement.
- Goal 2: Implement Manual Pipeline Trigger and Rollback Mechanism
  - Since the basic CI/CD pipeline is ready, we need support the option to trigger pipeline manually in cases of different failure reasons and revert the deployment to stable version(s).

### Tejas Prabhu

- Goal 1: Setting Up NGINX as Reverse Proxy
  - We need to deploy NGINX to work as a reverse proxy rather than exposing the docker container directly for security reasons.
- Goal 2: Enable Canary Deployment(s)
  - We need to implement canary deployment strategy in Kubernetes, directing a portion of traffic to the new version and scaling based on success metrics.

## Sprint Retrospective

### What Worked

- Fair Task Distribution and Ownership was at full display
- Git Commit standard were followed
- Feature code building; which then propogated to Dev and subsequently Main through PR(s) invoking our CI/CD pipeline ensured correctness of our approach and development.

### What Didn't Work

- Instead of focusing on individual task and resolving errors individually resulting in a lot of time investment, Paired Programming could be inculcated.

### What We'll Do Differently

- Incorporate Paired Programming:

  - Plan to incorporate paired programming sessions to enhance collaboration, problem-solving, and reduce time spent on individual task resolution.

- Streamline Error Resolution:

  - Implement a more efficient approach to resolving errors, potentially through collaborative efforts.

- Optimize Time Management:
  - Explore strategies to optimize time management during development, ensuring a balance between individual work and collaborative efforts.
