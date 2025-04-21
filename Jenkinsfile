pipeline {
    agent any

    environment {
        IMAGE_NAME = 'aohuuhneyugn/flask-cicd-demo'
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Clone code') {
            steps {
                echo 'Cloning repository...'
                // Nếu dùng multibranch thì Jenkins đã tự clone rồi, không cần lặp lại
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Login DockerHub & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-token', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh """
                        echo \$DOCKERHUB_PASSWORD | docker login -u \$DOCKERHUB_USERNAME --password-stdin
                        docker push $IMAGE_NAME:$IMAGE_TAG
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build & push Docker image thành công!'
        }
        failure {
            echo '❌ Build thất bại. Kiểm tra lại các bước.'
        }
    }
}
