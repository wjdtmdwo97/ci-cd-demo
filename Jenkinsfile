pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Setup Python') {
      steps {
        sh '''
          set -e
          python3 -V || (sudo apt-get update && sudo apt-get install -y python3 python3-pip)
          python3 -m pip install --upgrade pip
        '''
      }
    }
    stage('Install deps') {
      steps { sh 'pip3 install -r requirements.txt' }
    }
    stage('Test') {
      steps { sh 'pytest -q' }
    }
    stage('Archive') {
      steps { archiveArtifacts artifacts: '**/*.py', fingerprint: true }
    }
  }
  post {
    always {
      junit allowEmptyResults: true, testResults: '**/pytest*.xml'
    }
  }
}
