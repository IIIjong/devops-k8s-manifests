pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_IMAGE_VERSION', defaultValue: '', description: 'Docker Image Version')
    }

    stages {
        stage('Hello World') {
            steps {
                sh "${params.DOCKER_IMAGE_VERSION}"
            }
        }
    }
}