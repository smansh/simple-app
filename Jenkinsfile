pipeline {
    agent any
    tools {
        maven 'Maven_home'
    }
    
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload War To Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [
                      [
                        artifactId: 'simple-app',
                        classifier: '', 
                        file: 'target/simple-app-1.0.0.war', 
                        type: 'war'
                      ]
                 ], 
                 credentialsId: 'nexus3', 
                 groupId: 'in.javahome', 
                 nexusUrl: '192.168.43.186:8081', 
                 nexusVersion: 'nexus3', 
                 protocol: 'http', repository: 'smansh-app-release', 
                 version: '1.0.0'
                   
             }
   }
    }
}
