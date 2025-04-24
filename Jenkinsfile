pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = 'docker-credentials'  // ID of the credentials you created
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image for the Python application'
                    sh 'docker build -t my-python-app .'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    echo 'Pushing Docker image to registry'
                    withDockerRegistry(credentialsId: "$DOCKER_CREDENTIALS") {
                        sh 'docker push my-python-app'
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deploying to Kubernetes...'
                // Add your deployment steps here
            }
        }
    }
}

