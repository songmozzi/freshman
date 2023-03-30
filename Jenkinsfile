node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("kett/jenkins")
     }
     stage('Push image') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
 }


     stage('Build image') {
         app = docker.build("kett/jenkins") #Push Image 단계에서 빌드번호를 붙이기 때문에 옵션 제거
     }
     stage('Push image') {
         docker.withRegistry('https://registry.hub.docker.com', 'kettdocker') #업로드할 레지스트리 정보, Jenkins Credentials ID {
             app.push("latest") #image에 latest를 태그로 붙인 후 Push
     }
  }
}