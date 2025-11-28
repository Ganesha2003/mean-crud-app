pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME_FRONTEND = 'rmganesha/mean-frontend'
        IMAGE_NAME_BACKEND = 'rmganesha/mean-backend'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ganesha2003/mean-crud-app.git'
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    sh 'docker-compose build'
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push Images') {
            steps {
                script {
                    // Tag images (ensure these match names built by docker-compose)
                    sh "docker tag job1_frontend:latest $IMAGE_NAME_FRONTEND:latest"
                    sh "docker tag mean_backend:latest $IMAGE_NAME_BACKEND:latest"
                    
                    sh "docker push $IMAGE_NAME_FRONTEND:latest"
                    sh "docker push $IMAGE_NAME_BACKEND:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                // Stop existing containers and start new ones
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
    }
}
