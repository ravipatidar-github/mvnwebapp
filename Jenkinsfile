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
        
        
        stage('sonarqube analysis') {
            steps {
                script {
                    def scannerHome = tool 'SONAR_RUNNER_HOME';
                    
                    withSonarQubeEnv(credentialsId: 'NewProject') {
                        bat "${tool("SONAR_RUNNER_HOME")}/bin/sonar-scanner.bat" -D
                  "sonar.projectKey=NewProject" -D
                  "sonar.sources=." -D
                  "sonar.host.url=http://localhost:9000" -D
                  "sonar.login=19feec3fed72328451b0f0623e61c639fe12c458"
                    }
                }
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
