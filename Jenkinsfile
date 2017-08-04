pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('setup') {
      steps {
        sh 'echo ${VAL1}'
        pwd()
        isUnix()
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