# Continuous Development Project
![DevelopmentEnvironemntSetupProject!](https://lucid.app/publicSegments/view/db5a3c68-addf-4aa5-a15f-464c7bc00d66/image.png)

###### Project ToolBox 🧰
- [Git](https://git-scm.com/) Git will be used to manage our application source code.
- [Github](https://github.com/) Github is a free and open source distributed VCS designed to handle everything from small to very large projects with speed and efficiency
- [Maven](https://maven.apache.org/) Maven will be used for the application packaging and building including running unit test cases
- [SonarQube](https://docs.sonarqube.org/) SonarQube Catches bugs and vulnerabilities in your app, with thousands of automated Static Code Analysis rules.
- [Nexus](https://www.sonatype.com/) Nexus Manage Binaries and build artifacts across your software supply chain
- [EC2](https://aws.amazon.com/ec2/) EC2 allows users to rent virtual computers (EC2) to run their own workloads and applications.

## Configure Environments
1) Create a GitHub Repository
    - Navigate to https://github.com
    - Click on Repositories
    - Click on `Create` to Create a Repository
     - Repository Name: `jenkins-maven-sonarqube-nexus-project`
     - Click on `Create`
     - Download the Project Zip from https://github.com/UtamaDalington/Jenkins-Maven-Sonarqube-Nexus-Project
     - Unzip and Push the code to the Repository you just provisioned

2) SonarQube
    - Create an Ubuntu 24.04 VM instance and call it "SonarQube"
    - Instance type: c7i-flex.large (2 vCPU and 4 GiB Memory)
    - Security Group (Open): 9000 and 22 to 0.0.0.0/0 or Your-IP
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/UtamaDalington/Maven-SonarQube-Nexus-Jenkins-installations/blob/main/sonarqube-install.sh
    - Launch Instance

3) Nexus
    - Create an Ubuntu 24.04 VM instance and call it "Nexus"
    - Instance type: m7i-flex.large (2 vCPU and 8 GiB Memory)
    - Security Group (Open): 8081 and 22 to 0.0.0.0/0 or Your-IP
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/UtamaDalington/Maven-SonarQube-Nexus-Jenkins-installations/blob/main/nexus-install-t2large.sh
    - Launch Instance

4) Jenkins/Maven
    - Create an Amazon Linux 2 VM instance and call it "Jenkins-Maven"
    - Instance type: `t2.medium`
    - Security Group (Open): 8080 and 22 to 0.0.0.0/0 or Your-IP
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-sonarqube-nexus-jenkins-install/jenkins-install.sh
    - Launch Instance

## Configure Nexus Repository
Series of tutorial code snippets for use
#Maven publish tutorial steps
#Publishing artifact to Nexus snapshot and release repo using maven.
