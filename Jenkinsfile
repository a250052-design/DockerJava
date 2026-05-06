pipeline {
    agent any

    environment {
        IMAGE_NAME = "java-hello-app"
        CONTAINER_NAME = "java-container"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/a250052-design/DockerJava.git'
            }
        }

        stage('Pull Base Image') {
            steps {
                bat 'docker pull eclipse-temurin:17'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || echo Not running
                docker rm %CONTAINER_NAME% || echo Not exists
                docker run --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }
    }
}
