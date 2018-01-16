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
              script {
                echo 'Adding 30 seconds'
                sleep 30
              }
              
              sleep 30
            }
          }
          stage ('Run Smoke Tests') {
            when { anyOf { branch 'master'; branch 'develop' } }
            steps {
                script{
                sleep 30
                }
              }
            steps {
              echo "Run Smoke Tests against env..." 
            }
        }
      }
    }
}
}
  
