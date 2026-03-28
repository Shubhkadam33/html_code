pipeline {
    agent any

    stages {

        stage('Check Files') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t html-app .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }

    }
}
