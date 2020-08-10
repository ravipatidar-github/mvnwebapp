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
        stage('build & sonarqube analysis') {
              steps {
                  withSonarQubeEnv('sonarqube')
                  bat 'mvn clean install sonar: sonar'
                  sonar-scanner.bat -D
                  "sonar.projectKey=SONAR" -D
                  "sonar.sources=." -D
                  "sonar.host.url=http://localhost:9000" -D
                  "sonar.login=789d74bfdefdee292295fb4f9dc992f218de9ec6"
              }
         }
        
        stage ('upload war to nexus') {
            steps{
                nexusArtifactUploader artifacts: [
              [artifactId: 'mvnwebapp',
              classifier: '',
              file: 'target/mvnwebapp.war',
              type: 'war']
                ], 
              credentialsId: 'Nexus',
              groupId: 'jenkins.mvn.demo',
              nexusUrl: 'localhost:8081',
              nexusVersion: 'nexus3', 
              protocol: 'http',
              repository: 'SAMPLE-REL',
              version: '1.0.0'
            
            }
            
        }
    }
}
