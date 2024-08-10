pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_IMAGE_TAG', defaultValue: 'latest', description: 'Tag for the Docker image')
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
            def imageName = "mohamedhellal22/jenkins-depi"
            def imageTag = "${params.latest}"
            def image = docker.build("${jenkins}:${lts}")
        }
    }
}

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
