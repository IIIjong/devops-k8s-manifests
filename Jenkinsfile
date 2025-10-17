pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_IMAGE_VERSION', defaultValue: '', description: 'Docker Image Version')
    }

    stages {
        stage('Hello World') {
            steps {
                dir('department-api'){
                    echo "Received Docker Image Version ${params.DOCKER_IMAGE_VERSION}"
                    sh "sed -i 's|iiijong/department-service:.*|iiijong/department-service:${params.DOCKER_IMAGE_VERSION}|g' deploy.yaml"
                    sh 'cat deploy.yaml'
                }
            }
        }
    }
}