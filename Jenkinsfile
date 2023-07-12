node{
    def maven_home = tool name:"maven-3.9.3"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([githubPush()])])
    
    stage("Checkout from git"){
        git credentialsId: 'sumds', url: 'https://github.com/sumds/aem-guides-wknd-spa.git'
    }
    stage('Build source code'){
        sh "${maven_home}/bin/mvn clean package"
    }
    stage('ExecuteSonarCubeReport'){
        sh "${maven_home}/bin/mvn sonar:sonar"
    }
    stage('UploadArtifactToNexus'){
        sh "${maven_home}/bin/mvn deploy"
    }
}