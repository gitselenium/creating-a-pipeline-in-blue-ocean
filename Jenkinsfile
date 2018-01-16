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
          stage('Unit Test') 
          {
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
      stage('Build2') {
       def time = params.SLEEP_TIME_IN_SECONDS
    echo "Waiting ${SLEEP_TIME_IN_SECONDS} seconds for deployment to complete prior starting smoke testing"
    sleep time.toInteger() // seconds
      }
  }
}
  
