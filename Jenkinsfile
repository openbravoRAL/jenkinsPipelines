pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('print value') {
      steps {
        parallel(
          "print value": {
            sh 'echo ${VAL1}'
            
          },
          "arbitrary": {
            script {
              pipeline {
                agent {
                  node {
                    label 'master'
                  }
                  
                }
                stages {
                  stage('print value') {
                    steps {
                      sh 'echo ${VAL1} ${VAL1}'
                    }
                  }
                }
              }
            }
            
            
          }
        )
      }
    }
  }
  environment {
    VAL1 = 'nove'
  }
  triggers {
    cron('H 1 * * *')
  }
}