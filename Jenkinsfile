pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  triggers {
    cron('H 1 * * *')
  }
  stages {
    stage('print value') {
      steps {
        sh 'echo ${VAL1}'
      }
    }
  }
  environment {
    VAL1 = 'nove'
  }
}