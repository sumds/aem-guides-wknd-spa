pipeline{
    tools{
        maven_home 'maven-3.9.3'
    }
    options {
        timestamps()
    }
    triggers{
    }

    stages{
        stage("Checkout from git"){
            steps{
                git credentialsId: 'sumds', url: 'https://github.com/sumds/aem-guides-wknd-spa.git'
            }
        }
        stage("Build source code"){
            steps{
                sh "${maven_home}/bin/mvn clean package"
            }
        }
        stage("Execute sonarqube report"){
            steps{
                sh "${maven_home}/bin/mvn sonar:sonar"
            }
        }
        stage("Upload Artifact To Nexus"){
            sh "${maven_home}/bin/mvn deploy"
        }
    }
}