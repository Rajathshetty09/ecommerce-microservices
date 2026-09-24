pipeline {
    agent any

    environment {
        PROJECT_DIR = '.'
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Rajathshetty09/ecommerce-microservices.git'
            }
        }

        stage('Build Java Artifacts') {
            steps {
                sh 'chmod +x mvnw && ./mvnw clean package -DskipTests'
            }
        }

        stage('Build & Spin Up Containers') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose build'
                sh 'docker compose up -d'
            }
        }
    }

    post {
        always {
            sh 'docker image prune -f'
        }
    }
}
