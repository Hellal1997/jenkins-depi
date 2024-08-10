pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'e3bb9adf-6f8c-4632-bf74-1b4634a3ac0b', url: 'https://github.com/Hellal1997/jenkins-depi.git', branch: 'test'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("mohamedhellal/DOCKER_TAG:${params.latest}", "-f Dockerfile .")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'af255d4a-5daf-40af-a4c7-b217af9029a9') {
                        docker.image("mohamedhellal/DOCKER_TAG:${params.latest}").push('latest')
                    }
                }
            }
        }
    }
}
