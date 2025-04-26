pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'mahimajain01/flask-docker-app'  // Define your Docker image name
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-credentials'  // Jenkins credentials ID for Docker Hub
        GIT_REPO_URL = 'https://github.com/Mahimajain01/Jenkins-pipeline-setup.git'  // Add this because you used it
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the Git repository
                git branch: 'main', url: "${GIT_REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the root of your project
                    docker.build("${DOCKER_IMAGE}:latest", "-f flask-docker-app/Dockerfile .")
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Authenticate and push the Docker image to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
