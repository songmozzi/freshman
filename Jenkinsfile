pipeline {
    agent any
    environment {
        GIT_URL = "https://github.com/songmozzi/freshman.git"
        imageName = "kett/jenkins:1.0"
        repository = "https://hub.docker.com/repository/docker/kett/"  //docker hub id와 repository 이름
        DOCKERHUB_CREDENTIALS = credentials('kettdocker') // jenkins에 등록해 놓은 docker hub credentials 이름
        dockerImage = '' 
    }

    stages {
        stage('start') {
            steps {
                echo "start jenkins file test"
            }
        }
        stage('pull') {
            steps {
                git url : "${GIT_URL}", branch : "main", poll: true, changelog: true
            }
        }

        stage('Build Image') {
            steps {
                script {
                    docker.withRegistry(repository, DOCKERHUB_CREDENTIALS) {
                        def myImage = docker.build("kett/jenkins:${env.BUILD_NUMBER}", ".") // Docker Image를 빌드합니다.
                        myImage.push() // 생성된 Docker Image를 Docker Hub와 같은 Registry에 등록합니다.
                    }
                }
            }
        }
    }
}
