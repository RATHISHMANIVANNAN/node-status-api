pipeline {
  agent any

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

    stage('Docker Build & Deploy') {
      steps {
        bat '''
        docker build -t node-status-api:latest .
        docker stop node-status-api || exit 0
        docker rm node-status-api || exit 0
        docker run -d --name node-status-api -p 3000:3000 node-status-api:latest
        '''
      }
    }
  }
}
