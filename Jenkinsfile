pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'saitadikonda99/cloud-devops'  // Changed to "down"
        DOCKER_TAG = 'latest'
        DOCKER_REGISTRY = 'docker.io'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Build Next.js App') {
            steps {
                script {
                    // Build the Next.js application
                    sh 'npm run build'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image for the Next.js app
                    sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
                }
            }
        }

        stage('Login to Docker Registry') {
            steps {
                script {
                    // Login to Docker registry
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to the registry
                    sh 'docker push $DOCKER_IMAGE:$DOCKER_TAG'
                }
            }
        }

        stage('Clean up') {
            steps {
                script {
                    // Clean up Docker images after the push
                    sh 'docker rmi $DOCKER_IMAGE:$DOCKER_TAG'
                }
            }
        }
    }
}

