pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.yml'
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from version control
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-riyaantariq'
            }
        }

        stage('Build Docker Images') {
            steps {
                // Build Docker images
                bat 'docker build -t myimage .'
            }
        }

        stage('Run Docker Containers') {
            steps {
                // Run Docker containers
                bat 'docker run -d --name mycontainer myimage'
            }
        }

        stage('Run Tests') {
            steps {
                // Run your tests here
                // For example, you can run unit tests within your containers
            }
        }

        stage('Deploy') {
            steps {
                // You can add your deployment steps here
                // For example, pushing images to a Docker registry
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
