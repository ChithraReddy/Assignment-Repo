pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'my-python-app'
        DOCKER_REGISTRY = 'docker.io'  
        K8S_CLUSTER = 'my-k8s-cluster'
        K8S_NAMESPACE = 'default'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ChithraReddy/Assignment-Repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image for the Python application"
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing Docker image to registry"
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'docker-credentials') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    echo "Deploying Docker image to Kubernetes"
                    withKubeConfig([credentialsId: 'k8s-credentials', serverUrl: 'https://k8s-cluster.example.com']) {
                        sh '''
                        kubectl apply -f k8s/deployment.yaml --namespace=${K8S_NAMESPACE}
                        kubectl apply -f k8s/service.yaml --namespace=${K8S_NAMESPACE}
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment was successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
