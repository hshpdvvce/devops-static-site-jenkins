pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                // Windows CMD command
                bat 'docker build -t devops-static-site .'
            }
        }

        stage('Stop Old Container') {
            steps {
                // Stop & remove old container if exists (ignore if not)
                bat '''
                docker stop devops-site || echo "No existing container to stop"
                docker rm devops-site || echo "No existing container to remove"
                '''
            }
        }

        stage('Run New Container') {
            steps {
                // Run container on host port 8090
                bat 'docker run -d -p 8090:80 --name devops-site devops-static-site'
            }
        }
    }
}