pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = 'ecommerce-app'
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Rajathshetty09/ecommerce-microservices.git'
            }
        }

        stage('Build & Spin Up Containers') {
            steps {
                // Remove existing project containers and any orphans blocking container names
                sh 'docker compose --project-name ${COMPOSE_PROJECT_NAME} down --remove-orphans || true'
                
                // Spin up all microservices and infra containers cleanly
                sh 'docker compose --project-name ${COMPOSE_PROJECT_NAME} up -d --build'
            }
        }
    }

    post {
        always {
            sh 'docker image prune -f'
        }
    }
}
