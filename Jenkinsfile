pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
        IMAGE_NAME = 'aohuuhneyugn/flask-cicd-demo'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aohuuhneyugn/flask-cicd-demo.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh "docker push $IMAGE_NAME"
                }
            }
        }
    }
}
