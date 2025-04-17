pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('dockerhub-cred')
        IMAGE_NAME = 'aohuuhneyugn/flask-cicd-demo'
    }

    stages {
        stage('Clone source') {
            steps {
                git url: 'https://github.com/aohuuhneyugn/flask-cicd-demo.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh """
                    echo $DOCKER_HUB_CREDENTIALS_PSW | docker login -u $DOCKER_HUB_CREDENTIALS_USR --password-stdin
                    docker push $IMAGE_NAME
                """
            }
        }
    }
}
