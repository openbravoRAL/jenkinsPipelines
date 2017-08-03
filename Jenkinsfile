pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('error') {
      steps {
        sh 'echo ${VAL1}'
      }
    }
  }
  environment {
    VAL1 = 'uno'
  }
}