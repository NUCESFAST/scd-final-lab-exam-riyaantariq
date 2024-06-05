pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.yaml'
        IMAGE_TAG = "latest"
    }

    parameters {
        credentials(name: 'DOCKER_HUB_CREDENTIALS', description: 'Docker Hub credentials', credentialType: 'UsernamePassword')
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
                    withCredentials([usernamePassword(credentialsId: 'DOCKER_HUB_CREDENTIALS', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASSWORD')]) {
                        bat "docker login -u $DOCKER_USER -p $DOCKER_PASSWORD"
                        bat "docker build -t myimage ."
                    }
                }
            }
        }

        stage('Run Docker Containers') {
            steps {
                script {
                    // Run Docker containers
                    bat 'docker run -d --name mycontainer myimage'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run your tests here
                    // For example, you can run unit tests within your containers
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // You can add your deployment steps here
                    // For example, pushing images to a Docker registry
                }
            }
        }
    }

    post {
        always {
            script {
                // Ensure that the Docker Compose services are brought down
                bat 'docker-compose down'
            }
        }
    }
}
