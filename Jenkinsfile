pipeline {
    agent any
    stages {
        stage('---clean---') {
            steps {
                bat "mvn clean"
            }
        }
        stage('--test--') {
            steps {
                bat "mvn test"
            }
        }
        stage('--package--') {
            steps {
                bat "mvn package"
            }
        }
        
        stage ('upload war to nexus') {
            steps{
                nexusArtifactUploader artifacts: [
              [artifactId: 'mvnwebapp',
              classifier: '',
              file: 'target/mvnwebapp-0.0.1-SNAPSHOT.war',
              type: 'war']
                ], 
              credentialsId: 'Nexus',
              groupId: 'jenkins.mvn.demo',
              nexusUrl: 'localhost:8081',
              nexusVersion: 'nexus3', 
              protocol: 'http',
              repository: 'SAMPLE-REL',
              version: '0.0.1-SNAPSHOT'
            
            }
            
        }
    }
}
