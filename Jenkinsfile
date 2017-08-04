pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('print value') {
      steps {
        sh 'echo ${VAL1}'
      }
    }
  }
  environment {
    VAL1 = 'tres'
  }
  triggers {
    cron('* * * * * *')
  }
}