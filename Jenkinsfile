pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_IMAGE_VERSION', defaultValue: '', description: 'Docker Image Version')
    }

    stages {
        stage('Hello World') {
            steps {
                dir('department-api'){
                    echo "${params.DOCKER_IMAGE_VERSION}"
                }
            }
        }
    }
}