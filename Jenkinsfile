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
                // 'assemble' ensures the JAR file is created for archiving
                sh './gradlew clean test jacocoTestReport assemble'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // This name must match Jenkins -> Manage Jenkins -> System -> SonarQube installations
                withSonarQubeEnv('My Sonar Server') {
                    sh './gradlew sonar'
                }
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }
}
