pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_IMAGE_VERSION', defaultValue: '', description: 'Docker Image Version')
        string(name: 'DID_BUILD_APP', defaultValue: '', description: 'Did Build APP')
        string(name: 'DID_BUILD_API', defaultValue: '', description: 'Did Build API')
    }

    stages {
        stage('Checkout Main Branches') {
            steps {
                sh 'git checkout main'
                echo "DOCKER_IMAGE_VERSION: ${params.DOCKER_IMAGE_VERSION}"
                echo "DID_BUILD_VUE: ${params.DID_BUILD_VUE}"
                echo "DID_BUILD_API: ${params.DID_BUILD_API}"
            }
        
        }
        stage('update VUE deploy.yaml') {
            when {
                expression {
                    return params.DID_BUILD_APP == "true"
                }
            }
            steps {
                dir('university-vue'){
                
                    echo "Received Docker Image Version ${params.DOCKER_IMAGE_VERSION}"
                    sh 'git checkout main'
                    sh "sed -i 's|iiijong/university-service:.*|iiijong/university-service:${params.DOCKER_IMAGE_VERSION}|g' deploy.yaml"
                    sh 'cat deploy.yaml'
                }
            }
        }

        stage('update API deploy.yaml') {
            when {
                expression {
                    return params.DID_BUILD_API == "true"
                }
            }
            steps {
                dir('department-api'){
                
                    echo "Received Docker Image Version ${params.DOCKER_IMAGE_VERSION}"
                    sh "sed -i 's|iiijong/department-service:.*|iiijong/department-service:${params.DOCKER_IMAGE_VERSION}|g' deploy.yaml"
                    sh 'cat deploy.yaml'
                }
            }
        }

        stage('Commit & Push') {
            when {
                expression { 
                    return params.DID_BUILD_API == "true" ||  params.DID_BUILD_APP == "true"
                }
            }
            
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