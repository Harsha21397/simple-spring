pipeline {
  environment {
    registryCredential = "docker"
  }
  agent any
  stages {
    stage(‘Build’) {
      steps{
        script {
          sh 'mvn clean install'
        }
      }
    }
    stage(‘Load’) {
      steps{
        script {
          app = docker.build("harsha2018/tomcat1")
        }
      }
    }
     stage(‘Deploy’) {
      steps{
        script {
          withDockerRegistry(credentialsId: 'e051c2f9-f61a-409b-a73e-2031c8d2c586', url: 'https://hub.docker.com/') {
           // dockerImage.push()
          app.push("latest")
          }
        }
      }
    }
    stage('Deploy to kubernetes'){
      steps{
            sh 'kubectl apply -f deployment.yaml'
      }
    }
  }
  }
}
