pipeline {
  agent any
  environment {
    IMAGE = "jenkins-demo-app"
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install') {
      steps {
        bat 'npm install'
      }
    }
    stage('Test') {
      steps {
        bat 'npm test'
      }
    }
    stage('Build Docker image') {
      steps {
        bat "docker build -t %IMAGE%:${env.BUILD_NUMBER} ."
      }
    }
    stage('Deploy') {
      steps {
        bat "docker stop %IMAGE% || exit 0"
        bat "docker rm %IMAGE% || exit 0"
        bat "docker run -d -p 3000:3000 --name %IMAGE% %IMAGE%:${env.BUILD_NUMBER}"
      }
    }
  }
}
