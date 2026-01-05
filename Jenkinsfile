pipeline {
    agent any
    tools { nodejs "node"}
    environment {
        imageName = "mmadan/jenkins-app"
        registryCredential = 'docker-hub-credentials'
        dockerImage = ''
    }
    stages {
        stage("Install Dependencies"){
            steps {
                sh 'npm install'
            }
        }
        stage("Test"){
            steps {
                sh 'npm test'
            }
        }
        stage("Build Docker Image"){
            steps {
                script {
                    dockerImage = docker.build imageName
                }
            }
        }
        stage("Push Docker Image"){
            steps {
                script {
                    docker.withRegistry('https://registry.docker.com', 'docker-hub-credentials') {
                        dockerImage.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }
}
