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
        
        // stage("Build source code"){
        //     steps{
        //         sh "mvn clean package"
        //     }
        // }

        // stage("Execute sonarqube report"){
        //     steps{
        //         sh "mvn sonar:sonar"
        //     }
        // }

        stage("Upload Artifact To Nexus"){
            steps{
                //sh "mvn deploy"
                sh "mvn deploy:deploy-file -DgroupId=com.adobe.aem.guides.wkndspa.react -DartifactId=aem-guides-wknd-spa.react -Dversion=1.0.0-SNAPSHOT -DgeneratePom=true -Dpackaging=zip -DrepositoryId=nexus -Durl=http://3.92.61.217:8081/repository/wknd-spa-snapshot -Dfile=/var/lib/jenkins/workspace/aem-pipeline-code/all/target/aem-guides-wknd-spa.react.all-1.0.0-SNAPSHOT.zip"
                sh "mvn deploy:deploy-file -DgroupId=com.adobe.aem.guides.wkndspa.react -DartifactId=aem-guides-wknd-spa.react -Dversion=1.0.0-SNAPSHOT -DgeneratePom=true -Dpackaging=zip -DrepositoryId=nexus -Durl=http://3.92.61.217:8081/repository/wknd-spa-snapshot -Dfile=/var/lib/jenkins/workspace/aem-pipeline-code/ui.apps/target/aem-guides-wknd-spa.react.ui.apps-1.0.0-SNAPSHOT.zip"
                sh "mvn deploy:deploy-file -DgroupId=com.adobe.aem.guides.wkndspa.react -DartifactId=aem-guides-wknd-spa.react -Dversion=1.0.0-SNAPSHOT -DgeneratePom=true -Dpackaging=zip -DrepositoryId=nexus -Durl=http://3.92.61.217:8081/repository/wknd-spa-snapshot -Dfile=/var/lib/jenkins/workspace/aem-pipeline-code/ui.config/target/aem-guides-wknd-spa.react.ui.config-1.0.0-SNAPSHOT.zip"
                sh "mvn deploy:deploy-file -DgroupId=com.adobe.aem.guides.wkndspa.react -DartifactId=aem-guides-wknd-spa.react -Dversion=1.0.0-SNAPSHOT -DgeneratePom=true -Dpackaging=zip -DrepositoryId=nexus -Durl=http://3.92.61.217:8081/repository/wknd-spa-snapshot -Dfile=/var/lib/jenkins/workspace/aem-pipeline-code/ui.content/target/aem-guides-wknd-spa.react.ui.content-1.0.0-SNAPSHOT.zip"
            }
        }
    }
}