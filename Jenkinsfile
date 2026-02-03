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
                // This runs your verified gradle commands
                sh './gradlew clean test jacocoTestReport'
            }
        }
        stage('Archive Artifact') {
            steps {
                // This saves the JAR file so you can download it from the UI
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
