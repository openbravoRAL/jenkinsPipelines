pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('setup') {
      steps {
        echo '${workspace}'
      }
    }
    stage('stage 1') {
      steps {
        parallel(
          "step 1": {
            sh 'echo ${VAL1}'
            pwd()
            isUnix()
            
          },
          "step 2": {
            echo 'step 2'
            
          }
        )
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