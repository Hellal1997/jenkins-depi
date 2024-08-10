pipeline {
    agent any

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
                    sh "docker build -t mohamedhellal/jenkins-depi:${dockerTag} -f Dockerfile ."
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    def dockerTag = "${params.Docker Image Tag}"
                    sh "docker push mohamedhellal/jenkins-depi:${dockerTag}"
                }
            }
        }
    }
}
