pipeline{
    agent any

    tools{
        maven 'maven-3.9.3'
    }
    options {
        timestamps()
    }
    triggers {
        githubPush()
    }

    stages{
        stage("Checkout from git"){
            steps{
                git credentialsId: 'sumds', url: 'https://github.com/sumds/aem-guides-wknd-spa.git'
            }
        }
        stage("Build source code"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("Execute sonarqube report"){
            steps{
                sh "mvn sonar:sonar"
            }
        }
        stage("Upload Artifact To Nexus"){
            steps{
                sh "mvn deploy"
            }
        }
    }
}