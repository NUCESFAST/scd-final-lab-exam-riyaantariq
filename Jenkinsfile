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
                script {
                    docker.compose.build()
                }
            }
        }

        stage('Run Docker Containers') {
            steps {
                script {
                    docker.compose.up()
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
                docker.compose.down()
            }
        }
    }
}
