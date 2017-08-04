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
    VAL1 = 'dieci'
  }
  triggers {
    cron('H 1 * * *')
  }
}