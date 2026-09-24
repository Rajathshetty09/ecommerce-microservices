pipeline {
    agent any

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Rajathshetty09/ecommerce-microservices.git'
            }
        }

        stage('Build & Spin Up Containers') {
            steps {
                // Stop existing running containers if any
                sh 'docker compose down || true'
                
                // Build and start all microservice containers directly
                sh 'docker compose up -d --build'
            }
        }
    }

    post {
        always {
            // Clean up unused images to save disk space
            sh 'docker image prune -f'
        }
    }
}
