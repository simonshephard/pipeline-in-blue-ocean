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
      environment {
        CI = 'true'
      }
      steps {
        sh '''chmod 777 ./jenkins/scripts/test.sh
./jenkins/scripts/test.sh'''
      }
    }
    stage('Deliver') {
      steps {
        sh '''chmod 777 ./jenkins/scripts/deliver.sh
./jenkins/scripts/deliver.sh'''
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh '''chmod 777 ./jenkins/scripts/kill.sh
./jenkins/scripts/kill.sh'''
      }
    }
  }
}