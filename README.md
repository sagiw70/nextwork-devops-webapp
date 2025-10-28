# Hands-On AWS CI/CD Project 

I built this project to apply my AWS knowledge in a hands-on way after completing the AWS Solutions Architect Associate certification.
It features a complete CI/CD pipeline from GitHub to a live EC2 instance, using services like CodePipeline, CodeBuild, CodeDeploy, and CodeArtifact - all deployed on AWS.

The idea was inspired by the Nextwork 7-Day DevOps Challenge, which provided a solid starting point. I expanded on it to gain practical experience with real-world deployment issues and AWS service integrations.


---

## Objectives

- Automate the build and deployment process of a Java web application.
- Set up continuous integration (CI) and continuous deployment (CD) using GitHub as the source.
- Deploy the application to a live EC2 instance.

---

## Tools and Services Used

- **GitHub** - Source control.
- **AWS CodePipeline** - Orchestrates the CI/CD flow.
- **AWS CodeBuild** - Compiles the Maven project and builds the `.war` file.
- **AWS CodeDeploy** - Deploys the `.war` file to EC2.
- **AWS CodeArtifact** - Stores dependencies for the Maven build.
- **Amazon EC2** - Hosts the live web application.
- **Elastic IP** - Ensures stable access to the EC2 instance.

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

- **Elastic IP setup**: Without it, I couldn't reliably connect VS Code to the EC2 instance due to the public IP changing after restarts.  
- **Manual CodeArtifact configuration**: The setup skipped key steps, so I manually created the domain and repository and added missing permissions like `sts:GetServiceBearerToken` to the CodeBuild role.  
- **CodeDeploy agent troubleshooting**: Required SSH access to the EC2 instance, checking agent status and reading logs under `/opt/codedeploy-agent/deployment-root/deployment-logs` to debug silent deployment failures.  
- **IAM role misconfigurations**: Fixed missing permissions such as `codedeploy:GetApplicationRevision` and attached the correct IAM instance profile to the EC2 server.  
- **Deployment group filtering issues**: Solved by assigning the correct EC2 tag (e.g., `Name: NextWorkCodeDeployEC2Stack::WebServer`) to match the deployment group.  
- **SSH access issues**: Resolved by editing the EC2 security group to allow inbound traffic on port 22 and meeting EC2 Instance Connect prerequisites.  
- **Accidental nested Git repo**: Removed the embedded repository and added it to `.gitignore` to clean up the project structure.  

