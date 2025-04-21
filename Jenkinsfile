pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/aohuuhneyugn/flask-cicd-demo.git'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'pip install -r requirements.txt'
                sh 'pytest test_app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-cicd-demo .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKERHUB_TOKEN')]) {
                    sh 'echo "$DOCKERHUB_TOKEN" | docker login -u aohuuhneyugn --password-stdin'
                    sh 'docker tag flask-cicd-demo aohuuhneyugn/flask-cicd-demo:latest'
                    sh 'docker push aohuuhneyugn/flask-cicd-demo:latest'
                }
            }
        }
    }
}
