pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                sh './gradlew clean test jacocoTestReport assemble'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // We call sonar directly without the 'withSonarQubeEnv' wrapper
                sh './gradlew sonar'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
