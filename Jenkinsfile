pipeline {
    agent any

    stage('Clone source') {
    steps {
        git url: 'https://github.com/aohuuhneyugn/flask-cicd-demo.git', branch: 'main'
    }
}

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("aohuuhneyugn/flask-cicd")
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
