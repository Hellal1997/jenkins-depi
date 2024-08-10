pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'Docker image tag')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                script {
                    // Debugging: List files in workspace
                    sh 'ls -la'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = "mohamedhellal/jenkins/jenkins"
                    def imageTag = "${params.latest}"
                    
                    // Build Docker image
                    docker.build("${imageName}:${imageTag}", "-f Dockerfile .")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("mohamedhellal/jenkins/jenkins:${params.latest}").push("${params.latest}")
                    }
                }
            }
        }
    }
}
