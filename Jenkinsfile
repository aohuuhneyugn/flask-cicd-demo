pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/aohuuhneyugn/flask-cicd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("flask-cicd-demo")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    dockerImage.run("-p 5000:5000")
                }
            }
        }
    } // <-- Đóng stages ở đây
} // <-- Đóng pipeline ở đây
