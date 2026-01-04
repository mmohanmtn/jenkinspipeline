pipeline {
    agent any
    tools { nodejs "node"}
    environment {
        image = "mmadan/jenkins-app"
        registryCredential = credentials('docker-hub-credential')
        dockerImage = 
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
                    docker.withRegistry('https://registr.docker.com', 'docker-hub-credential') {
                        dockerImage.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }
}
