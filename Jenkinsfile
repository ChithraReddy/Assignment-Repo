pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ChithraReddy/Assignment-Repo.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building application..."
                sh 'python3 app.py'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
            }
        }
    }
}
