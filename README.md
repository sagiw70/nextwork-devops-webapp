# Nextwork DevOps CI/CD Project

This project showcases a full CI/CD pipeline built on AWS using CodePipeline, CodeBuild, CodeDeploy, CodeArtifact, EC2 and GitHub. The goal was to automate the deployment of a Java web application (.war) with minimal manual intervention.

This project was created as a hands-on follow-up to my AWS Solutions Architect Associate certification to solidify concepts through practice.

---

## Objectives

- Automate the build and deployment process of a Java web application.
- Set up continuous integration (CI) and continuous deployment (CD) using GitHub as the source.
- Deploy the application to a live EC2 instance.

---

## Tools and Services Used

- **GitHub** – Source control.
- **AWS CodePipeline** – Orchestrates the CI/CD flow.
- **AWS CodeBuild** – Compiles the Maven project and builds the `.war` file.
- **AWS CodeDeploy** – Deploys the `.war` file to EC2.
- **AWS CodeArtifact** – Stores dependencies for the Maven build.
- **Amazon EC2** – Hosts the live web application.
- **Elastic IP** – Ensures stable access to the EC2 instance.

---

## Architecture Overview

The following components were connected:

- Source (GitHub) triggers CodePipeline.
- CodePipeline passes artifacts to CodeBuild.
- CodeBuild uses CodeArtifact for dependencies and outputs a `.war` file.
- CodeDeploy deploys to an EC2 instance (Tomcat server).
- Elastic IP used to avoid issues with changing public IPs.

---

## Challenges Encountered

- **Elastic IP setup**: Without it, I couldn't reliably connect VS Code to the instance.
- **Manual CodeArtifact configuration**: Had to manually create a domain and repository, and fix missing permissions for CodeBuild's IAM role.
- **CodeDeploy agent**: Required checking logs inside the EC2 instance when deployment failed without a clear error.
- **IAM roles**: Troubleshooting permissions between CodePipeline and CodeDeploy.
- **Lifecycle event errors**: Resolved by attaching the correct IAM instance profile and security group.
- **Index.jsp not updating**: Solved by checking if the correct EC2 instance was in use and ensuring `.war` override.
- **Accidental nested Git repo**: Cleaned up with `.gitignore`.



