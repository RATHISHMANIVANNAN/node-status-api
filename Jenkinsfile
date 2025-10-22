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
        sh 'npm ci'
      }
    }

    stage('Docker Build & Deploy') {
      steps {
        sh '''
          docker build -t node-status-api:latest .
          docker stop node-status-api || true
          docker rm node-status-api || true
          docker run -d --name node-status-api -p 3000:3000 node-status-api:latest
        '''
      }
    }
  }
}
