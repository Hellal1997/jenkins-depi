pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'af255d4a-5daf-40af-a4c7-b217af9029a9' // Replace with your Docker Hub credentials ID
        DOCKER_IMAGE_NAME = 'mohamedhellal/jenkins-depi'
    }

    parameters {
        string(name: 'Docker Image Tag', defaultValue: 'latest', description: 'Tag for the Docker image')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'Test', url: 'https://github.com/Hellal1997/jenkins-depi.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerTag = "${params.Docker Image Tag}"
                    sh "docker build -t ${DOCKER_IMAGE_NAME}:${dockerTag} -f Dockerfile ."
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    def dockerTag = "${params.Docker Image Tag}"
                    withCredentials([usernamePassword(credentialsId: af255d4a-5daf-40af-a4c7-b217af9029a9 , passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin"
                        sh "docker push ${DOCKER_IMAGE_NAME}:${dockerTag}"
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images
            sh "docker rmi ${DOCKER_IMAGE_NAME}:${params.Docker Image Tag} || true"
        }
    }
}
