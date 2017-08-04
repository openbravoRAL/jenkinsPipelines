pipeline {
  agent {
    node {
      label 'master'
    }
    
  }

  stages {
    stage('setup') {
      steps {

        echo workspace
        
      }
    }
    stage('stage 1') {
      steps {
        sh 'echo ${VAL1}'
        pwd()
        isUnix()
      }
    }
  }
  environment {
    VAL1 = 'duodieci'
    workspace = pwd()
  }
  triggers {
    cron('H 1 * * *')
  }
}