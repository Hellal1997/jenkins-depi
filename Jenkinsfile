pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_TAG', defaultValue: 'latest', description: 'Tag for the Docker image')
    }

    environment {
        // Define Docker image name
        DOCKER_IMAGE_NAME = 'your-docker-image-name'
        // Define Docker registry credentials ID
        DOCKER_CREDENTIALS_ID = 'your-docker-credentials-id'
    }

    triggers {
        // Trigger the build on changes to the Test branch
        scm('H/5 * * * *')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout code from Git repository
                git credentialsId: 'your-github-credentials-id', url: 'https://github.com/your-repo.git', branch: 'Test'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image with the parameterized tag
                    def image = docker.build("${DOCKER_IMAGE_NAME}:${params.DOCKER_TAG}", "-f Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Log in to Docker registry and push Docker image
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        docker.image("${DOCKER_IMAGE_NAME}:${params.DOCKER_TAG}").push("${params.DOCKER_TAG}")
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images to save space
            script {
                sh 'docker system prune -f'
            }
        }
    }
}
