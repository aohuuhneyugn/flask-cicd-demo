pipeline {
    agent any

    stages {
        stage('Clone source') {
            steps {
                git url: 'https://github.com/aohuuhneyugn/flask-cicd-demo.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t your-image-name .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push your-image-name
                    """
                }
            }
        }
    }
}
