pipeline {
  agent any // This specifies that the pipeline can run on any available agent
  stages {
    stage('Validate Project') {
        steps {
            sh 'mvn validate'
        }
    }
    stage('Unit Test'){
        steps {
            sh 'mvn test'
        }
    }
    stage('App Packaging | Build'){
        steps {
            sh 'mvn package'
        }
    }
    stage('Integration Test'){
        steps {
            sh 'mvn verify -DskipUnitTests'
        }
    }
    stage ('Checkstyle Code Analysis'){
        steps {
            sh 'mvn checkstyle:checkstyle'
        }
    }
    stage('SonarQube Inspection') {
        steps {
            sh  """mvn sonar:sonar \
                    -Dsonar.projectKey=ecommerce-java-webapp \
                    -Dsonar.host.url=http://75.101.251.162:9000 \
                    -Dsonar.login=e5f2bd65a07c94dbf113b610d258b964a7d7e7b4"""
        }
    } 
    stage("Upload Artifact To Nexus"){
        steps{
             sh 'mvn deploy'
        } 
        post {
            success {
              echo 'Successfully Uploaded Artifact to Nexus Artifactory'
        }
      }
    }
  }
}