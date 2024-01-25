# Status Report 2

## Team Accomplishments

### Tilak Satra | Unity_Id: trsatra

- Accomplishment 1: integrated code coverage

  - Description:
    Successfully integrated code coverage tools into our CI pipeline, enhancing the accuracy and effectiveness of our testing strategy. This integration provides valuable insights into the test coverage of our codebase, ensuring we maintain high-quality standards and address any potential gaps in our tests.
  - Link:
    - https://github.ncsu.edu/trsatra/Devops_Project/commit/70a61c8e910cf67aa78596efabfe2b8b0365fb00

### Tejas Prabhu | Unity_Id: tprabhu2

After sucessfully deploying the app in a single container environment, we are now focusing on scaling our solution to multiple containers using kubernetes. On top of that, we are working on using canary deployment strategy to flawlessly deploy the app without much interuption.

- Accomplishment 1: Kubernetes installation and setup on the nodes

  - Description: Successfully developed an Ansible playbook for the installation and setup of Kubernetes on development environment nodes. This playbook includes the necessary configuration for Docker and Istio, laying the groundwork for a scalable and robust development infrastructure. The current focus is on optimizing the setup for the development environment. Future plans include extending and adapting these efforts to our OA (Operational Acceptance Testing) and production environments, ensuring a consistent and reliable deployment process across all stages.

  - Links:
    - https://github.ncsu.edu/trsatra/Devops_Project/commit/b0c60f9d7ca358ec0585eacc310dc3a02a552b29
    - https://github.ncsu.edu/trsatra/Devops_Project/commit/e98c6c1870882f7bdacb0b82cc04f82e43150df5
    - https://github.ncsu.edu/trsatra/Devops_Project/commit/1fee643280f64420335930983a4ce0442620c3f9

- Accomplishment 2: Implementation of Canary Deployment Kubernetes Manifests Using Istio
  - Description: Crafted Kubernetes manifests to facilitate canary deployments. This encompasses deployment configurations for both canary and stable versions, along with the requisite service files and Istio configuration for traffic management. This implementation is pivotal in enabling us to conduct phased rollouts and A/B testing, significantly reducing the risk associated with deploying new versions and ensuring seamless user experiences.
  - Links:
    - https://github.ncsu.edu/trsatra/Devops_Project/commit/ba79a5f09eee9ab907a4c39b505d5ab5abf836b3
    - https://github.ncsu.edu/trsatra/Devops_Project/commit/de9ac57a190aa9d7d4d703c0db874e9567b8b824

## Next Steps

### Tilak Satra

- Goal 1: Implement security practices
  - Dependency-Check to identify vulnerabilities in third-party libraries, along with Container Scanning to assess Docker images for security flaws. We also plan to implement robust Secrets Management to ensure sensitive data is securely handled, and Static Application Security Testing (SAST) to proactively identify potential vulnerabilities in our source code.
  - Implementation Plan:
    - Step 1: Select and integrate Dependency-Check for dependency scanning and a container scanning tool for Docker images. Ensure these tools are configured to automatically scan during each CI build.
  - Estimated Effort: One week
- Goal 2: Fine-Tune CI/CD Pipeline Integration
  - Focusing on refining the integration of our Continuous Integration (CI) and Continuous Deployment (CD) pipelines. This enhancement aims to ensure seamless transitions between code integration and deployment stages, optimizing the overall development process for efficiency and reliability.
  - Implementation Plan:
    - Step 1: Create scripts or tasks to connect CI and CD pipelines, ensuring smooth transitions between code integration and deployment stages.
    - Step 2: Test the integrated pipeline, focusing on optimization for efficiency, and make necessary adjustments based on the test results.
  - Estimated Effort: Once both pipelines are finalised, it should take 2-3 days to integrate them and do integrated tests.

### Tejas Prabhu

- Goal 1: Kubernetes Integration in Continuous Deployment Pipeline

  - The current state of our project sees Kubernetes setup files and deployment manifests as standalone components. The immediate goal is to integrate these crucial elements directly into our main Continuous Deployment (CD) pipeline. This integration will centralize and streamline our deployment process, ensuring that Kubernetes configurations are consistently updated and in sync with each deployment.
  - Implementation Plan:
    - Step 1: Finalize and stabilize Kubernetes setup files and deployment manifests, ensuring they meet the project's operational requirements.
    - Step 2: Develop scripts or automation tasks that seamlessly integrate these Kubernetes elements into the existing CD pipeline.
    - Step 3: Conduct thorough testing of the integrated pipeline in a controlled environment to ensure stability and reliability before full-scale implementation.
  - Estimated Effort: Standalone kubernetes setup using ansible is almost working. Integrating it with deployment pipeline should take 2 days and futher integrated testing should take 2 more days.

- Goal 2: Creation of a Manual Gatekeeping Pipeline for Stable Version Releases
  - Establish a new pipeline process that allows for manual approval and promotion of canary versions to stable releases. This pipeline will serve as a critical control point, ensuring that only thoroughly tested and vetted versions of the application are marked as stable and deployed to production.
  - Implementation Plan:
    - Step 1: Implement a gatekeeping mechanism where a responsible team member can review test results and manually approve the promotion of a canary version to a stable release.
    - Step 2: Integrate this pipeline with existing deployment processes, ensuring that it works in harmony with automated deployments and does not introduce bottlenecks.
  - Estimated Effort: Preliminary idea of the github action file required is clear. Implementing it and testing independently should take 2 days. Integrating it with main pipeline and integrated testing might take one day.

## Sprint Retrospective

### What Worked

- **Learning from Previous Retrospective:** We successfully leveraged insights from our previous retrospective, focusing more on teamwork and early engagement.
- **Integration of Code Coverage:** Successfully integrated code coverage tools, enhancing the quality and reliability of our codebase.
- **Designing a Canary Deployment Pipeline:** Implemented a pipeline to incorporate canary deployment with manual gatekeeping, optimizing our release process.
- **Adherence to Best Practices:** Followed best practices for secret management and deployment, ensuring a secure and efficient workflow.

### What Didn't Work

- **Challenges with Kubernetes Setup:** The transition from using kubernetes in Minikube like environment to a production-grade Kubernetes environment was more complex than anticipated. Despite the steep learning curve and the significant time and effort investment, we view these as valuable learning experiences and not merely setbacks.

### What We'll Do Differently

- **Targeted Time Management:** To address the challenges faced with Kubernetes setup, we plan to allocate specific time blocks for research and collaborative problem-solving sessions, ensuring a more targeted and effective use of our time.
- **Leveraging Existing Tools and Resources:** We realized the importance of utilizing existing tools like Kubespray, which could have streamlined our Kubernetes setup process. Going forward, we will prioritize the use of such resources to avoid reinventing the wheel and to save valuable development time.
