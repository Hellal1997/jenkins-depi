pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_NAME', defaultValue: 'nginx', description: 'Docker image to pull')
        string(name: 'TAG', defaultValue: 'latest', description: 'Tag of the Docker image')
        booleanParam(name: 'RUN_CONTAINERS', defaultValue: true, description: 'Run Docker containers after pulling the image')
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    def imageName = params.IMAGE_NAME
                    def tag = params.TAG
                    echo "Pulling Docker image ${imageName}:${tag}"
                    sh "docker pull ${imageName}:${tag}"
                }
            }
        }

        stage('Run Docker Containers') {
            when {
                expression { params.RUN_CONTAINERS }
            }
            steps {
                script {
                    def imageName = params.IMAGE_NAME
                    def tag = params.TAG
                    echo "Running Docker container for ${imageName}:${tag}"
                    sh "docker run -d ${imageName}:${tag}"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
