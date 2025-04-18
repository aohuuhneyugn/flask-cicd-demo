pipeline {
    agent any

    environment {
        IMAGE_NAME = "aohuuhneyugn/flask-cicd-demo"
        TAG = "latest"
    }

    stages {
        stage('Clone code') {
            steps {
                git 'https://github.com/aohuuhneyugn/flask-cicd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME:$TAG .'
                }
            }
        }

        stage('Login DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME:$TAG'
            }
        }
    }
}
