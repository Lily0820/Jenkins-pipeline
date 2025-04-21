pipeline {
    agent any
    tools {
        gradle 'Gradle-8.6'  // Name of Gradle tool configured in Jenkins
        jdk 'OpenJDK-11'  // Name of JDK tool configured in Jenkins
    }
    environment {
        ARTIFACTORY_URL = "http://localhost:8081/artifactory/libs-release-local"
        ARTIFACTORY_CREDENTIALS = "admin:password"  // Update as needed
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'develop', url: 'https://github.com/your-repo/microservices.git'
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
