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
              }
         }
    }
}
