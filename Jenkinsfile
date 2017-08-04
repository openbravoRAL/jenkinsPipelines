pipeline {
  agent {
    node {
      label 'master'
    }
  }

  triggers {
      cron('* * * * * *')
  }
  
  stages {
    stage('print value') {
      steps {
        sh 'echo ${VAL1}'
      }
    }
  }
  
  environment {
    VAL1 = 'dos'
  }
}
