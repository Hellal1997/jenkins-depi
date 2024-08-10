pipeline {
    agent any

    parameters {
        string(name: ' custom-nginx', defaultValue: 'nginx', description: 'Docker image to pull')
        string(name: 'latst', defaultValue: 'latest', description: 'Tag of the Docker image')
        booleanParam(name: 'RUN_CONTAINERS', defaultValue: true, description: 'Run Docker containers after pulling the image')
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                script {
                    def imageName = params. custom-nginx
                    def tag = params.latest 
                    echo "Pulling Docker image ${ custom-nginx}:${latest}"
                    sh "docker pull ${ custom-nginx}:${latest}"
                }
            }
        }

        stage('Run Docker Containers') {
            when {
                expression { params.RUN_CONTAINERS }
            }
            steps {
                script {
                    echo "Running Docker container for ${params. custom-nginx}:${params.latest}"
                    sh "docker run -d ${params. custom-nginx}:${params.latest}"
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
