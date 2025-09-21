pipeline {
  agent {
    docker {
      image 'python:3.11-slim'
      args  '-u root'
    }
  }
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Install deps') {
      steps {
        sh 'python -m pip install --upgrade pip'
        sh 'pip install -r requirements.txt'
      }
    }
    stage('Test') {
      steps { sh 'pytest -q' }
    }
    stage('Archive') {
      steps { archiveArtifacts artifacts: '**/*.py', fingerprint: true }
    }
  }
}
