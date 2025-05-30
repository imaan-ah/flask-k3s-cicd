pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = 'imanah'
        IMAGE_NAME = 'flask-k3s-cicd'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/imaan-ah/flask-k3s-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_HUB_USER/$IMAGE_NAME:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $DOCKER_HUB_USER/$IMAGE_NAME:latest'
                }
            }
        }

        stage('Deploy to K3s') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
