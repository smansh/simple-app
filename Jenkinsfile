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
                script{

                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT")" : "smansh-app-release"
                    
                 nexusArtifactUploader artifacts: [
                      [
                        artifactId: 'simple-app',
                        classifier: '', 
                        file: "target/simple-app-${mavenPom.version}.war", 
                        type: 'war'
                      ]
                 ], 
                 credentialsId: 'nexus3', 
                 groupId: 'in.javahome', 
                 nexusUrl: '192.168.43.186:8081', 
                 nexusVersion: 'nexus3', 
                 protocol: 'http', 
                 repository: '${nexusRepoName}', 
                 version: '${mavenPom.version}'
                   
             }
   }
    }
}
}
