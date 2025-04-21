pipeline {
    agent any
    environment {
        IMAGE_NAME = 'aohuuhneyugn/flask-cicd-demo'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/aohuuhneyugn/flask-cicd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-token', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh '''
                        echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f flask-app || true
                    docker run -d --name flask-app -p 5000:5000 $IMAGE_NAME
                '''
            }
        }
    }
}
