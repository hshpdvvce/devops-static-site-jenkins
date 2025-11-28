pipeline {
    agent any   // run on any available Jenkins agent (your local Jenkins)

    stages {
        stage('Checkout') {
            steps {
                // Jenkins will use the Git repo configured in the job
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image from Dockerfile in this repo
                sh 'docker build -t devops-static-site .'
            }
        }

        stage('Stop Old Container') {
            steps {
                // Stop & remove old container if it exists, ignore errors
                sh '''
                  docker stop devops-site || true
                  docker rm devops-site || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                // Run container mapping port 8090 on host -> 80 in container
                sh 'docker run -d -p 8090:80 --name devops-site devops-static-site'
            }
        }
    }
}