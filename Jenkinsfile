pipeline {
    agent any
    tools {
        gradle 'Gradle-8.6'     // Match this with what you've set up in Jenkins Global Tools
        jdk 'jdk17'
    }
    environment {
        ARTIFACTORY_URL = "http://localhost:8081/artifactory/libs-release-local"
        ARTIFACTORY_CREDENTIALS = "admin:password"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Lily0820/Jenkins-pipeline.git'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew clean build'
            }
        }
        stage('Publish Artifacts to Artifactory') {
            steps {
                sh './gradlew publish'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
