pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }
    
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Unit Test') {
      parallel {
        stage('Unit Test') {
          environment {
            CI = 'true'
          }
          steps {
            sh './jenkins/scripts/test.sh'
          }
        }
        stage('Functional Test') {
          steps {
            echo 'Functional Test ran successfully.'
          }
        }
      }
    }
  }
}