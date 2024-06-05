pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.yaml'
        IMAGE_TAG = "latest"
    }

    stages {
        stage('1101 Checkout') {
            steps {
                // Checkout code from version control
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-riyaantariq'
            }
        }

        stage('1101 Build Docker Images') {
            steps {
                // Build Docker images
                bat 'docker build -t myimage .'
            }
        }

        stage('1101 Run Docker Containers') {
            steps {
                // Run Docker containers
                bat 'docker run -d --name mycontainer myimage'
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
