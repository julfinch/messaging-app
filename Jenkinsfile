pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  // environment {
  //   DOCKERHUB_CREDENTIALS = credentials('dockerHub')
  // }
  stages {
    stage('Build') {
      steps {
        bat 'docker build -t julfinch/messaging-app:latest .'
      }
    }
    // stage('Login') {
    //   steps {
    //     bat '$DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
    //   }
    // }
    stage('Push') {
      steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
        bat 'docker push julfinch/messaging-app:latest'
        }
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}