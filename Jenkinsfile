pipeline {
    agent any
    environment {
        registry = 'anilkumarbh/pythonapp'
        registryCredential = 'jenkin_docker_token'
        dockerImage = ''
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/ananyasanu622-dot/jen.git']]
                )
            }
        }
        stage('Build Docker image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:latest")
                }
            }
        }
        stage('Push Docker image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
