pipeline {
    agent any

    stages {
        stage('Clone source') {
            steps {
                git 'https://github.com/tenban/flask-cicd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("yourdockerhubusername/flask-cicd")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'docker-hub-creds', url: '' ]) {
                    script {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
