pipeline {
    agent any

    environment {
        IMAGE_NAME = "shubhkadam33/html-app:${BUILD_NUMBER}"
        DOCKER_CREDENTIALS = "docker-hub-cred"
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

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-cred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh ''' kubectl apply -f deployment.yaml
                       kubectl set image deployment/html-app html-app=$IMAGE_NAME --record
                '''
            }
        }

        stage('Expose Service') {
            steps {
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
