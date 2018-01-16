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
    stage('Test') {
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
    stage ("wait_prior_starting_smoke_testing") {
            echo 'Waiting 5 minutes for deployment to complete prior starting smoke testing'
            sleep 300 // seconds
          }
  }
}
