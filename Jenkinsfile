pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = 'rajk18'
        IMAGE_NAME = 'web-app1'
        TAG = 'v1'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:${TAG} ."
            }
        }
        stage('Push to Docker Hub') {
            steps {
                docker.withRegistry('', 'docker-hub-credentials-id') {
                    sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:${TAG}"
                }
            }
        }
        stage('Deploy to Minikube') {
            steps {
                sh "kubectl set image deployment/web-deploy web-deploy=${DOCKER_HUB_USER}/${IMAGE_NAME}:${TAG}"
            }
        }
    }
}
