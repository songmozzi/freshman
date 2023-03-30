pipeline {
    agent any
    
    environment {
        registryCredential = 'kettdocker' // Credential ID 입력
        tag = "latest" // 태그 이름 입력
    }
    
    stages {
        stage('Cloning Git') {
            steps {
                git branch: 'main', url: 'https://github.com/songmozzi/freshman.git'
            }
        }
        
        stage('Building Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/kett/jenkins', registryCredential) {
                        def customImage = docker.build("kett/jenkins:${tag}", ".")
                    }
                }
            }
        }
        
        stage('Pushing Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/kett/jenkins', registryCredential) {
                        def customImage = docker.build("kett/jenkins:${tag}", ".")
                        customImage.push()
                    }
                }
            }
        }
        
        stage('Cleanup') {
            steps {
                sh "docker rmi kett/jenkins:${tag}"
            }
        }
    }
}
