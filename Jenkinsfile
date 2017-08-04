pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('stage 1') {
      steps {
        sh 'echo ${VAL1}'
      }
    }
  }
  environment {
    VAL1 = 'undieci'
  }
  triggers {
    cron('H 1 * * *')
  }
}