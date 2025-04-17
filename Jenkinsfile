pipeline {
    agent any

    stages {
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
    }
}
