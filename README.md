# Continuous Development Environment
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
    - Create an Ubuntu 24.04 VM instance and call it "Jenkins-Maven"
    - Instance type: c7i-flex.large (2 vCPU and 4 GiB Memory)
    - Security Group (Open): 8080 and 22 to 0.0.0.0/0 or Your-IP
    - Key pair: Select or create a new keypair
    - User data (Copy the following user data): https://github.com/UtamaDalington/Maven-SonarQube-Nexus-Jenkins-installations/blob/main/install-jenkins1.sh
    - Launch Instance

### Project Preparation (Jenkins/Maven)
- Verify the Maven installation and version
    ```
    mvn -v
    ```

- Verify the Java installation and version
    ```
    java -version
    ```

- This Project requires Java 11 installed, so install and switch to Java 11, if otherwise.
    ```
    sudo apt-get install -y openjdk-11-jdk
    sudo update-alternatives --config java
    ```
            
- Create the `.m2` directory in the home directory of your current user that will orchestrate the build (jenkins)
    ```
    sudo mkdir .m2/
    ```

- Create the Settings file inside of the `~/.m2` directory
    ```
    cd ~/.m2/
    sudo wget (copy and paste the [raw file link](https://raw.githubusercontent.com/UtamaDalington/Jenkins-Maven-Sonarqube-Nexus-Project/refs/heads/main/settings.xml) of the `settings.xml` file from GitHub Repository to download the file and it's content into `.m2`)
    ```

- Ensure to change ownership of both `.m2` and `settings.xml` from root to jenkins
    ```
    sudo chown jenkins:jenkins .m2/
    sudo chown jenkins:jenkins settings.xml
    ```
