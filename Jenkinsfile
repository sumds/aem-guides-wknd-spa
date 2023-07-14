pipeline{
    agent any

    tools{
        maven 'maven-3.9.3'
    }
    options {
        timestamps()
    }

    parameters {
        choice choices: ['master', 'develop', 'feature', 'qa'], name: 'branchName'
        string defaultValue: 'https://github.com/sumds/aem-guides-wknd-spa.git', name: 'giturl'
    }

    stages{
        stage("Checkout from git"){
            steps{
                git branch: "${params.branchName}",credentialsId: 'sumds', url: "${params.giturl}"
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