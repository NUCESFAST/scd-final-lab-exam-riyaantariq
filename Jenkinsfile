pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.yaml'
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
                script {
                    // Build Docker images
                    sh 'docker build -t myimage .'
                }
            }
        }

        stage('Run Docker Containers') {
            steps {
                script {
                    // Run Docker containers
                    sh 'docker run -d --name mycontainer myimage'
                }
            }
        }

       
    }

    post {
        always {
            script {
                // Ensure that the Docker Compose services are brought down
                sh 'docker-compose down'
            }
        }
    }
}
