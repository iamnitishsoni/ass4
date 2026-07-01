pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh "docker build -t rajk18/web-app1:latest ."
            }
        }
        stage('Push') {
            steps {
                docker.withRegistry('', 'docker-hub-credentials-id') {
                    sh "docker push rajk18/web-app1:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                // Force Kubernetes to pull the latest image
                sh "kubectl rollout restart deployment/web-deploy"
            }
        }
    }
}
