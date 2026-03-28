pipeline {
    agent any

    environment {
        IMAGE_NAME = "html-app"
    }

    stages {

        stage('Check Files') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }

        stage('Expose Service') {
            steps {
                sh 'kubectl apply -f service.yaml'
            }
        }

    }
}
