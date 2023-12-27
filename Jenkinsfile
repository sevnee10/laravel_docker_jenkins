pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('rickyca-dockerhub')
  }
  stages {
    // stage('Build') {
    //   steps {
    //     sh 'docker build -t rickyca/rc-alpine:latest .'
    //   }
    // }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push rickyca/rc-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}