pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  triggers {
    cron('H * * * * *')
  }
  stages {
    stage('print value') {
      steps {
        sh 'echo ${VAL1}'
      }
    }
  }
  environment {
    VAL1 = 'otto'
  }
}