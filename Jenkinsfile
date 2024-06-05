pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = '777e72f2-96a7-4ea6-8c10-32401a1b398d'
        DOCKER_COMPOSE_FILE = 'docker-compose.yaml'
        IMAGE_TAG = "latest"
    }

    stages {
        stage('21i-1101 Checkout') {
            steps {
                // Checkout code from version control
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-riyaantariq'
            }
        }

        stage('21i-1101 Build Docker Images') {
            steps {
                // Build each Docker image separately
                script {
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_REGISTRY_CREDENTIALS, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        bat 'docker build -t auth ./Auth'
                        bat 'docker build -t classrooms ./Classrooms'
                        bat 'docker build -t post ./Post'
                        bat 'docker build -t client ./client'
                    }
                }
            }
        }

        stage('21i-1101 Run Services') {
            steps {
                // Start Docker Compose services
                bat 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            // Ensure that the Docker Compose services are brought down
            bat 'docker-compose down'
        }
    }
}
