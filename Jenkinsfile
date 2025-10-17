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
                    sh 'git checkout main'
                    sh "sed -i 's|iiijong/department-service:.*|iiijong/department-service:${params.DOCKER_IMAGE_VERSION}|g' deploy.yaml"
                    sh 'cat deploy.yaml'
                }
            }
        }

        stage('Commit & Push') {
            steps {
                
                sh 'git config --list'
                sh 'git config user.name "iiijong"'
                sh 'git config user.email "pjwfish@naver.com"'
                sh 'git config --list'
                sh 'git add .'
                sh "git commit -m 'Update Image Version ${params.DOCKER_IMAGE_VERSION}'"
                sh 'git status'
                sshagent(['github-k8s-manifests']) {
                    sh 'git push'
                }
            }
        }
    }
}