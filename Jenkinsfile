pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'mahimajain01/flask-docker-app'
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-credentials' // Jenkins credentials ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Mahimajain01/Jenkins-pipeline-setup.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker build -t flask-docker-app -f flask-docker-app/Dockerfile .
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    } // <-- This closing brace was missing
} // <-- Added this to properly close the pipeline block
