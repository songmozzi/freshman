pipeline {
    agent {
        dockerfile {
                filename 'Dockerfile.build'
                dir 'build'
                label 'my-defined-label'
                registryUrl 'https://hub.docker.com/repository/docker/kett/jenkins/general'
                registryCredentialsId 'jh'
        }
    }
    environment {
        GIT_URL = "https://github.com/JeongJaeHa/project-test.git"
        imageName = "kett/jenkins:1.0"
        repository = "https://hub.docker.com/repository/docker/kett/jenkins/general"  //docker hub id와 repository 이름
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
                    // def docker = docker()
                    docker.withRegistry('https://hub.docker.com/repository/docker/kett/jenkins/general', DOCKERHUB_CREDENTIALS) {
                        def myImage = docker.build("kett/jenkins:${env.BUILD_NUMBER}", ".") // Docker Image를 빌드합니다.
                        myImage.push() // 생성된 Docker Image를 Docker Hub와 같은 Registry에 등록합니다.
                    }
                }
            }
        }
    }
}

// node {
//   stage('========== Clone repository ==========') {
//     checkout scm
//   }
//   stage('========== Build image ==========') {
//     app = docker.build("jenkins-docker-pipeline/my-image")
//   }
//   stage('========== Push image ==========') {
//     docker.withRegistry('https://hub.docker.com/repository/docker/kett/jenkins/general', 'kettdocker') {
//       app.push("${env.BUILD_NUMBER}")
//       app.push("latest")
//     }
//   }
// }
