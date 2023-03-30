pipeline {
    agent any
    
    environment {
        registry = "kett" // Docker Hub Username 입력
        registryCredential = 'kettdocker' // Credential ID 입력
        imageName = "kett/jenkins" // Docker Hub Repository 이름 입력
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
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                        def customImage = docker.build("${registry}/${imageName}:${tag}", ".")
                    }
                }
            }
        }
        
        stage('Pushing Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                        def customImage = docker.build("${registry}/${imageName}:${tag}", ".")
                        customImage.push()
                    }
                }
            }
        }
        
        stage('Cleanup') {
            steps {
                sh "docker rmi ${registry}/${imageName}:${tag}"
            }
        }
    }
}
