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
                    // List files to debug
                    sh 'ls -la'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = "mohamedhellal22/jenkins-depi"
                    def imageTag = "${params.lts}"
                    
                    // Build Docker image
                    docker.build("${jenkins/jenkins}:${lts}", "-f Dockerfile .")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("mohamedhellal22/jenkins-depi:${params.lts}").push("${params.lts}")
                    }
                }
            }
        }
    }
}
